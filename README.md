## 📚 Guia de Estudos e Consulta: Controle de Versão (VCS) e Git/GitHub

---

### 0. ⌨️ O Editor Interno do Git (Vim)

| Ação | Teclas / Comando | Modo do Editor |
| :--- | :--- | :--- |
| Entrar em Modo de Edição | **`i`** (insert) ou **`a`** (append) | Modo de Inserção |
| Sair do Modo de Edição | **`ESC`** | Modo de Comando |
| Salvar e Sair | **`:wq`** | Modo de Comando |
| Sair Sem Salvar | **`:q!`** | Modo de Comando |
| Salvar (apenas) | **`:w`** | Modo de Comando |

---
---

### 1. 💻 Conceitos Fundamentais

| Conceito | Descrição |
| :--- | :--- |
| **Versionamento de Código** | Controle das versões de um arquivo ou projeto ao longo do tempo. |
| **Branching (Ramificação)** | Criação de linhas de desenvolvimento paralelas no Git. |
| **Merging (Fusão)** | Ação de unir as alterações de uma *branch* em outra. |
| **Git** | Sistema de Controle de Versão **Distribuído** (DVCS). |
| **GitHub** | Plataforma de hospedagem de código para controle de versão que utiliza o Git. |

#### Sistemas de Controle de Versão (VCS)

| Tipo | Característica Principal | Exemplos |
| :--- | :--- | :--- |
| **Centralizado** | Apenas 1 servidor no controle de versão. | CVS, Subversion |
| **Distribuído** | Cada 'banco de versão' é duplicado localmente. | Git, Mercurial |

---

### 2. 🛠️ Comandos Essenciais do Git (Local e Remoto)

#### 2.1. Manipulação do Repositório Local

| Comando | Descrição |
| :--- | :--- |
| `$ mkdir <nome>` | Cria nova pasta. |
| `$ git init` | Inicializa repositório Git. |
| `$ touch <nome-arquivo>` | Cria arquivo vazio. |
| `$ git status` | Mostra o estado. |
| `$ git add <arquivo>` ou `$ git add .` | Adiciona à Staging Area. |
| `$ git commit -m "mensagem"` | Salva as alterações (commit). |
| `$ git log` | Exibe histórico de commits. |
| `$ cat config` | Exibe `.git/config`. |
| `$ git reflog` | Exibe histórico de alterações (HEAD). |

---

#### 2.2. Fluxo Completo: Criar Remoto e Sincronizar

| Ação / Comando | Descrição |
| :--- | :--- |
| `$ git remote add origin <URL Github>` | Conecta local ao remoto. |
| `$ git branch -M main` | Renomeia branch principal para `main`. |
| `$ git push -u origin main` | Envia commits do local para o remoto. |
| `$ git clone <URL>` | Cria cópia local de um repositório existente. |
| `$ git pull` | Baixa e mescla (fetch e merge). |
| `$ git fetch origin` | Baixa atualizações (sem mesclar). |
| `$ git push` | Envia novos commits para o remoto. |

---

### 3. 🔑 Autenticação no GitHub

#### 3.1. Autenticação via Chave SSH (Recomendado)

| Comando Git Bash | Observações |
| :--- | :--- |
| `$ ls -a ~/.ssh` | Lista chaves existentes. |
| `$ ssh-keygen -t ed25519 -C "email github"` | Gera par de chaves. |
| `$ cat id_ed25519.pub` | Exibe chave pública para o GitHub. |
| `$ eval "$(ssh-agent -s)" | Inicia `ssh-agent`. |
| `$ ssh-add ~/.ssh/id-ed25519` | Adiciona chave privada ao agente. |

---

### 4. 📝 Ciclo de Commit (Salvando Alterações)

| Passo | Comando | Estado do Arquivo |
| :--- | :--- | :--- |
| **1. Modificar** | (Edição no código) | Área de Trabalho (*Working Area*) |
| **2. Preparar** | `$ git add .` | Área de Preparação (*Staging Area*) |
| **3. Salvar** | `$ git commit -m 'mensagem'` | Repositório Local |
| **4. Enviar** | `$ git push` | Repositório Remoto |

---

### 5. Desfazendo Alterações e Limpeza

| Objetivo | Comando |
| :--- | :--- |
| **Descartar Alterações Locais** | `$ git restore <arquivo>` |
| **Remover da Staging Area** | `$ git restore --staged <file>` |
| **Alterar Última Mensagem** | `$ git commit --amend -m "nova msg"` |
| **Arquivar Modificações** | `$ git stash` |

#### Git Reset (Desfazer Commits)

| Tipo de Reset | Comando |
| :--- | :--- |
| **Soft** | `$ git reset --soft <hash>` |
| **Mixed (Padrão)** | `$ git reset --mixed <hash>` |
| **Hard** | `$ git reset --hard <hash>` |

---

### 6. 🌳 Trabalhando com Branches

| Objetivo | Comando |
| :--- | :--- |
| **Listar Branches** | `$ git branch -v` |
| **Criar e Mudar** | `$ git checkout -b nome-de-nova-branch` |
| **Mesclar Branches** | `$ git merge nome-de-nova-branch` |
| **Excluir Branch** | `$ git branch -d nome-de-branch` |

---

### 7. 📘 Guia Rápido — Correções e .gitignore

#### 7.1. ⚠️ Correção do Erro: `src refspec main does not match any`

| Passo | Comando |
| :--- | :--- |
| **1. Adicionar** | `$ git add .` |
| **2. Commit** | `$ git commit -m "first commit"` |
| **3. Renomear** | `$ git branch -M main` |
| **4. Push** | `$ git push -u origin main` |

#### 7.2. 📄 Como criar um `.gitignore`

| Ação | Comando |
| :--- | :--- |
| **Criar o Arquivo** | `$ touch .gitignore` |

**Conteúdo para `.gitignore` (arquivo genérico):**
```gitignore
# IntelliJ IDEA
.idea/
*.iml
*.iws
*.ipr

# VSCode
.vscode/

# NetBeans
nbproject/private/
build/
nbbuild/
dist/
nbdist/
.nb-gradle/

# Eclipse
.project
.classpath
.settings/
bin/
tmp/

# Java / Build
*.class
out/
target/
build/
classes/
generated/
*.jar
*.war
*.ear

# Logs
*.log

# OS
.DS_Store
Thumbs.db
*~

# Outros
*.tmp
*.swp
*.bak
venv/
env/
