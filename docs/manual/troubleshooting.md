# 🔧 Troubleshooting - Resolução de Problemas

> **Guia de resolução de problemas comuns**  
> Público-alvo: Usuários e Administradores

---

## 📑 Índice

1. [Problemas de Acesso](#problemas-de-acesso)
2. [Problemas no Editor](#problemas-no-editor)
3. [Problemas de Envio](#problemas-de-envio)
4. [Problemas de Agendamento](#problemas-de-agendamento)
5. [Problemas de Performance](#problemas-de-performance)
6. [Problemas de Visualização](#problemas-de-visualização)
7. [Problemas de Autenticação](#problemas-de-autenticação)
8. [Logs e Diagnóstico](#logs-e-diagnóstico)

---

## 🚪 Problemas de Acesso

### App não aparece no Teams

**Sintomas:**
- Não vejo o ícone do F1 Comunica no Teams
- App não está na lista de aplicativos

**Possíveis Causas:**
1. App não foi instalado para sua organização
2. Você não tem permissão de acesso
3. App foi desabilitado pelo administrador

**Soluções:**

```bash
✅ Verifique com o administrador do Teams
✅ Acesse "Apps" no Teams e busque por "F1 Comunica"
✅ Solicite instalação se não encontrar
```

### Tela branca ao abrir o app

**Sintomas:**
- App abre mas mostra tela branca
- Carregamento infinito

**Soluções:**

```bash
1. Aguarde 30 segundos (pode ser conexão lenta)
2. Recarregue a página (F5 ou Ctrl+R)
3. Limpe o cache do Teams:
   - Feche o Teams completamente
   - Delete: %appdata%\Microsoft\Teams\Cache (Windows)
   - Reabra o Teams
4. Atualize o Teams para a última versão
```

### Erro "Não autorizado" ao acessar

**Sintomas:**
- Mensagem de erro 401 ou "Não autorizado"
- App fecha imediatamente

**Soluções:**

```bash
1. Verifique sua conta Microsoft 365
2. Saia e entre novamente no Teams
3. Limpe cookies do navegador
4. Contate o administrador para verificar permissões
```

---

## ✏️ Problemas no Editor

### Editor trava ao adicionar elementos

**Sintomas:**
- Interface congela ao arrastar elementos
- Nenhuma resposta ao clicar

**Soluções:**

```bash
1. Aguarde 10-15 segundos (processamento)
2. Use Ctrl+Z para desfazer última ação
3. Salve o rascunho e recarregue a página
4. Limpe o cache do navegador:
   - Edge: Ctrl+Shift+Delete
   - Chrome: Ctrl+Shift+Delete
   - Selecione "Imagens e arquivos em cache"
```

### Elementos não aparecem no preview

**Sintomas:**
- Adiciono elemento mas não aparece no preview
- Preview está vazio

**Soluções:**

```bash
1. Aguarde sincronização (1-2 segundos)
2. Clique em "Atualizar Preview"
3. Mude para outro elemento e volte
4. Salve e recarregue a página
```

### Imagens não são carregadas no editor

**Sintomas:**
- Imagem não aparece após upload
- Ícone de "quebrado" no lugar da imagem

**Causas e Soluções:**

| Causa | Solução |
|-------|---------|
| **Arquivo muito grande** | Reduza para < 5 MB |
| **Formato inválido** | Use JPG, PNG ou GIF |
| **URL inválida** | Verifique o link |
| **Firewall bloqueando** | Contate TI |
| **Conexão instável** | Tente novamente |

### Não consigo deletar um elemento

**Sintomas:**
- Clico em deletar mas elemento permanece
- Botão de deletar não funciona

**Soluções:**

```bash
1. Selecione o elemento e pressione Delete (teclado)
2. Clique com botão direito > Remover
3. Use Ctrl+Z para desfazer adição
4. Recarregue a página e tente novamente
```

---

## 📤 Problemas de Envio

### Mensagem não está sendo enviada

**Sintomas:**
- Clico em "Enviar" mas nada acontece
- Mensagem fica em "Enviando" indefinidamente

**Checklist de Validação:**

```bash
✅ Verificar conexão com internet
✅ Validar se destinatários estão selecionados
✅ Confirmar que há conteúdo na mensagem
✅ Verificar se não há erros de validação
✅ Aguardar 1-2 minutos (processamento no servidor)
```

**Soluções:**

```bash
1. Salve como rascunho
2. Recarregue a página
3. Abra o rascunho e tente enviar novamente
4. Verifique logs do console (F12)
5. Contate suporte se persistir
```

### Erro "Falha ao enviar mensagem"

**Sintomas:**
- Mensagem de erro após clicar em Enviar
- Toast de erro aparece

**Soluções:**

```bash
1. Verifique se você tem permissão para enviar
2. Confirme que os grupos selecionados são válidos
3. Reduza o tamanho de imagens se houver
4. Tente enviar para um grupo menor primeiro
5. Contate suporte com screenshot do erro
```

### Mensagem enviada mas não chegou aos destinatários

**Sintomas:**
- Status mostra "Enviada"
- Usuários não receberam

**Investigação:**

```bash
1. Verifique métricas de entrega na mensagem
2. Confirme se destinatários estão corretos
3. Aguarde 5-10 minutos (pode haver delay)
4. Verifique se usuários têm Teams instalado
5. Contate administrador se problema persistir
```

---

## 📅 Problemas de Agendamento

### Não consigo selecionar data no calendário

**Sintomas:**
- Calendário não abre
- Datas não são clicáveis

**Soluções:**

```bash
1. Clique diretamente no campo de data
2. Recarregue a página
3. Tente usar navegador diferente
4. Limpe cache do navegador
```

### Erro "Agendamento deve ter no mínimo 5 minutos"

**Sintomas:**
- Mensagem de erro ao tentar agendar
- Data/hora não são aceitas

**Causa:**
Você está tentando agendar para um horário muito próximo ou no passado.

**Solução:**

```bash
1. Verifique hora atual
2. Adicione pelo menos 5 minutos
3. Confirme se data está correta
4. Se necessário, ajuste fuso horário
```

### Hora não carrega ao editar mensagem agendada

**Sintomas:**
- Campo de hora aparece vazio ao editar
- Data carrega mas hora não

**Solução:**

```bash
1. Aguarde 2-3 segundos (sincronização)
2. Recarregue a página
3. Se persistir, anote a hora atual
4. Delete e crie novo agendamento
```

### Mensagem agendada não foi enviada

**Sintomas:**
- Horário passou mas mensagem não foi enviada
- Status continua "Agendada"

**Investigação:**

```bash
1. Verifique se mensagem foi cancelada
2. Confirme horário de agendamento
3. Aguarde 5 minutos após horário agendado
4. Verifique logs do sistema
5. Contate suporte se não enviou após 10 min
```

---

## ⚡ Problemas de Performance

### Sistema está muito lento

**Sintomas:**
- Demora para carregar páginas
- Cliques demoram para responder
- Interface travando

**Diagnóstico:**

```bash
# Verificar uso de memória
1. Abra Task Manager (Ctrl+Shift+Esc)
2. Verifique uso de memória do Teams
3. Se > 2GB, reinicie o Teams

# Verificar conexão
1. Teste velocidade: speedtest.net
2. Mínimo recomendado: 5 Mbps download
```

**Soluções:**

```bash
✅ Feche abas não utilizadas no navegador
✅ Reinicie o Teams
✅ Limpe cache (Ctrl+Shift+Delete)
✅ Desabilite extensões do navegador
✅ Atualize Teams para última versão
✅ Verifique se há outros apps pesados rodando
```

### Timeout ao carregar mensagens

**Sintomas:**
- Erro de timeout
- Lista de mensagens não carrega

**Soluções:**

```bash
1. Verifique conexão de internet
2. Aguarde 30 segundos e recarregue
3. Limpe cache
4. Tente acessar mais tarde
5. Contate suporte se persistir
```

---

## 👁️ Problemas de Visualização

### Layout quebrado / Elementos desalinhados

**Sintomas:**
- Elementos sobrepostos
- Texto cortado
- Scrollbar não funciona

**Soluções:**

```bash
1. Ajuste zoom do navegador para 100% (Ctrl+0)
2. Maximize a janela do Teams
3. Recarregue a página (F5)
4. Teste em navegador diferente
5. Verifique resolução de tela (mínimo 1280x720)
```

### Imagens não aparecem nas mensagens

**Sintomas:**
- Placeholder no lugar da imagem
- Ícone de "quebrado"

**Soluções:**

```bash
1. Verifique se URL da imagem está acessível
2. Teste a URL em navegador separado
3. Confirme formato (JPG, PNG, GIF)
4. Verifique se não há bloqueio de firewall
5. Re-upload da imagem
```

### Cores estão diferentes do esperado

**Sintomas:**
- Cores não correspondem ao preview
- Tema escuro/claro afeta cores

**Explicação:**
O Teams pode aplicar temas que alteram cores. Isso é comportamento normal.

**Solução:**
- Use cores neutras (cinza, branco, preto)
- Teste em tema claro e escuro
- Evite cores muito claras ou muito escuras

---

## 🔐 Problemas de Autenticação

### Erro "Token expirado"

**Sintomas:**
- Mensagem "Token expirado" ou "Unauthorized"
- App pede para fazer login novamente

**Solução:**

```bash
1. Feche o F1 Comunica
2. Feche o Teams completamente
3. Reabra o Teams
4. Reabra o F1 Comunica
5. Se persistir, limpe cache e tente novamente
```

### Erro "Permissão negada"

**Sintomas:**
- "Permission denied" ou "Access denied"
- Não consegue realizar ações

**Soluções:**

```bash
1. Verifique se você tem as permissões necessárias
2. Entre em contato com administrador
3. Confirme que sua conta está ativa
4. Saia e entre novamente no Teams
```

---

## 📋 Logs e Diagnóstico

### Como acessar logs do navegador

```bash
1. Abra DevTools (F12)
2. Vá na aba "Console"
3. Procure por mensagens em vermelho (erros)
4. Copie o erro e envie ao suporte
```

### Informações úteis para suporte

Ao reportar um problema, inclua:

```
✅ Versão do Teams
✅ Navegador e versão
✅ Sistema operacional
✅ Resolução de tela
✅ Passos para reproduzir
✅ Screenshot do erro
✅ Logs do console (se possível)
```

### Como fazer screenshot

**Windows:**
- Tela inteira: PrtScn
- Área selecionada: Windows + Shift + S

**Mac:**
- Tela inteira: Cmd + Shift + 3
- Área selecionada: Cmd + Shift + 4

---

## 📞 Quando Contactar o Suporte

Contate o suporte se:

- ❌ Problema persiste após tentar todas as soluções
- ❌ Erro crítico impede uso do sistema
- ❌ Dados foram perdidos
- ❌ Problema afeta múltiplos usuários
- ❌ Suspeita de bug no sistema

**Canais de Suporte:**
- 📧 Email: suporte-f1comunica@functionone.com.br
- 💬 Teams: #f1-comunica-suporte
- 📚 Documentação: [/docs](../index.md)

---

**Última Atualização:** Janeiro 2026  
**Versão:** 1.0
