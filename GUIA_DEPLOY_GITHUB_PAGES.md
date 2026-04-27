# 🚀 Guia de Deploy — KPI Inspeção no GitHub Pages + Google Drive

---

## PARTE 1 — GitHub Pages (o site)

### Passo 1 · Criar conta no GitHub
→ Acesse https://github.com/signup  
→ Escolha um username (ex: `andersonsouza`)  
→ Plano gratuito é suficiente

---

### Passo 2 · Criar o repositório
1. Clique em **New repository** (botão verde no canto superior direito)
2. Preencha:
   - **Repository name:** `kpi-inspecao` (ou qualquer nome sem espaços)
   - **Visibility:** ✅ Public
   - ❌ NÃO marque "Add a README file"
3. Clique **Create repository**

---

### Passo 3 · Fazer upload do HTML
1. Na página do repositório vazio, clique em **uploading an existing file**
2. Arraste o arquivo `KPI_CONTROLE_DE_INSPECOES_v1_6.html`
3. **IMPORTANTE:** Renomeie o arquivo para `index.html`  
   (clique no nome do arquivo e edite antes de confirmar)
4. Clique **Commit changes**

---

### Passo 4 · Ativar o GitHub Pages
1. No repositório, clique em **Settings** (aba superior)
2. No menu lateral esquerdo, clique em **Pages**
3. Em **Source**, selecione:
   - Branch: **main**
   - Pasta: **/ (root)**
4. Clique **Save**
5. Aguarde ~2 minutos

✅ Seu KPI estará disponível em:  
**`https://SEU_USUARIO.github.io/kpi-inspecao`**

---

## PARTE 2 — Google Cloud Console (o login)

### Passo 5 · Criar projeto no Google Cloud
1. Acesse https://console.cloud.google.com
2. Clique no seletor de projeto (topo) → **Novo Projeto**
3. Nome: `KPI Inspeção` → **Criar**

---

### Passo 6 · Ativar a Google Drive API
1. Menu lateral → **APIs e Serviços** → **Biblioteca**
2. Pesquise: `Google Drive API`
3. Clique nela → **Ativar**

---

### Passo 7 · Configurar tela de consentimento OAuth
1. Menu lateral → **APIs e Serviços** → **Tela de consentimento OAuth**
2. Tipo de usuário: **Externo** → **Criar**
3. Preencha:
   - Nome do app: `KPI Inspeção`
   - E-mail de suporte: seu e-mail
   - E-mail do desenvolvedor: seu e-mail
4. Clique **Salvar e continuar** (nas próximas telas também)
5. Na tela **Usuários de teste** → **Add users** → adicione seu e-mail Google
6. Clique **Salvar e continuar** → **Voltar ao painel**

---

### Passo 8 · Criar credencial OAuth 2.0
1. Menu lateral → **APIs e Serviços** → **Credenciais**
2. Clique **+ Criar credenciais** → **ID do cliente OAuth 2.0**
3. Tipo de aplicativo: **Aplicativo da Web**
4. Nome: `KPI GitHub Pages`
5. Em **Origens JavaScript autorizadas**, clique **+ Adicionar URI**:
   ```
   https://SEU_USUARIO.github.io
   ```
6. Em **URIs de redirecionamento autorizados**, clique **+ Adicionar URI**:
   ```
   https://SEU_USUARIO.github.io/kpi-inspecao
   ```
7. Clique **Criar**
8. Uma janela aparece com o **ID do cliente** — copie esse valor!
   Formato: `XXXXXXXXXX-xxxxxxxxxxxxxxxxxx.apps.googleusercontent.com`

---

## PARTE 3 — Configurar o CLIENT_ID no HTML

### Passo 9 · Colar o Client ID
1. Abra o `KPI_CONTROLE_DE_INSPECOES_v1_6.html` no VS Code
2. Use **Ctrl+F** e pesquise: `SEU_CLIENT_ID_AQUI`
3. Substitua por seu Client ID copiado no passo anterior:
   ```js
   // ANTES:
   const DRIVE_CLIENT_ID = 'SEU_CLIENT_ID_AQUI.apps.googleusercontent.com';

   // DEPOIS (exemplo):
   const DRIVE_CLIENT_ID = '123456789-abcdefghijk.apps.googleusercontent.com';
   ```
4. Salve o arquivo

---

### Passo 10 · Fazer upload da versão final no GitHub
1. Acesse seu repositório no GitHub
2. Clique no arquivo `index.html`
3. Clique no ícone de **lápis** (editar) → depois em **...** → **Upload file**  
   OU: arraste o HTML atualizado diretamente para a página do repositório
4. Confirme o commit

---

## PARTE 4 — Usar o KPI

### Passo 11 · Primeiro acesso
1. Abra `https://SEU_USUARIO.github.io/kpi-inspecao` no navegador
2. Clique no botão **☁ Conectar Drive** na barra de controles
3. Uma janela do Google abre → selecione sua conta → **Permitir**
4. O KPI carrega seus dados do Drive automaticamente

### A partir do segundo acesso:
- O token expira após 1 hora de inatividade — basta clicar **☁ Conectar Drive** novamente
- Os dados **nunca se perdem** — estão no arquivo `kpi_state.json` no seu Google Drive

---

## ❓ Dúvidas comuns

**O arquivo kpi_state.json fica onde?**  
Na raiz do seu Google Drive. Você pode ver em https://drive.google.com

**Posso fazer backup manual?**  
Sim! Baixe o `kpi_state.json` do Drive quando quiser. É só um arquivo de texto.

**E se eu atualizar o HTML no futuro?**  
Faça upload do novo `index.html` no GitHub. Os dados ficam no Drive, não no HTML.

**Quero limpar todos os dados e começar do zero?**  
Delete o `kpi_state.json` do Google Drive. Na próxima conexão um novo arquivo vazio é criado.

**O repositório precisa ser público?**  
Para GitHub Pages gratuito, sim. O HTML é visível, mas os **dados ficam no Drive privado** — ninguém acessa seus dados sem sua senha Google.

---

## 📋 Checklist final

- [ ] Repositório criado no GitHub
- [ ] `index.html` enviado e GitHub Pages ativo
- [ ] URL do Pages funcionando (`https://usuario.github.io/kpi-inspecao`)
- [ ] Projeto criado no Google Cloud Console
- [ ] Google Drive API ativada
- [ ] Tela de consentimento configurada + seu e-mail adicionado como usuário de teste
- [ ] Credencial OAuth criada com a URL do GitHub Pages
- [ ] `DRIVE_CLIENT_ID` atualizado no HTML
- [ ] HTML atualizado reenviado ao GitHub
- [ ] Testou o botão ☁ Conectar Drive com sucesso
