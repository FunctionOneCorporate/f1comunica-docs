# ❓ FAQ - Perguntas Frequentes

> **Respostas rápidas para dúvidas comuns**  
> Público-alvo: Todos os usuários

---

## 📑 Categorias

- [Acesso e Login](#acesso-e-login)
- [Criação de Mensagens](#criação-de-mensagens)
- [Agendamento](#agendamento)
- [Destinatários](#destinatários)
- [Métricas](#métricas)
- [Problemas Técnicos](#problemas-técnicos)

---

## 🚪 Acesso e Login

### Como acesso o F1 Comunica?

O F1 Comunica é um app do Microsoft Teams. Para acessar:

1. Abra o Microsoft Teams
2. Localize o ícone do F1 Comunica na barra lateral esquerda
3. Clique para abrir

### Preciso fazer login separadamente?

**Não.** O sistema usa autenticação automática (SSO - Single Sign-On) do Teams. Se você está logado no Teams, está automaticamente logado no F1 Comunica.

### Não consigo encontrar o app no Teams. O que fazer?

1. Verifique se você tem permissão de acesso
2. Entre em contato com o administrador do Teams
3. Verifique se o app foi instalado para sua organização

### Posso usar o F1 Comunica fora do Teams?

Atualmente, **não**. O sistema é exclusivo para Microsoft Teams.

---

## ✍️ Criação de Mensagens

### Qual a diferença entre Modo Clássico e Modo Designer?

| Aspecto | Modo Clássico | Modo Designer |
|---------|---------------|---------------|
| **Interface** | 3 painéis separados | Canvas interativo |
| **Edição** | Drag & drop de elementos | Clique direto nos elementos |
| **Público** | Usuários técnicos | Todos os usuários |
| **Preview** | Painel separado | Integrado |

**Recomendação**: Modo Designer para usuários iniciantes.

### Posso usar HTML personalizado nas mensagens?

**Não.** O sistema usa Adaptive Cards, que tem uma estrutura predefinida. Você pode:
- Adicionar textos formatados
- Inserir imagens
- Adicionar botões
- Incorporar vídeos

### Qual o tamanho máximo de imagem?

- **Tamanho do arquivo**: Máximo 5 MB
- **Dimensões recomendadas**: 800x600px ou superior
- **Formatos aceitos**: JPG, PNG, GIF

### Posso adicionar anexos (PDFs, Word, etc)?

**Não diretamente.** Alternativas:
- Hospede o arquivo em SharePoint ou OneDrive
- Adicione um botão com link para download
- Use o próprio Teams para compartilhar arquivos

### Como salvo um rascunho?

**Automático**: O sistema salva automaticamente a cada alteração.

**Manual**: Clique em "Finalizar > Salvar Rascunho"

### Posso duplicar uma mensagem existente?

**Sim!**
1. Acesse a lista de mensagens
2. Clique nos três pontos (...) na mensagem
3. Selecione "Duplicar"
4. Edite a cópia

---

## 📅 Agendamento

### Qual o tempo mínimo de antecedência para agendar?

**5 minutos.** Você não pode agendar uma mensagem para menos de 5 minutos no futuro.

### Posso agendar para o mesmo dia?

**Sim**, desde que respeite os 5 minutos de antecedência.

Exemplo:
- Hora atual: 10:00
- ✅ Pode agendar: 10:05 ou depois
- ❌ Não pode agendar: 10:04 ou antes

### O que acontece se eu agendar para um horário passado por engano?

O sistema **bloqueia** automaticamente. Você verá uma mensagem de erro:
> ❌ Agendamento deve ter no mínimo 5 minutos de antecedência

### Posso agendar mensagens recorrentes?

**Sim!** Opções disponíveis:
- **Única**: Envia apenas uma vez
- **Diária**: Repete todos os dias
- **Semanal**: Repete a cada 7 dias
- **Mensal**: Repete a cada 30 dias

### Como editar uma mensagem agendada?

1. Acesse "Mensagens" no menu
2. Filtre por "Agendadas"
3. Clique na mensagem
4. Edite os campos
5. Clique em "Salvar"

**Atenção**: Você pode editar até o momento do envio.

### Posso cancelar uma mensagem agendada?

**Sim!**
1. Acesse a mensagem agendada
2. Clique em "Cancelar Agendamento"
3. Confirme

### O sistema avisa se há conflito de horários?

Não. Você pode agendar múltiplas mensagens para o mesmo horário.

---

## 👥 Destinatários

### Como sei quais grupos existem?

Ao selecionar destinatários, o sistema exibe:
- Lista de todos os grupos disponíveis
- Número de membros em cada grupo

### Posso enviar para usuários específicos (não grupos)?

Atualmente, **não**. O envio é apenas para:
- Grupos predefinidos
- Todos os usuários (se habilitado)

**Solução temporária**: Crie um grupo específico no Teams/Azure AD.

### O que significa "Enviar para Todos"?

Envia a mensagem para **todos os usuários da organização**.

**⚠️ Atenção**: Use apenas para comunicados críticos ou gerais.

### Por que não vejo a opção "Todos os Usuários"?

Essa opção pode estar desabilitada nas configurações:
1. Acesse "Configurações > Configurações Gerais"
2. Verifique se "Permitir envio para todos os usuários" está ativo

Se não está disponível, contate o administrador.

### Posso enviar para múltiplos grupos ao mesmo tempo?

**Sim!** Selecione vários grupos na lista de destinatários.

### Como sei quantas pessoas vão receber a mensagem?

O sistema exibe a contagem total ao lado de cada grupo selecionado.

---

## 📊 Métricas

### Quais métricas estão disponíveis?

- **Comunicados Gerados**: Total criado
- **Recebidos**: Entregas confirmadas
- **Visualizados**: Mensagens abertas

Por mensagem:
- Total de destinatários
- Taxa de entrega
- Taxa de abertura
- Cliques em botões (se aplicável)

### Quando as métricas são atualizadas?

- **Tempo real**: Envios e entregas
- **Atualização**: A cada 5 minutos para aberturas

### Por que a taxa de visualização é baixa?

Possíveis razões:
1. **Horário de envio**: Enviado fora do expediente
2. **Público**: Grupo não engajado
3. **Conteúdo**: Título não chamou atenção
4. **Frequência**: Muitos comunicados recentes (fadiga)

**Dica**: Analise métricas históricas para identificar melhores horários.

### Como sei quem abriu minha mensagem?

Atualmente, o sistema **não exibe** usuários individuais, apenas métricas agregadas:
- Total de aberturas
- Percentual de visualização

### Métricas de mensagens antigas estão disponíveis?

**Sim**, as métricas são mantidas indefinidamente no histórico.

---

## 🔧 Problemas Técnicos

### A mensagem não está sendo enviada. O que fazer?

**Verifique:**
1. ✅ Conexão com internet estável
2. ✅ Destinatários selecionados
3. ✅ Conteúdo preenchido
4. ✅ Nenhum erro de validação

Se o problema persistir:
- Salve como rascunho
- Recarregue a página
- Tente novamente

### O editor travou/não responde. Como resolver?

**Soluções:**
1. **Aguarde 30 segundos** - Pode ser processamento
2. **Atualize a página** (F5)
3. **Limpe o cache do navegador**:
   - Edge: Ctrl+Shift+Delete
   - Chrome: Ctrl+Shift+Delete
4. **Reinicie o Teams**

### As imagens não aparecem na mensagem. Por quê?

Possíveis causas:
1. **URL inválida** - Verifique o link
2. **Imagem muito grande** - Máximo 5 MB
3. **Formato não suportado** - Use JPG, PNG ou GIF
4. **Firewall bloqueando** - Contate TI

### O preview não está mostrando corretamente. É normal?

O preview é uma **aproximação**. Pequenas diferenças são normais devido a:
- Diferentes versões do Teams
- Configurações do usuário
- Tema claro/escuro

**Dica**: Teste enviando para você mesmo antes.

### Recebi erro "Token expirado". O que significa?

Sua sessão expirou. **Solução:**
1. Feche o F1 Comunica
2. Feche o Teams
3. Abra o Teams novamente
4. Abra o F1 Comunica

### O sistema está lento. Como melhorar?

**Otimizações:**
1. **Feche abas não utilizadas** no navegador
2. **Limpe o cache** periodicamente
3. **Atualize o Teams** para última versão
4. **Verifique conexão de internet**

### Perdi meu rascunho. Posso recuperar?

Se o rascunho foi salvo, **sim**:
1. Acesse "Mensagens"
2. Filtre por "Rascunhos"
3. Localize sua mensagem

Se não foi salvo: **não é possível recuperar**.

**Dica**: O sistema salva automaticamente a cada alteração.

---

## 🆘 Outras Dúvidas

### Onde encontro mais ajuda?

- 📖 **Manual Completo**: [Manual do Usuário](./manual-usuario.md)
- 🔧 **Guia Técnico**: [Documentação Técnica](../technical/README.md)
- 🐛 **Problemas**: [Troubleshooting](./troubleshooting.md)
- 📧 **Suporte**: suporte-f1comunica@functionone.com.br

### Como sugiro uma nova funcionalidade?

1. Entre em contato com o time de desenvolvimento
2. Descreva a funcionalidade desejada
3. Explique o caso de uso
4. Aguarde avaliação

### O sistema será atualizado?

**Sim!** Acompanhe o roadmap: [Próximas Features](../roadmap/proximas-features.md)

---

## 📞 Contato

- 📧 **Email**: suporte-f1comunica@functionone.com.br
- 💬 **Teams**: Canal #f1-comunica-suporte
- 📚 **Documentação**: [/docs](../index.md)

---

**Última Atualização:** Janeiro 2026  
**Versão:** 1.0
