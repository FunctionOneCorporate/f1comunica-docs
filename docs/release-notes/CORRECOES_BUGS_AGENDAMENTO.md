---
render_with_liquid: false
---

# 🐛 Correções de Bugs - Agendamento de Mensagens

**Data:** 20 de Dezembro de 2025  
**Contexto:** Correção de bugs críticos relacionados ao agendamento de mensagens e responsividade  
**Resolução testada:** 1020x790

---

## 🎯 Problemas Identificados e Corrigidos

### 1. ❌ **Loop Infinito de Renderização no ScheduleOptionsV2.jsx**

#### **Problema:**

Ao trocar a data no DatePicker, o componente entrava em loop infinito de renderização, travando a interface.

**Causa Raiz:**

```jsx
// ❌ ANTES: useEffect sem controle
useEffect(() => {
  if (selectedDate) {
    setDate(new Date(selectedDate)); // Dispara re-render
  }
}, [selectedDate]); // selectedDate muda → useEffect → onUpdateProperties → pai re-render → selectedDate muda → LOOP
```

O fluxo problemático era:

1. Usuário seleciona data → `setDate()`
2. `useEffect` valida → `onUpdateProperties({ date: scheduledISO })`
3. Componente pai atualiza prop `selectedDate`
4. Prop muda → `useEffect` de sincronização dispara → volta ao passo 2 (LOOP)

#### **Solução Implementada:**

```jsx
import { useEffect, useState, useCallback, useRef } from "react";

const ScheduleOptions = ({
  schedule,
  onScheduleChange,
  onUpdateProperties,
  selectedDate,
}) => {
  const isInitializing = useRef(false); // 🔹 Flag para controlar inicialização
  const lastSentValue = useRef(null); // 🔹 Memorizar último valor enviado

  // 🔹 Sincroniza SOMENTE na montagem inicial
  useEffect(() => {
    if (selectedDate && !isInitializing.current) {
      isInitializing.current = true;
      const d = new Date(selectedDate);
      setDate(d);
      const h = String(d.getHours()).padStart(2, "0");
      const m = String(d.getMinutes()).padStart(2, "0");
      setTime(`${h}:${m}`);
    }
  }, [selectedDate]);

  // 🔹 Validação estável com useCallback
  const validate = useCallback(() => {
    // ... validação ...
    const scheduledISO = scheduled.toISOString();

    // 🔹 SÓ atualiza se mudou (evita loop)
    if (lastSentValue.current !== scheduledISO) {
      lastSentValue.current = scheduledISO;
      onUpdateProperties({ date: scheduledISO });
    }
  }, [date, time, schedule, onUpdateProperties]);

  useEffect(() => {
    validate();
    const interval = setInterval(validate, 30_000);
    return () => clearInterval(interval);
  }, [validate]);
};
```

**Benefícios:**

- ✅ `useRef(isInitializing)` impede sincronizações repetidas
- ✅ `useRef(lastSentValue)` evita chamadas desnecessárias de `onUpdateProperties`
- ✅ `useCallback` estabiliza a função de validação
- ✅ Loop infinito eliminado

---

### 2. ❌ **Valores de Agendamento Não Anulados ao Selecionar "Agora"**

#### **Problema - Estado Persistente:**

Ao selecionar "Enviar Agora" após ter escolhido "Agendar", os campos `date` e `time` permaneciam preenchidos internamente, podendo causar envio acidental de mensagem agendada.

#### **Solução Implementada:**

```jsx
<ChoiceGroup
  selectedKey={selectedSend}
  onChange={(_, o) => {
    const isScheduled = o?.key === "1";
    onScheduleChange(isScheduled);

    // 🔹 Ao selecionar "Agora", limpar data/hora
    if (!isScheduled) {
      setDate(undefined);
      setTime(null);
      setError(null);
      isInitializing.current = false;
    }
  }}
  options={[
    { key: "0", text: "Agora", iconProps: { iconName: "LightningBolt" } },
    { key: "1", text: "Agendar", iconProps: { iconName: "Calendar" } },
  ]}
/>
```

**E na validação:**

