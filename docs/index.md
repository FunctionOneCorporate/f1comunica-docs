# 📚 Documentação F1 Comunica Front

> **Aplicação Front-End para Sistema F1 Comunica**  
> Framework: React 18 + Vite + FluentUI  
> Versão: 2.0.0

---

## 🎯 Visão Geral

F1 Comunica é uma aplicação front-end desenvolvida em React para comunicação interna corporativa, integrada ao Microsoft Teams. Permite criar, agendar e enviar mensagens interativas usando Adaptive Cards para colaboradores e grupos.

---

## 📖 Documentação Disponível

### 🔧 Documentação Técnica
- **[Guia Técnico Completo](./technical/README.md)** - Arquitetura, estrutura, padrões e troubleshooting
- **[Variáveis de Ambiente](./technical/variaveis-ambiente.md)** - Configuração de ambiente
- **[Comandos e Scripts](./technical/comandos.md)** - NPM scripts, build e deploy

### 📘 Manual do Usuário
- **[Manual de Uso](./manual/manual-usuario.md)** - Como usar o sistema
- **[Principais Funcionalidades](./manual/funcionalidades.md)** - Features e fluxos
- **[FAQ - Perguntas Frequentes](./manual/faq.md)** - Dúvidas comuns

### 📝 Release Notes
- **[Histórico de Versões](./release-notes/README.md)** - Todas as versões
- **[Versão 2.0.0 - Principal](./release-notes/RELEASE_NOTES_01-Principal.md)** - Última versão major
- **[Correções de Bugs - Agendamento](./release-notes/CORRECOES_BUGS_AGENDAMENTO.md)**
- **[Melhorias de QA](./release-notes/MELHORIAS_QA_IMPLEMENTADAS.md)**
- **[Melhorias de Responsividade](./release-notes/MELHORIAS_RESPONSIVIDADE_IMPLEMENTADAS.md)**

### 🗺️ Roadmap
- **[Próximas Features](./roadmap/proximas-features.md)** - Planejamento futuro
- **[Backlog Técnico](./roadmap/backlog-tecnico.md)** - Débitos técnicos

---

## 🚀 Quick Start

### Pré-requisitos

- Node.js 16 ou 18
- NPM ou Yarn
- Conta Microsoft 365
- Teams Toolkit Extension (VS Code)

### Instalação

```bash
# 1. Clonar repositório
git clone https://github.com/FunctionOneCorporate/FCConectaFront.git

# 2. Instalar dependências
cd FCConectaFront
npm install

# 3. Configurar variáveis de ambiente
cp env/.env.local.bkp .env.local
# Editar .env.local com suas credenciais

# 4. Executar em desenvolvimento
npm run dev:teamsfx
```

### Build para Produção

```bash
npm run build:teamsfx
```

---

## 🏗️ Estrutura do Projeto

```
FCConectaFront/
├── docs/                    # 📚 Documentação completa
│   ├── manual/             # Manual do usuário
│   ├── release-notes/      # Release notes
│   ├── technical/          # Documentação técnica
│   ├── roadmap/            # Planejamento
│   └── assets/             # Imagens e recursos
├── src/                    # 🔧 Código-fonte
│   ├── components/         # Componentes React
│   ├── contexts/           # Context API
│   ├── hooks/              # Custom hooks
│   ├── services/           # Serviços e API
│   ├── helpers/            # Funções utilitárias
│   ├── styles/             # Estilos globais
│   └── pages/              # Páginas principais
├── public/                 # Arquivos públicos
├── env/                    # Arquivos de ambiente
├── appPackage/             # Manifesto Teams
└── infra/                  # Infraestrutura Azure
```

---

## 🛠️ Principais Tecnologias

| Tecnologia | Versão | Uso |
|------------|--------|-----|
| **React** | 18.x | Framework principal |
| **Fluent UI** | 9.x | Sistema de design Microsoft |
| **React Router** | 6.x | Navegação |
| **Axios** | 0.21.x | Cliente HTTP |
| **Date-fns** | 4.x | Manipulação de datas |
| **Adaptive Cards** | 2.10.x | Cards interativos |
| **MSAL** | 3.x/4.x | Autenticação Microsoft |
| **Teams JS SDK** | 2.13.x | Integração Teams |

---

## 📦 Scripts NPM Disponíveis

| Comando | Descrição |
|---------|-----------|
| `npm start` | Inicia servidor de desenvolvimento |
| `npm run dev:teamsfx` | Desenvolvimento com Teams Toolkit |
| `npm run build` | Build de produção |
| `npm run build:teamsfx` | Build com Teams Toolkit |
| `npm test` | Executa testes |

---

## 🔐 Autenticação

O sistema utiliza **Microsoft Entra ID (Azure AD)** com fluxo **On-Behalf-Of (OBO)** para autenticação:

- Single Sign-On (SSO) com Teams
- Tokens JWT gerenciados pelo MSAL
- Refresh tokens automático
- Suporte a single-tenant

---

## 🌍 Ambientes

| Ambiente | URL | Branch |
|----------|-----|--------|
| **Desenvolvimento** | Local | `develop` |
| **Homologação** | TODO | `staging` |
| **Produção** | TODO | `main` |

---

## 📞 Suporte e Contribuição

### 📧 Contato
- **Equipe**: F1 Comunica Development Team
- **Empresa**: FunctionOne Corporate

### 🐛 Reportar Bugs
1. Verifique se o bug já foi reportado
2. Inclua passos para reproduzir
3. Adicione screenshots quando possível
4. Informe versão do navegador e resolução de tela

### 💡 Sugerir Melhorias
- Abra uma issue descrevendo a feature
- Explique o caso de uso
- Considere impacto em UX

---

## 📄 Licença

Copyright © 2025-2026 FunctionOne Corporate  
Uso interno restrito.

---

## 📚 Links Úteis

- [Microsoft Teams Toolkit](https://aka.ms/teams-toolkit)
- [Fluent UI Documentation](https://react.fluentui.dev/)
- [Adaptive Cards Designer](https://adaptivecards.io/designer/)
- [Microsoft Graph API](https://docs.microsoft.com/graph/)
- [React Documentation](https://react.dev/)

---

**Última Atualização:** Janeiro 2026  
**Versão da Documentação:** 1.0
