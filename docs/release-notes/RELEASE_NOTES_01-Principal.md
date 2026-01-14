# 📦 Release Notes - Branch 01-Principal

**Versão:** 2.0.0  
**Data de Release:** Janeiro 2026  
**Branch:** `01-Principal`  
**Base:** Merge de `main` + Novas Funcionalidades

---

## 🎯 Visão Geral

Esta release representa uma **refatoração significativa** do F1 Comunica, focando em:

- ✅ **Novo Modo Designer** - Editor visual interativo para criação de mensagens
- ✅ **Sistema de Configurações Centralizado** - Configurações persistidas via API
- ✅ **Responsividade Completa** - Suporte a telas de 1000x750 até 4K
- ✅ **Correções de QA** - Bugs críticos de agendamento resolvidos
- ✅ **Migração para JavaScript** - Remoção de TypeScript para simplificação

---

## 🚀 Novos Recursos

### 1. 🎨 Modo Designer (Editor Visual)

Um novo modo de edição interativo que oferece experiência visual aprimorada para criação de Adaptive Cards.

#### Componentes Adicionados

| Componente          | Arquivo                                             | Descrição                                 |
| ------------------- | --------------------------------------------------- | ----------------------------------------- |
| **ModeToggle**      | `src/components/V2/designerMode/ModeToggle.js`      | Alternador entre modo Clássico e Designer |
| **DesignerCanvas**  | `src/components/V2/designerMode/DesignerCanvas.js`  | Canvas interativo com seleção visual      |
| **DesignerToolbox** | `src/components/V2/designerMode/DesignerToolbox.js` | Toolbox otimizada para modo visual        |
| **PreviewToggle**   | `src/components/V2/designerMode/PreviewToggle.js`   | Alternador de preview                     |
| **ToolboxHeader**   | `src/components/V2/designerMode/ToolboxHeader.js`   | Header unificado com ações                |

#### Como Usar

1. Acesse **Configurações > Configurações Gerais**
2. Ative o toggle **"Modo Designer como padrão"**
3. Ao criar nova mensagem, o editor abrirá no modo Designer

#### Funcionalidades do Modo Designer

- 📌 **Seleção Visual** - Clique em elementos para selecionar
- 🔄 **Drag & Drop** - Reordene elementos arrastando
- 📋 **Duplicação** - Duplique elementos com um clique
- 👁️ **Preview Integrado** - Visualize o card em tempo real
- 📅 **Agendamento Completo** - Suporte a agendamento com recorrência

---

### 2. ⚙️ Sistema de Configurações Centralizado

Configurações agora são persistidas via API e sincronizadas entre sessões.

#### Configurações Disponíveis

| Configuração          | Chave API               | Descrição                                  |
| --------------------- | ----------------------- | ------------------------------------------ |
| **Enviar para Todos** | `Settings/SendAllUsers` | Habilita/desabilita opção "Todos Usuários" |
| **Modo do Editor**    | `Settings/EditorMode`   | Define modo padrão (classic/designer)      |

#### Onde Configurar

**Navegação:** Menu > Configurações > Configurações Gerais

```
┌─────────────────────────────────────────┐
│  ⚙️ Configurações Gerais                │
├─────────────────────────────────────────┤
│                                         │
│  📤 Controle de Envio                   │
│  ┌─────────────────────────────────┐    │
│  │ Permitir envio para todos      [●]   │
│  │ os usuários                          │
│  └─────────────────────────────────┘    │
│                                         │
│  ✏️ Editor de Mensagens                 │
│  ┌─────────────────────────────────┐    │
│  │ Modo Designer como padrão      [○]   │
│  └─────────────────────────────────┘    │
│                                         │
└─────────────────────────────────────────┘
```

---

### 3. 📱 Layout Responsivo Completo

Sistema agora suporta telas a partir de **1000x750** sem quebra de layout.

#### Breakpoints Implementados