```jsx
const validate = useCallback(() => {
  if (!schedule) {
    // 🔹 IMPORTANTE: Ao selecionar "Agora", anular agendamento
    if (lastSentValue.current !== null) {
      lastSentValue.current = null;
      onUpdateProperties({ date: null });
    }
    setError(null);
    return;
  }
  // ... resto da validação
}, [date, time, schedule, onUpdateProperties]);
```

**Benefícios:**

- ✅ Estado limpo ao trocar para "Agora"
- ✅ `onUpdateProperties({ date: null })` garante que pai também limpe
- ✅ Flag `isInitializing` resetada para permitir futura edição

---

### 3. ❌ **Botão "Salvar Mensagem Agendada" Habilitado Sem Campos Obrigatórios**

#### **Problema - Validação Ausente:**

O componente `MessageActions.js` não validava se os campos obrigatórios de agendamento estavam preenchidos, permitindo salvar mensagem agendada inválida.

#### **Antes:**

```jsx
const menuProps = schedule
  ? [
      {
        key: "saveScheduledMessage",
        text: "Salvar Mensagem Agendada",
        onClick: onSaveDraft,
        disabled: false, // ❌ Sempre habilitado
      },
    ]
  : [
      /* ... */
    ];
```

#### **Depois:**

```jsx
const MessageActions = ({ onSend, onSaveDraft, schedule, disableSend }) => {
  // 🔹 Validação adicional: se agendamento, verificar se não está desabilitado
  const canSaveScheduled = schedule && !disableSend;

  const menuProps = schedule
    ? [
        {
          key: "saveScheduledMessage",
          text: "Salvar Mensagem Agendada",
          iconProps: { iconName: "Save" },
          onClick: canSaveScheduled ? onSaveDraft : undefined,
          disabled: !canSaveScheduled, // 🔹 TRAVA: Desabilita se inválido
        },
      ]
    : [
        {
          key: "saveDraft",
          text: "Salvar Rascunho",
          onClick: onSaveDraft,
          disabled: false,
        },
        {
          key: "sendMessage",
          text: "Enviar Mensagem",
          onClick: disableSend ? undefined : onSend,
          disabled: disableSend,
        },
      ];

  return (
    <div className="message-actions-container">
      {/* ... */}
      <PrimaryButton
        text="Finalizar"
        menuProps={{ items: menuProps }}
        split={false}
      />
    </div>
  );
};
```

**Benefícios:**

- ✅ Botão desabilitado quando `disableSend === true`
- ✅ `disableSend` vem da validação `isValidMessage()` do componente pai
- ✅ Consistência: mesma lógica de validação para envio e agendamento

---

### 4. ❌ **Falta de Validação Final do Payload Antes de Enviar**

#### **Problema - Payload Sem Verificação:**

Mesmo com validação no frontend, era possível (por bug ou manipulação) enviar payload com data inválida.

#### **Solução Implementada:**

**No `onSaveDraft` (NewMessagePage.js):**

```jsx
const onSaveDraft = async () => {
  // 🔹 VALIDAÇÃO CRÍTICA: Bloquear se agendamento inválido
  if (messageProps.schedule) {
    if (!messageProps.date) {
      console.error("❌ BLOQUEADO: Agendamento sem data");
      navigate("/home", {
        state: {
          notification: {
            type: "error",
            message: "❌ Data e horário são obrigatórios para agendamento",
          },
        },
      });
      return;
    }

    const scheduledDate = new Date(messageProps.date);

    // Verificar se data é válida
    if (isNaN(scheduledDate.getTime())) {
      console.error("❌ BLOQUEADO: Data inválida");
      navigate("/home", {
        state: {
          notification: {
            type: "error",
            message: "❌ Data de agendamento inválida",
          },
        },
      });
      return;
    }

    // Verificar antecedência mínima de 5 minutos
    const now = Date.now();
    const scheduled = scheduledDate.getTime();
    if (scheduled - now < 5 * 60 * 1000) {
      console.error("❌ BLOQUEADO: Agendamento com menos de 5min");
      navigate("/home", {
        state: {
          notification: {
            type: "error",
            message:
              "❌ Agendamento deve ter no mínimo 5 minutos de antecedência",
          },
        },
      });
      return;
    }

    // ... continua salvamento
  }

  // ... prepara payload e envia
};
```

