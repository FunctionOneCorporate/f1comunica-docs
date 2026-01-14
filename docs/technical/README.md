# 🔧 Guia Técnico - F1 Comunica Front

> **Documentação técnica completa para desenvolvedores**  
> Público-alvo: Desenvolvedores, DevOps, Arquitetos

---

## 📑 Índice

1. [Arquitetura](#arquitetura)
2. [Estrutura de Pastas](#estrutura-de-pastas)
3. [Padrões de Código](#padrões-de-código)
4. [Configuração de Ambiente](#configuração-de-ambiente)
5. [Comandos e Scripts](#comandos-e-scripts)
6. [Build e Deploy](#build-e-deploy)
7. [Fluxo de Autenticação](#fluxo-de-autenticação)
8. [Integração com API](#integração-com-api)
9. [Context API e Estado Global](#context-api-e-estado-global)
10. [Componentes Principais](#componentes-principais)
11. [Troubleshooting](#troubleshooting)

---

## 🏛️ Arquitetura

### Stack Tecnológico

```
┌─────────────────────────────────────────┐
│         Microsoft Teams                 │
│      (Container/Host Application)       │
├─────────────────────────────────────────┤
│         F1 Comunica Front               │
│         React 18 + Vite                 │
├─────────────────────────────────────────┤
│         Fluent UI 9.x                   │
│    (Microsoft Design System)            │
├─────────────────────────────────────────┤
│       MSAL (Authentication)             │
│     Microsoft Entra ID (Azure AD)       │
├─────────────────────────────────────────┤
│         Backend API                     │
│     (ASP.NET Core / Azure)              │
└─────────────────────────────────────────┘
```

### Fluxo de Dados

```
User Action → Component → Custom Hook → Context API → Service Layer → Backend API
     ↓                                      ↓                              ↓
  UI Update ← Component ← Context Update ← Response ← API Response
```

### Padrão de Arquitetura

O projeto segue uma arquitetura **Component-Based** com:

- **Separação de Responsabilidades** (SoC)
- **Composition Pattern** para reusabilidade
- **Context API** para estado global
- **Custom Hooks** para lógica reutilizável
- **Service Layer** para comunicação com API

---

## 📁 Estrutura de Pastas

```
src/
├── components/              # Componentes React
│   └── V2/                 # Nova versão (refatoração)
│       ├── Home/           # Dashboard principal
│       ├── newMessage/     # Editor de mensagens
│       ├── MessageList/    # Lista de mensagens
│       ├── Calendar/       # Visualização de calendário
│       ├── designerMode/   # Modo designer (editor visual)
│       ├── messageSendProperties/  # Propriedades de envio
│       └── shared/         # Componentes compartilhados
│
├── contexts/               # Context API (Estado Global)
│   ├── AuthContext.jsx    # Autenticação
│   ├── MessageContext.jsx # Mensagens
│   └── SettingsContext.jsx # Configurações
│
├── hooks/                  # Custom Hooks
│   ├── useAuth.js         # Hook de autenticação
│   ├── useElements.js     # Gerenciamento de elementos
│   ├── useFeedbackToast.js # Notificações toast
│   └── useElementsManager.js # Manager de elementos Adaptive Card
│
├── services/              # Camada de serviços
│   ├── apiService.js     # Cliente HTTP (Axios)
│   ├── authService.js    # Serviços de autenticação
│   └── messageService.js # Serviços de mensagens
│
├── helpers/               # Funções utilitárias
│   ├── validation/       # Validações
│   ├── dateHelpers.js    # Manipulação de datas
│   └── formatters.js     # Formatadores
│
├── styles/               # Estilos globais
│   ├── global.scss       # Estilos globais
│   ├── variables.scss    # Variáveis CSS
│   └── themes/           # Temas customizados
│
├── pages/                # Páginas (rotas)
│   ├── HomePage.jsx
│   ├── NewMessagePage.jsx
│   └── SettingsPage.jsx
│
├── assets/               # Recursos estáticos
│   ├── images/
│   └── icons/
│
├── App.jsx               # Componente raiz
├── index.jsx             # Entry point
└── configVars.jsx        # Configurações da aplicação
```

### Convenções de Nomenclatura

- **Componentes**: PascalCase (ex: `MessageList.jsx`)
- **Hooks**: camelCase com prefixo `use` (ex: `useAuth.js`)
- **Contextos**: PascalCase com sufixo `Context` (ex: `AuthContext.jsx`)
- **Serviços**: camelCase com sufixo `Service` (ex: `apiService.js`)
- **Utilitários**: camelCase (ex: `dateHelpers.js`)

---

## 💻 Padrões de Código

### Componentes React

```javascript
// ✅ Padrão recomendado: Function Component com hooks
import React, { useState, useEffect } from 'react';
import { Button } from '@fluentui/react-components';

/**
 * Componente de exemplo
 * @param {Object} props - Propriedades do componente
 * @param {string} props.title - Título
 * @param {Function} props.onAction - Callback de ação
 */
const ExampleComponent = ({ title, onAction }) => {
  const [state, setState] = useState(null);

  useEffect(() => {
    // Setup
    return () => {
      // Cleanup
    };
  }, []);

  return (
    <div className="example-component">
      <h2>{title}</h2>
      <Button onClick={onAction}>Ação</Button>
    </div>
  );
};

export default ExampleComponent;
```

### Custom Hooks

```javascript
// ✅ Padrão de custom hook
import { useState, useEffect } from 'react';

/**
 * Hook para gerenciar dados de mensagens
 * @returns {Object} { data, loading, error, refresh }
 */
export const useMessages = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchData = async () => {
    setLoading(true);
    try {
      const response = await apiService.get('/messages');
      setData(response.data);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchData();
  }, []);

  return { data, loading, error, refresh: fetchData };
};
```

### Context API

```javascript
// ✅ Padrão de Context com Provider
import React, { createContext, useContext, useState } from 'react';

const MessageContext = createContext();

export const MessageProvider = ({ children }) => {
  const [messages, setMessages] = useState([]);

  const addMessage = (message) => {
    setMessages([...messages, message]);
  };

  return (
    <MessageContext.Provider value={{ messages, addMessage }}>
      {children}
    </MessageContext.Provider>
  );
};

// Hook customizado para usar o contexto
export const useMessageContext = () => {
  const context = useContext(MessageContext);
  if (!context) {
    throw new Error('useMessageContext must be used within MessageProvider');
  }
  return context;
};
```

### Service Layer

```javascript
// ✅ Padrão de serviço
import axios from 'axios';

const BASE_URL = process.env.REACT_APP_API_URL;

class MessageService {
  async getAll() {
    try {
      const response = await axios.get(`${BASE_URL}/messages`);
      return response.data;
    } catch (error) {
      console.error('Error fetching messages:', error);
      throw error;
    }
  }

  async create(messageData) {
    try {
      const response = await axios.post(`${BASE_URL}/messages`, messageData);
      return response.data;
    } catch (error) {
      console.error('Error creating message:', error);
      throw error;
    }
  }
}

export default new MessageService();
```

---

## ⚙️ Configuração de Ambiente

### Variáveis de Ambiente

O projeto utiliza variáveis de ambiente para configuração. Arquivos disponíveis:

```
env/
├── .env.f1treina          # Ambiente F1 Treina
├── .env.local.bkp         # Backup configuração local
└── .env.local.user.bkp    # Backup usuário específico
```

### Variáveis Principais

| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `REACT_APP_API_URL` | URL da API backend | `https://api.f1comunica.com` |
| `REACT_APP_CLIENT_ID` | Client ID Azure AD | `xxxxx-xxxx-xxxx-xxxx` |
| `REACT_APP_TENANT_ID` | Tenant ID Azure AD | `xxxxx-xxxx-xxxx-xxxx` |
| `REACT_APP_SCOPE` | Scopes de autenticação | `api://xxx/.default` |

### Configurar Ambiente Local

```bash
# 1. Copiar arquivo de exemplo
cp env/.env.local.bkp .env.local

# 2. Editar com suas credenciais
nano .env.local

# 3. Executar com configuração
npm run dev:teamsfx
```

---

## 🚀 Comandos e Scripts

### Scripts NPM

| Comando | Descrição | Quando usar |
|---------|-----------|-------------|
| `npm start` | Inicia dev server padrão | Desenvolvimento React simples |
| `npm run dev:teamsfx` | Dev com Teams Toolkit | **Desenvolvimento recomendado** |
| `npm run build` | Build de produção | Build padrão React |
| `npm run build:teamsfx` | Build com Teams Toolkit | **Build para deploy Teams** |
| `npm test` | Executa testes | CI/CD e validação |
| `npm run eject` | Eject do CRA | ⚠️ Não recomendado |

### Comandos de Debug

```bash
# Abrir DevTools no Teams
Ctrl+Shift+I (Windows) ou Cmd+Option+I (Mac)

# Limpar cache
npm run clean
rm -rf node_modules package-lock.json
npm install

# Verificar versão Node
node -v  # Deve ser 16.x ou 18.x

# Verificar dependências
npm list --depth=0
```

---

## 📦 Build e Deploy

### Build Local

```bash
# 1. Instalar dependências
npm install

# 2. Build com Teams Toolkit
npm run build:teamsfx

# 3. Output gerado em /build
ls -la build/
```

### Deploy Azure (via Teams Toolkit)

```bash
# 1. Login Azure
az login

# 2. Provisionar recursos
teamsfx provision

# 3. Deploy
teamsfx deploy

# 4. Publicar no Teams
teamsfx publish
```

### Estrutura de Build

```
build/
├── static/
│   ├── css/          # CSS minificado
│   ├── js/           # JS bundles
│   └── media/        # Imagens/fonts
├── index.html        # HTML principal
├── manifest.json     # Manifest PWA
└── asset-manifest.json  # Mapa de assets
```

---

## 🔐 Fluxo de Autenticação

### On-Behalf-Of (OBO) Flow

```
1. User → Teams → F1 Comunica (SSO Token)
2. F1 Comunica → Exchange token → Backend API
3. Backend → Validate → Microsoft Entra ID
4. Microsoft Entra ID → Return Access Token
5. Backend → Use Token → Call Graph API (if needed)
6. Backend → Return Data → F1 Comunica
```

### Implementação MSAL

```javascript
// Configuração MSAL
const msalConfig = {
  auth: {
    clientId: process.env.REACT_APP_CLIENT_ID,
    authority: `https://login.microsoftonline.com/${process.env.REACT_APP_TENANT_ID}`,
    redirectUri: window.location.origin,
  },
  cache: {
    cacheLocation: 'sessionStorage',
    storeAuthStateInCookie: false,
  },
};

// Inicializar
const msalInstance = new PublicClientApplication(msalConfig);

// Adquirir token silenciosamente
const getToken = async () => {
  const request = {
    scopes: [process.env.REACT_APP_SCOPE],
  };
  
  try {
    const response = await msalInstance.acquireTokenSilent(request);
    return response.accessToken;
  } catch (error) {
    // Fallback para login interativo
    const response = await msalInstance.acquireTokenPopup(request);
    return response.accessToken;
  }
};
```

---

## 🌐 Integração com API

### Cliente HTTP (Axios)

```javascript
// src/services/apiService.js
import axios from 'axios';
import { getToken } from './authService';

const apiClient = axios.create({
  baseURL: process.env.REACT_APP_API_URL,
  timeout: 30000,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Interceptor para adicionar token
apiClient.interceptors.request.use(async (config) => {
  const token = await getToken();
  config.headers.Authorization = `Bearer ${token}`;
  return config;
});

// Interceptor para tratar erros
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // Token expirado - renovar
      return refreshTokenAndRetry(error.config);
    }
    return Promise.reject(error);
  }
);

export default apiClient;
```

### Endpoints Principais

| Endpoint | Método | Descrição |
|----------|--------|-----------|
| `/messages` | GET | Lista mensagens |
| `/messages` | POST | Cria mensagem |
| `/messages/{id}` | GET | Detalhes mensagem |
| `/messages/{id}` | PUT | Atualiza mensagem |
| `/messages/{id}` | DELETE | Remove mensagem |
| `/settings/AppSetting` | GET | Obtém configuração |
| `/settings` | POST | Atualiza configuração |
| `/SentNotifications/metrics` | GET | Métricas de envio |

---

## 🗂️ Context API e Estado Global

### Contextos Disponíveis

#### 1. AuthContext
Gerencia autenticação e usuário logado

```javascript
const { user, isAuthenticated, login, logout } = useAuth();
```

#### 2. MessageContext
Gerencia mensagens e operações

```javascript
const { 
  messages, 
  sentMetrics, 
  fetchMessages, 
  createMessage,
  updateMessage,
  deleteMessage 
} = useMessageContext();
```

#### 3. SettingsContext
Gerencia configurações da aplicação

```javascript
const { 
  settings, 
  updateSetting, 
  editorMode,
  sendAllUsersEnabled 
} = useSettings();
```

---

## 🧩 Componentes Principais

### NewMessagePage
Editor de mensagens com dois modos:
- **Modo Clássico**: Editor baseado em toolbox
- **Modo Designer**: Editor visual com canvas interativo

### MessageList
Lista de mensagens com filtros, ordenação e paginação

### Calendar
Visualização de calendário com mensagens agendadas

### ScheduleOptions
Componente de agendamento com validação completa

### MessageProperties
Painel de propriedades para configuração de envio

---

## 🔍 Troubleshooting

### Problema: Token expirado
**Solução:**
```javascript
// Forçar renovação de token
await msalInstance.acquireTokenPopup(request);
```

### Problema: Build falha
**Solução:**
```bash
# Limpar cache e reinstalar
rm -rf node_modules package-lock.json build
npm install
npm run build:teamsfx
```

### Problema: API retorna 401
**Solução:**
- Verificar variáveis de ambiente
- Validar token no jwt.io
- Verificar scopes configurados

### Problema: Layout quebrado
**Solução:**
- Limpar cache do navegador
- Verificar versão do Fluent UI
- Testar em navegador diferente

---

## 📚 Recursos Adicionais

- [React Documentation](https://react.dev/)
- [Fluent UI](https://react.fluentui.dev/)
- [Teams Toolkit](https://aka.ms/teams-toolkit)
- [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)
- [Adaptive Cards](https://adaptivecards.io/)

---

**Última Atualização:** Janeiro 2026  
**Versão:** 1.0