| Resolução       | Comportamento                              |
| --------------- | ------------------------------------------ |
| **≥ 1600px**    | Layout completo 3 colunas (320px laterais) |
| **1366-1600px** | Colunas laterais reduzidas (280px)         |
| **1100-1366px** | Layout compacto (240px laterais)           |
| **1000-1100px** | Layout mínimo (180px laterais)             |
| **< 1000px**    | Layout vertical empilhado                  |

#### Modo Clássico Compacto

Quando `editorMode === "classic"`, o painel de propriedades usa layout simplificado:

- ✅ Blocos empilhados verticalmente
- ✅ Botão único "Enviar Agora" (sem agendamento)
- ✅ Campos de formulário menores
- ✅ Scroll vertical habilitado

---

### 4. 🔍 Sistema de Validação Aprimorado

#### Validação de Mensagens

Novo arquivo `src/helpers/validation/messageValidation.js` com validação completa:

```javascript
const validation = validateMessage(elements, messageProps);
// Retorna: { isValid: boolean, errors: ValidationError[] }
```

#### Diálogo de Erros de Validação

Componente `ValidationErrorsDialog` exibe erros de forma amigável:

- Lista de problemas com ícones
- Navegação direta para elemento com erro
- Contagem de erros no badge

---

### 5. 🗓️ Correções de Agendamento

#### Bugs Corrigidos

| Bug                                        | Solução                                       |
| ------------------------------------------ | --------------------------------------------- |
| Loop infinito ao mudar data                | Implementado `useRef` para controle de estado |
| Hora não carregava ao editar               | Sincronização corrigida no `useEffect`        |
| Valores não anulados ao selecionar "Agora" | Reset completo de campos                      |
| Validação de data mínima                   | 5 minutos de antecedência obrigatório         |
| Horários passados na lista                 | Regeneração dinâmica a cada 30s               |

#### Validação de Agendamento

```javascript
// Data deve ser pelo menos 5min no futuro
if (messageProps.schedule) {
  if (!messageProps.date) return false;
  const scheduled = new Date(messageProps.date).getTime();
  const now = Date.now();
  if (scheduled - now < 5 * 60 * 1000) return false;
}
```

---

## 📁 Estrutura de Arquivos Novos

```
src/
├── components/V2/
│   ├── designerMode/           # 🆕 Novo módulo
│   │   ├── index.js
│   │   ├── ModeToggle.js
│   │   ├── ModeToggle.css
│   │   ├── DesignerCanvas.js
│   │   ├── DesignerCanvas.css
│   │   ├── DesignerToolbox.js
│   │   ├── DesignerToolbox.css
│   │   ├── PreviewToggle.js
│   │   ├── PreviewToggle.css
│   │   ├── ToolboxHeader.js
│   │   └── ToolboxHeader.css
│   ├── messageSendProperties/
│   │   ├── MessageProperties.js  # Refatorado
│   │   ├── MessageProperties.scss
│   │   ├── SendSummary.js        # 🆕 Novo
│   │   └── SendSummary.scss
│   ├── newMessage/
│   │   ├── PreviewActionBar.js   # 🆕 Novo
│   │   ├── PreviewActionBar.scss
│   │   ├── ValidationErrorsDialog.js  # 🆕 Novo
│   │   └── ValidationErrorsDialog.scss
│   └── shared/
│       ├── SharedRenderers.js    # 🆕 Novo
│       ├── SharedRenderers.css
│       └── index.js
├── helpers/
│   └── validation/
│       └── messageValidation.js  # 🆕 Novo
├── hooks/
│   ├── useElementsManager.js     # Refatorado
│   └── useFeedbackToast.js       # Refatorado
└── styles/
    └── variables.scss            # 🆕 Variáveis CSS centralizadas
```

---

## 🔧 Configuração Técnica

### Variáveis de Ambiente

Sem alterações nas variáveis de ambiente.

### Dependências

```json
{
  "@fluentui/react": "^8.x",
  "@fluentui/react-components": "^9.x",
  "@fluentui/react-icons": "^2.x",
  "react": "^18.x",
  "react-datepicker": "^4.x",
  "date-fns": "^2.x"
}
```