**No `onSend`:**

```jsx
const onSend = async () => {
  // 🔹 VALIDAÇÃO: Não deve enviar agendamento por este método
  if (messageProps.schedule && messageProps.date) {
    console.error("❌ BLOQUEADO: Tentativa de envio imediato com agendamento");
    navigate("/home", {
      state: {
        notification: {
          type: "error",
          message:
            "❌ Mensagens agendadas devem ser salvas, não enviadas imediatamente",
        },
      },
    });
    return;
  }

  // ... continua envio
};
```

**Benefícios:**

- ✅ Camada extra de validação antes de chamar API
- ✅ Feedback claro ao usuário com mensagens específicas
- ✅ Logs no console para debug
- ✅ Proteção contra payloads corrompidos

---

### 5. ❌ **Breakpoint Incorreto - Componentes Empilhados em 1020x790**

#### **Problema - Responsividade:**

Na resolução 1020x790 (relatada pelo usuário), os componentes ficavam empilhados verticalmente, tornando impossível criar mensagens pois não havia espaço suficiente para visualizar tudo.

**Breakpoint anterior:**

```scss
@media (max-width: 1280px) {
  .new-message-page {
    flex-direction: column; // ❌ Empilhava muito cedo
  }
}
```

#### **Solução Implementada:**

```scss
/* 🔹 1200px - Reduzir ainda mais os painéis laterais */
@media (max-width: 1200px) {
  .toolbox-container,
  .message-properties-container {
    flex: 0 0 18%;
    min-width: 180px;
    max-width: 240px;
  }
}

/* 🔹 1000px - RESOLUÇÃO CRÍTICA - LAYOUT EM COLUNA (antes era 1280px) */
@media (max-width: 1000px) {
  .new-message-page {
    flex-direction: column; // ✅ Empilha apenas abaixo de 1000px
    gap: 12px;
    height: auto;
    padding: 12px;
    margin-top: 12px;
  }

  .toolbox-container {
    max-height: 30vh;
    order: 1;
  }

  .card-renderer-container {
    max-height: 50vh;
    order: 2;
  }

  .message-properties-container {
    max-height: 40vh;
    order: 3;
  }

  /* Todos em largura total */
  .toolbox-container,
  .card-renderer-container,
  .message-properties-container {
    max-width: 100%;
    min-width: 100%;
  }
}
```

**Benefícios:**

- ✅ 1020x790 mantém layout lado a lado (3 colunas)
- ✅ Painéis laterais reduzidos para 18% (180px min)
- ✅ Empilhamento vertical apenas abaixo de 1000px
- ✅ Layout funcional para criar mensagens em resoluções corporativas

---

## 📊 Tabela de Comparação

| Aspecto                          | Antes                      | Depois                                |
| -------------------------------- | -------------------------- | ------------------------------------- |
| **Loop de renderização**         | ❌ Trava ao trocar data    | ✅ Estável com useRef + useCallback   |
| **Limpar ao selecionar "Agora"** | ❌ Valores persistiam      | ✅ Estado limpo automaticamente       |
| **Validação em MessageActions**  | ❌ Botão sempre habilitado | ✅ Desabilitado se campos inválidos   |
| **Validação final do payload**   | ❌ Nenhuma                 | ✅ Tripla verificação antes de enviar |
| **Breakpoint empilhamento**      | 1280px (empilhava cedo)    | 1000px (mantém lado a lado em 1020px) |
| **Feedback ao usuário**          | Console.log genérico       | ✅ Toast com mensagem específica      |

---

## 🧪 Como Testar

### **Teste 1: Loop de Renderização Corrigido**

```
1. Abrir Nova Mensagem
2. Selecionar "Agendar"
3. Trocar data múltiplas vezes
ESPERADO: ✅ Componente responde normalmente, sem travar
```

### **Teste 2: Anular Valores ao Selecionar "Agora"**

