# 🚀 COMPILAR APK PELO GITHUB (Automático!)

## O que é GitHub Actions?

Um bot no GitHub que **compila seu app automaticamente** quando você faz upload! Você **não precisa instalar nada** no PC.

---

## 📋 PASSO 1️⃣ - CRIAR CONTA NO GITHUB

1. Vá em: https://github.com
2. Clique em **"Sign up"** (canto superior direito)
3. Email, senha, username (nome de usuário)
4. **Verifique seu email** (GitHub vai mandar um link)
5. ✅ Conta criada!

---

## 📁 PASSO 2️⃣ - CRIAR UM REPOSITÓRIO NOVO

1. Clique no **"+"** (canto superior direito)
2. **"New repository"**
3. Preencha:
   - **Repository name:** `SMS-Forwarder` (ou qualquer nome)
   - **Description:** `SMS Forwarder App` (opcional)
   - **Public** (deixe marcado)
   - ✅ **"Create repository"**

**Pronto!** Repositório criado vazio.

---

## 📤 PASSO 3️⃣ - UPLOAD DO PROJETO

### Opção A: Direto no GitHub (Mais Fácil)

1. Na página do repositório, clique em **"Add file"**
2. **"Upload files"**
3. **Arraste a pasta `SMSForwarder-v2` aqui** (ou clique pra selecionar)
4. Clique em **"Commit changes"**

**Pronto!** Todos os arquivos foram para o GitHub!

### Opção B: Usando Git (Se você sabe Git)

```bash
cd SMSForwarder-v2
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/seu-usuario/SMS-Forwarder.git
git push -u origin main
```

---

## ⚙️ PASSO 4️⃣ - CONFIGURAR GITHUB ACTIONS

Agora vamos fazer um bot compilar o APK automaticamente!

### A. Criar o arquivo de configuração

1. No repositório, clique em **"Add file"** → **"Create new file"**
2. No campo do nome do arquivo, escreva:
   ```
   .github/workflows/android-build.yml
   ```
3. Cole este código (abaixo):

```yaml
name: Build APK

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Set up JDK 11
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        distribution: 'adopt'
    
    - name: Build APK
      run: |
        chmod +x gradlew
        ./gradlew assembleRelease
    
    - name: Upload APK
      uses: actions/upload-artifact@v3
      with:
        name: APK
        path: app/build/outputs/apk/release/app-release.apk
```

4. Clique em **"Commit new file"** (verde, canto direito)

---

## 🔨 PASSO 5️⃣ - DISPARAR A COMPILAÇÃO

Agora a compilação vai começar automaticamente!

1. Vá em **"Actions"** (menu superior do repositório)
2. Você verá um workflow rodando:
   ```
   Build APK (em progresso...)
   ████████░░░░░░░░░░░░░░░░░░ 50%
   ```

3. **Aguarde 10-15 minutos** (primeira compilação demora mais)

4. Quando terminar, você verá:
   ```
   ✅ Build APK (sucesso!)
   ```

---

## 📥 PASSO 6️⃣ - BAIXAR O APK

Quando o build terminar com ✅:

1. Clique no workflow **"Build APK"** (verde)
2. Role para baixo até **"Artifacts"**
3. Clique em **"APK"**
4. Vai baixar um `.zip` com seu `app-release.apk`!

---

## 🎯 RESUMO VISUAL

```
1. GitHub (https://github.com)
   ↓
2. Sign up (criar conta)
   ↓
3. New repository (SMS-Forwarder)
   ↓
4. Upload files (drag & drop SMSForwarder-v2)
   ↓
5. Add file → Create new → .github/workflows/android-build.yml
   ↓
6. Paste o código (yml acima)
   ↓
7. Commit new file
   ↓
8. Actions (acompanhar compilação)
   ↓
9. Aguarde 10-15 minutos
   ↓
10. Download do APK! ✅
```

---

## ⚡ APÓS TER O APK

1. **Descompacte o .zip** baixado
2. **Pegue o arquivo:** `app-release.apk`
3. **Envie para seu Android:**
   - Email
   - Telegram
   - Google Drive
   - WhatsApp
   - Qualquer forma!

4. **No Android:**
   - Abra o `.apk`
   - Clique em "Instalar"
   - Conceda permissões
   - ✅ Pronto!

5. **Configure:**
   - Configurações → Apps → SMS Forwarder
   - Permissões → SMS ✅
   - App padrão de SMS → SMS Forwarder

6. **Teste:**
   - Envie um SMS para você
   - Abra: `http://seu-ip:3000`
   - ✅ SMS aparece em tempo real!

---

## 🆘 DÚVIDAS

### P: Onde eu vejo o APK?
**R:** Actions → Seu build (aquele em verde) → Artifacts → APK

### P: Quanto tempo demora?
**R:** Primeira vez 10-15 min, próximas 5-10 min

### P: Posso fazer novamente?
**R:** Sim! Toda vez que você fizer `push` (atualizar arquivos), compila novamente automaticamente

### P: Deu erro na compilação?
**R:** Clique no build vermelho → "Build APK" → veja o erro
- Se for Android SDK, GitHub instala automaticamente (deixa rodar)
- Se for código, algo pode estar faltando

### P: O APK funciona igual?
**R:** Sim! 100% igual ao compilado no PC

### P: Preciso de mais de um APK?
**R:** Pode compilar quantas vezes quiser! GitHub Actions é grátis

---

## 🎁 BONUS: Sempre Ter o Último APK

Para facilitar, você pode configurar para o APK ficar sempre disponível:

1. Vá em **"Releases"** (no repositório)
2. **"Create a new release"**
3. **"Choose a tag"** → Digite: `v1.0.0`
4. **"Title"** → `Version 1.0.0`
5. **Arraste o APK** para upload
6. **"Publish release"**

Pronto! Sempre disponível para baixar! 📥

---

## ✅ CHECKLIST

- [ ] Conta GitHub criada
- [ ] Repositório criado
- [ ] Arquivos upados
- [ ] Workflow criado (.github/workflows/android-build.yml)
- [ ] Compilação iniciada (Actions)
- [ ] Compilação concluída com ✅
- [ ] APK baixado
- [ ] APK enviado para Android
- [ ] App instalado
- [ ] Permissão de SMS dada
- [ ] 🎉 FUNCIONANDO!

---

## 🚀 ALTERNATIVA: GitHub Desktop (Mais Fácil)

Se achar confuso, pode usar **GitHub Desktop** (app visual):

1. Baixe: https://desktop.github.com
2. Faça login
3. Clique em **"Add"** → **"Clone repository"**
4. Selecione seu repositório
5. Clique em **"Create Branch"**
6. **Arraste a pasta do projeto** para o GitHub Desktop
7. **Commit** e **Publish**

Aí os Actions disparam automaticamente!

---

## 📞 PRECISA DE AJUDA?

- GitHub Help: https://docs.github.com
- GitHub Actions: https://docs.github.com/actions
- Android Gradle: https://developer.android.com/studio/build

---

**Pronto!** Seu APK vai ser compilado **automaticamente** no GitHub! 🎉

Sem instalar nada no PC, sem usar terminal!

**Sucesso!** 🚀📱✨