### API Endpoints Utilizados

| Endpoint               | Método | Descrição             |
| ---------------------- | ------ | --------------------- |
| `/settings/AppSetting` | GET    | Recupera configuração |
| `/settings`            | POST   | Atualiza configuração |

---

## 🔄 Migração

### De TypeScript para JavaScript

Esta branch remove TypeScript do projeto. Todos os arquivos `.ts`/`.tsx` foram convertidos para `.js`/`.jsx`.

### Arquivos Removidos

- Todos os arquivos `.ts` e `.tsx`
- Configurações TypeScript (`tsconfig.json`, `tsconfig.node.json`)
- Arquivos de teste (pasta `tests/`)
- Documentação antiga (múltiplos arquivos `.md`)
- APIs deprecated (`src/api/`, `src/deprecated_api/`)

---

## 🧪 Testes Recomendados

### Fluxo de Nova Mensagem (Modo Clássico)

1. ✅ Criar nova mensagem
2. ✅ Adicionar texto/imagem/vídeo
3. ✅ Selecionar destinatários (Grupos ou Todos)
4. ✅ Clicar "Enviar Agora"
5. ✅ Confirmar envio

### Fluxo de Nova Mensagem (Modo Designer)

1. ✅ Ativar modo Designer nas configurações
2. ✅ Criar nova mensagem
3. ✅ Usar canvas interativo para adicionar elementos
4. ✅ Alternar para Preview
5. ✅ Configurar destinatários
6. ✅ Escolher "Agora" ou "Agendar"
7. ✅ Confirmar envio/agendamento

### Testes de Responsividade

1. ✅ Testar em 1920x1080
2. ✅ Testar em 1366x768
3. ✅ Testar em 1280x720
4. ✅ Testar em 1024x768
5. ✅ Verificar scroll vertical funciona
6. ✅ Verificar 3 colunas visíveis até 1000px

### Testes de Configuração

1. ✅ Alterar "Permitir envio para todos" → Verificar opção some do seletor
2. ✅ Alterar "Modo Designer" → Verificar editor abre no modo correto
3. ✅ Recarregar página → Verificar configurações persistidas

---

## ⚠️ Breaking Changes

| Item                      | Impacto                       | Mitigação                          |
| ------------------------- | ----------------------------- | ---------------------------------- |
| Remoção de TypeScript     | Projetos que importavam tipos | Usar PropTypes ou JSDoc            |
| APIs deprecated removidas | Código usando `/src/api/`     | Usar `/src/services/apiService.js` |
| Estrutura de pastas       | Imports antigos podem quebrar | Atualizar imports                  |

---

## 📞 Suporte

Para dúvidas ou problemas:

1. Verifique os arquivos de documentação na raiz do projeto
2. Consulte os comentários no código-fonte
3. Entre em contato com a equipe de desenvolvimento

---

## 📝 Changelog Resumido

### Adicionado

- 🆕 Modo Designer com canvas interativo
- 🆕 Sistema de configurações via API
- 🆕 Validação de mensagens aprimorada
- 🆕 Diálogo de erros de validação
- 🆕 Componentes compartilhados (`SharedRenderers`)
- 🆕 Variáveis CSS centralizadas
- 🆕 Suporte a telas 1000x750

### Modificado

- 🔄 `MessageProperties` com modo compacto
- 🔄 `NewMessagePage` com suporte a Designer Mode
- 🔄 Layout responsivo otimizado
- 🔄 Migração de TypeScript para JavaScript

### Corrigido

- 🐛 Loop infinito no agendamento
- 🐛 Hora não carregava ao editar agendada
- 🐛 Validação de data mínima
- 🐛 Reset de campos ao mudar modo de envio
- 🐛 Scroll em telas pequenas

### Removido

- ❌ TypeScript e configurações relacionadas
- ❌ APIs deprecated
- ❌ Documentação obsoleta
- ❌ Testes unitários (serão reimplementados)

---

**Desenvolvido por:** Equipe F1 Comunica  
**Copyright © 2025-2026 FunctionOne Corporate**