```
1. Selecionar "Agendar"
2. Preencher data e hora
3. Selecionar "Agora"
4. Abrir Dev Tools → React DevTools → ver estado do componente
ESPERADO: ✅ date=undefined, time=null, error=null
```

### **Teste 3: Botão Desabilitado Sem Campos**

```
1. Selecionar "Agendar"
2. NÃO preencher data/hora
3. Clicar em "Finalizar" → tentar "Salvar Mensagem Agendada"
ESPERADO: ✅ Opção desabilitada (cinza)
```

### **Teste 4: Validação de Payload**

```
1. Via Dev Tools, forçar messageProps.schedule = true e messageProps.date = null
2. Tentar salvar
ESPERADO: ✅ Bloqueado com toast "❌ Data e horário são obrigatórios"
```

### **Teste 5: Layout em 1020x790**

```
1. Redimensionar navegador para 1020px largura
2. Abrir Nova Mensagem
ESPERADO: ✅ 3 painéis visíveis lado a lado (não empilhados)
```

---

## 🔧 Arquivos Modificados

### 1. **ScheduleOptionsV2.jsx**

**Mudanças:**

- ✅ Adicionado `useRef(isInitializing)` para controlar sincronização inicial
- ✅ Adicionado `useRef(lastSentValue)` para memorizar último valor enviado
- ✅ Refatorado validação com `useCallback` para estabilidade
- ✅ Adicionado limpeza de estado ao selecionar "Agora"
- ✅ Validação anula `date` quando não agendado

### 2. **MessageActions.js**

**Mudanças:**

- ✅ Adicionado variável `canSaveScheduled = schedule && !disableSend`
- ✅ Propriedade `disabled` agora respeita validação para agendamento
- ✅ Consistência entre envio imediato e agendamento

### 3. **NewMessagePage.js**

**Mudanças:**

- ✅ Validação tripla em `onSaveDraft`:
  - Data não pode ser null
  - Data deve ser válida (não NaN)
  - Antecedência mínima de 5 minutos
- ✅ Validação em `onSend`: bloqueia envio imediato de mensagem agendada
- ✅ Feedback com toast específico para cada tipo de erro

### 4. **NewMessagePage.scss**

**Mudanças:**

- ✅ Breakpoint 1280px → 1000px para empilhamento
- ✅ Adicionado breakpoint 1200px intermediário
- ✅ Painéis laterais reduzidos para 18% (180px min) em resoluções médias

---

## 🎯 Resultado Final

### ✅ Problemas Resolvidos:

1. **Loop infinito eliminado** - useRef evita re-sincronizações
2. **Estado limpo ao trocar para "Agora"** - valores anulados automaticamente
3. **Botão bloqueado corretamente** - validação consistente
4. **Payload validado antes de enviar** - 3 camadas de proteção
5. **Layout funcional em 1020x790** - painéis visíveis lado a lado

### 🛡️ Camadas de Proteção Implementadas:

```
Camada 1: ScheduleOptionsV2.jsx
└─ Validação de campos obrigatórios
   └─ onUpdateProperties({ date: null }) se inválido

Camada 2: isValidMessage() (NewMessagePage.js)
└─ Validação completa antes de habilitar botões
   └─ disableSend={!isValidMessage()}

Camada 3: MessageActions.js
└─ Botão desabilitado se disableSend === true
   └─ canSaveScheduled = schedule && !disableSend

Camada 4: onSaveDraft/onSend (NewMessagePage.js)
└─ Validação final do payload antes de chamar API
   └─ Retorna early com toast de erro se inválido
```

---

## 📞 Suporte

**Problemas conhecidos após correções:**

- Nenhum identificado ✅

**Se encontrar bugs:**

1. Abrir Dev Tools → Console
2. Procurar por logs iniciados com `❌ BLOQUEADO:`
3. Verificar mensagem de erro específica
4. Reportar com screenshots e passos para reproduzir

---

## ✍️ Autor

**Front-End Developer** - F1 Comunica  
Data: 20/12/2025  
Versão: 2.1 (Correção de Bugs + Responsividade)
