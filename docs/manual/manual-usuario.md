# 📖 Manual do Usuário - F1 Comunica

> **Guia Completo de Uso da Aplicação**  
> Público-alvo: Usuários finais, Comunicadores, Gestores

---

## 📑 Índice

1. [Visão Geral](#visão-geral)
2. [Acessando o Sistema](#acessando-o-sistema)
3. [Tela Inicial (Home)](#tela-inicial-home)
4. [Criar Nova Mensagem](#criar-nova-mensagem)
5. [Agendar Mensagens](#agendar-mensagens)
6. [Gerenciar Mensagens](#gerenciar-mensagens)
7. [Visualizar Métricas](#visualizar-métricas)
8. [Configurações](#configurações)
9. [Dicas e Boas Práticas](#dicas-e-boas-práticas)

---

## 🎯 Visão Geral

O **F1 Comunica** é uma ferramenta de comunicação interna integrada ao Microsoft Teams que permite:

- ✅ Criar mensagens interativas com cards visuais
- ✅ Enviar comunicados para grupos específicos ou todos os usuários
- ✅ Agendar mensagens para envio futuro
- ✅ Acompanhar métricas de entrega e visualização
- ✅ Gerenciar histórico de comunicações

### Principais Funcionalidades

| Funcionalidade | Descrição |
|----------------|-----------|
| **Editor de Mensagens** | Crie mensagens ricas com texto, imagens, vídeos e botões |
| **Agendamento** | Programe envios para datas e horários específicos |
| **Recorrência** | Configure envios recorrentes (diário, semanal, mensal) |
| **Destinatários** | Escolha grupos específicos ou todos os usuários |
| **Dashboard** | Visualize métricas e estatísticas |
| **Histórico** | Acesse mensagens enviadas, agendadas e rascunhos |

---

## 🚪 Acessando o Sistema

### Através do Microsoft Teams

1. **Abra o Microsoft Teams**
2. **Localize o app F1 Comunica** na barra lateral esquerda
3. **Clique no ícone** para abrir a aplicação
4. **Aguarde o carregamento** - A autenticação é automática (SSO)

### Primeira Vez

Na primeira vez que acessar:

1. O Teams pode solicitar permissão para acessar seus dados
2. Clique em **"Aceitar"** ou **"Permitir"**
3. A aplicação será carregada automaticamente

---

## 🏠 Tela Inicial (Home)

A tela inicial exibe um dashboard completo com:

### 1. Cards de Métricas (Topo)

```
┌────────────────┬────────────────┬────────────────┐
│  Comunicados   │   Recebidos    │  Visualizados  │
│      150       │      142       │      128       │
└────────────────┴────────────────┴────────────────┘
```

- **Comunicados**: Total de mensagens enviadas
- **Recebidos**: Mensagens entregues com sucesso
- **Visualizados**: Mensagens lidas pelos colaboradores

### 2. Gráfico de Comunicados (Centro)

Visualização mensal de comunicados enviados com:
- Total de mensagens por mês
- Mensagens lidas vs não lidas
- Filtro por ano

### 3. Atividades Recentes (Lateral Direita)

Lista das últimas ações realizadas:
- Mensagens enviadas
- Agendamentos criados
- Rascunhos salvos

### Navegação Principal

```
┌─────────────────────────────────┐
│  [Home] [Mensagens] [Calendário]│
│  [Configurações]                │
└─────────────────────────────────┘
```

---

## ✍️ Criar Nova Mensagem

### Passo 1: Acessar o Editor

1. Clique em **"Nova Mensagem"** ou **"+"** no menu
2. O editor será aberto

### Passo 2: Escolher Modo de Edição

#### **Modo Clássico** (Padrão)

Interface tradicional com 3 painéis:

```
┌──────────┬────────────────┬─────────────┐
│ Toolbox  │   Preview      │ Properties  │
│          │                │             │
│ - Texto  │  [Card Visual] │ Destinários │
│ - Imagem │                │ Agendamento │
│ - Vídeo  │                │ Recorrência │
│ - Botão  │                │             │
└──────────┴────────────────┴─────────────┘
```

**Como usar:**
1. Arraste elementos da Toolbox para o card
2. Configure cada elemento no painel direito
3. Visualize o resultado em tempo real no centro

#### **Modo Designer** (Novo)

Interface visual interativa:

- Clique diretamente nos elementos para editar
- Drag & Drop para reordenar
- Preview integrado
- Mais intuitivo para usuários não técnicos

**Ativar Modo Designer:**
1. Vá em **Configurações > Configurações Gerais**
2. Ative **"Modo Designer como padrão"**

### Passo 3: Adicionar Conteúdo

#### Adicionar Texto

1. Clique em **"Texto"** ou arraste o elemento
2. Digite o conteúdo
3. Configure estilo:
   - Tamanho (Pequeno, Médio, Grande)
   - Peso (Normal, Negrito)
   - Cor
   - Alinhamento

#### Adicionar Imagem

1. Clique em **"Imagem"**
2. Escolha a fonte:
   - **Upload**: Envie arquivo do computador (JPG, PNG)
   - **URL**: Cole link direto da imagem
3. Ajuste tamanho e alinhamento

#### Adicionar Vídeo

1. Clique em **"Vídeo"**
2. Cole a URL do vídeo (YouTube, Vimeo, Stream)
3. Configure thumbnail (opcional)

#### Adicionar Botão

1. Clique em **"Botão"**
2. Configure:
   - Texto do botão
   - Ação:
     - **Abrir URL**: Link externo
     - **Enviar dados**: Callback ao backend
   - Estilo (Primário, Secundário)

### Passo 4: Configurar Destinatários

No painel **Propriedades** (direita):

1. **Selecionar Grupos**
   - Escolha um ou mais grupos
   - Visualize quantidade de membros

2. **Todos os Usuários** (se habilitado)
   - Envia para toda a organização
   - ⚠️ Use com cautela

### Passo 5: Configurar Envio

#### Envio Imediato

1. Selecione **"Enviar Agora"**
2. Clique em **"Finalizar > Enviar Mensagem"**
3. Confirme o envio

#### Envio Agendado

1. Selecione **"Agendar"**
2. Escolha **Data** (calendário)
3. Escolha **Hora** (dropdown)
   - ⚠️ Mínimo 5 minutos no futuro
4. Configure **Recorrência** (opcional):
   - Única (sem repetição)
   - Diária
   - Semanal
   - Mensal
5. Clique em **"Finalizar > Salvar Mensagem Agendada"**

---

## 📅 Agendar Mensagens

### Validações Importantes

- ✅ Data deve ser futura
- ✅ Hora deve ter pelo menos **5 minutos** de antecedência
- ✅ Data e hora são **obrigatórios** para agendamento
- ✅ Horários passados são automaticamente atualizados

### Tipos de Recorrência

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| **Única** | Envio único na data especificada | Comunicado especial |
| **Diária** | Repetir todos os dias | Lembretes diários |
| **Semanal** | Repetir a cada 7 dias | Relatórios semanais |
| **Mensal** | Repetir a cada 30 dias | Newsletters mensais |

### Editar Mensagem Agendada

1. Acesse **"Mensagens"** no menu
2. Filtre por **"Agendadas"**
3. Clique na mensagem desejada
4. Edite os campos necessários
5. Clique em **"Salvar"**

### Cancelar Agendamento

1. Acesse a mensagem agendada
2. Clique em **"Cancelar Agendamento"**
3. Confirme a ação

---

## 📋 Gerenciar Mensagens

### Visualizar Lista de Mensagens

Acesse **"Mensagens"** no menu para ver:

```
┌────────────────────────────────────────┐
│ Filtros: [Todas] [Enviadas] [Agendadas]│
│         [Rascunhos] [Canceladas]       │
├────────────────────────────────────────┤
│ Título       | Status    | Data        │
├────────────────────────────────────────┤
│ Comunicado 1 | Enviada   | 10/01/2026  │
│ Reunião Team | Agendada  | 15/01/2026  │
│ Rascunho     | Rascunho  | 08/01/2026  │
└────────────────────────────────────────┘
```

### Filtros Disponíveis

- **Todas**: Exibe todas as mensagens
- **Enviadas**: Apenas mensagens já enviadas
- **Agendadas**: Mensagens programadas
- **Rascunhos**: Mensagens salvas, não enviadas
- **Canceladas**: Mensagens canceladas

### Buscar Mensagem

Use a barra de busca para:
- Buscar por título
- Filtrar por data
- Buscar por autor

### Ações Disponíveis

Para cada mensagem, você pode:

| Ação | Quando Disponível | Descrição |
|------|-------------------|-----------|
| **Visualizar** | Todas | Ver detalhes completos |
| **Editar** | Rascunhos, Agendadas | Modificar conteúdo |
| **Duplicar** | Todas | Criar cópia |
| **Cancelar** | Agendadas | Cancelar envio |
| **Excluir** | Rascunhos | Remover permanentemente |

---

## 📊 Visualizar Métricas

### Dashboard Principal

Na tela inicial (Home), você encontra:

#### 1. Métricas Resumidas

- **Comunicados Gerados**: Total de mensagens criadas
- **Recebidos**: Entregas confirmadas
- **Visualizados**: Mensagens abertas pelos usuários

#### 2. Gráfico Mensal

Visualize a evolução mensal de comunicados:
- Total por mês
- Taxa de leitura
- Comparativo anual

#### 3. Métricas por Mensagem

Clique em uma mensagem para ver:
- Total de destinatários
- Entregas bem-sucedidas
- Falhas (se houver)
- Taxa de abertura
- Cliques em botões (se aplicável)

### Interpretar Métricas

| Métrica | Boa Performance | Atenção Necessária |
|---------|-----------------|-------------------|
| **Taxa de Entrega** | > 95% | < 90% |
| **Taxa de Abertura** | > 70% | < 50% |
| **Taxa de Cliques** | > 30% | < 10% |

---

## ⚙️ Configurações

### Acessar Configurações

1. Clique em **"Configurações"** no menu
2. Selecione **"Configurações Gerais"**

### Opções Disponíveis

#### 1. Controle de Envio

**Permitir envio para todos os usuários**
- Quando ativo: Opção "Todos" disponível no seletor
- Quando inativo: Apenas grupos específicos

#### 2. Editor de Mensagens

**Modo Designer como padrão**
- Quando ativo: Nova mensagem abre no modo Designer
- Quando inativo: Abre no modo Clássico

### Salvar Configurações

1. Altere as opções desejadas
2. Clique em **"Salvar"**
3. Confirmação aparecerá no topo da tela

---

## 💡 Dicas e Boas Práticas

### Criação de Mensagens

✅ **Faça:**
- Use títulos claros e objetivos
- Mantenha o texto conciso (máximo 200 palavras)
- Use imagens de boa qualidade (mínimo 800x600px)
- Teste o preview antes de enviar
- Inclua call-to-action claro (botões)

❌ **Evite:**
- Textos muito longos ou complexos
- Imagens de baixa resolução
- Excesso de cores ou fontes
- Mensagens sem contexto claro
- Spam (envios muito frequentes)

### Agendamento

✅ **Recomendado:**
- Agende com pelo menos 1 hora de antecedência
- Prefira horários comerciais (8h às 18h)
- Evite fins de semana e feriados
- Use recorrência para comunicados regulares

❌ **Evite:**
- Agendar com pouca antecedência (< 5min)
- Horários fora do expediente sem necessidade
- Recorrência muito frequente (fadiga)

### Destinatários

✅ **Boas Práticas:**
- Segmente bem o público (use grupos específicos)
- Valide se o grupo está correto antes de enviar
- Evite "Todos" para comunicados não críticos
- Mantenha grupos atualizados

### Métricas

✅ **Análise:**
- Acompanhe taxa de abertura semanalmente
- Compare performance entre comunicados
- Identifique melhores horários de envio
- Ajuste estratégia baseado nos dados

---

## ❓ Perguntas Frequentes

### 1. Posso editar uma mensagem já enviada?
**Não.** Mensagens enviadas não podem ser editadas. Você pode:
- Enviar uma correção/atualização
- Duplicar e enviar nova versão

### 2. Como sei se minha mensagem foi entregue?
- Acesse a mensagem na lista
- Verifique as métricas de entrega
- Status "Enviada" indica sucesso

### 3. Posso agendar uma mensagem para vários horários?
Sim, use **Recorrência**:
- Diária: Repete todo dia
- Semanal: Repete toda semana
- Mensal: Repete todo mês

### 4. O que acontece se eu sair do Teams durante o envio?
Nada. O envio acontece no servidor, não depende de você estar online.

### 5. Posso anexar arquivos nas mensagens?
Atualmente, não. Você pode:
- Adicionar links para download
- Usar botões com URLs
- Incluir imagens inline

---

## 📞 Suporte

### Precisa de Ajuda?

- 📧 **Email:** suporte-f1comunica@functionone.com.br
- 💬 **Teams:** Canal #f1-comunica-suporte
- 📚 **Documentação:** [/docs](../index.md)

### Reportar Problema

1. Descreva o problema
2. Inclua passos para reproduzir
3. Adicione screenshots
4. Informe navegador e resolução de tela

---

**Última Atualização:** Janeiro 2026  
**Versão do Manual:** 1.0
