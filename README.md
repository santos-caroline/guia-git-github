## 📚 Guia de Estudos e Consulta: Controle de Versão (VCS) e Git/GitHub

Este documento é um resumo organizado das minhas anotações sobre **Sistemas de Controle de Versão (VCS)**, com foco em **Git** e **GitHub**, seus comandos essenciais e fluxos de trabalho.

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

| Tipo | Característica Principal | Vantagens | Exemplos |
| :--- | :--- | :--- | :--- |
| **Centralizado** | Apenas 1 servidor no controle de versão. | Simples para iniciar. | CVS, Subversion |
| **Distribuído** | Cada 'banco de versão' é duplicado localmente. | ➡️ Possível **clonar o repositório completo**. ➡️ **Trabalhar sem conexão à rede**. ➡️ Redundância (backup local). | Git, Mercurial |

---

### 2. 🛠️ Comandos Essenciais do Git (Local e Remoto)

#### 2.1. Manipulação do Repositório Local

| Passo | Comando | Descrição |
| :--- | :--- | :--- |
| **Criação de Diretório** | `$ mkdir <nome>` | Cria uma nova pasta (diretório) para o projeto. |
| **Inicializar Git** | `$ git init` | Transforma o diretório atual em um repositório Git. Cria a pasta oculta **`.git`**. |
| **Criação de Arquivo** | `$ touch <nome-arquivo>` | Cria um arquivo vazio (ex: `README.md`). |
| **Status** | `$ git status` | Mostra o estado da árvore de trabalho e da *staging area* (arquivos rastreados, modificados, ou não rastreados). |
| **Adicionar (Staging)** | `$ git add <arquivo>` ou `$ git add .` | Adiciona o(s) arquivo(s) modificado(s) à **Área de Preparação** (*Staging Area*). |
| **Salvar (Commit)** | `$ git commit -m "mensagem"` | Grava as alterações da *Staging Area* no histórico do repositório local. |
| **Histórico** | `$ git log` | Exibe o histórico de *commits*. |
| **Configuração** | `$ cat config` | Exibe o conteúdo do arquivo de configuração (`.git/config`). |
| **Histórico de Comandos** | `$ git reflog` | Exibe o histórico de alterações (HEAD). |

> 📌 **Nota sobre `git status`**: **"untracked files"** são arquivos que o Git não rastreia, estão na área de trabalho e nunca foram commitados.

---

#### 2.2. Fluxo Completo: Criar Remoto e Sincronizar (Merge com Local)

| Passo | Ação / Comando | Descrição |
| :--- | :--- | :--- |
| **1. Criar Repositório Remoto** | (Ação feita no GitHub) | No GitHub, crie um "New repository". |
| **2. Adicionar Remoto** | `$ git remote add origin <URL Github>` | Conecta seu repositório local ao recém-criado remoto, nomeando-o como **`origin`**. |
| **3. Mudar Nome da Branch** | `$ git branch -M main` | Renomeia sua *branch* local principal para `main`. |
| **4. Primeira Sincronização** | `$ git push -u origin main` | Envia os *commits* do local (`main`) para o remoto (`origin`). O `-u` define `origin main` como *upstream*. |
| **5. Clonar Repositório** | `$ git clone <URL>` | Cria uma cópia local de um repositório Git existente. |
| **6. Baixar e Mesclar** | `$ git pull` | "Puxa" as alterações do repositório remoto para o local (**`fetch`** e **`merge`**). |
| **7. Baixar (Apenas Fetch)** | `$ git fetch origin` | Verifica se há atualizações no remoto sem mesclá-las no branch atual. |
| **8. Enviar Alterações** | `$ git push` | Envia os novos *commits* do repositório local para o remoto. |

---

### 3. 🔑 Autenticação no GitHub

O acesso ao GitHub para operações como `git clone` ou `git push` requer autenticação.

#### 3.1. Autenticação via Chave SSH (Recomendado)

| Ação | Comando Git Bash | Observações |
| :--- | :--- | :--- |
| **Verificar Chaves** | `$ ls -a ~/.ssh` | Lista os arquivos existentes no diretório `.ssh`. |
| **Gerar Nova Chave** | `$ ssh-keygen -t ed25519 -C "email github"` | Cria um par de chaves (**privada** e **pública**). |
| **Exibir Chave Pública** | `$ cat id_ed25519.pub` | Copie o conteúdo para colar no GitHub (**Settings** $\rightarrow$ **Access** $\rightarrow$ **SSH...**). |
| **Iniciar `ssh-agent`** | `$ eval "$(ssh-agent -s)" | Inicia o agente para gerenciar as chaves. |
| **Adicionar Chave Privada** | `$ ssh-add ~/.ssh/id-ed25519` | Adiciona a chave privada ao agente SSH. |

---

### 4. 📝 Ciclo de Commit (Salvando Alterações)

Este é o fluxo fundamental para registrar o progresso no Git.

| Passo | Comando | Estado do Arquivo | Descrição |
| :--- | :--- | :--- | :--- |
| **1. Modificar** | (Edição no código) | Área de Trabalho (*Working Area*) | Arquivos são alterados. |
| **2. Preparar** | `$ git add .` | Área de Preparação (*Staging Area*) | Move os arquivos do *Working Area* para o *Staging Area*. |
| **3. Salvar** | `$ git commit -m 'mensagem'` | Repositório Local | Cria um ponto permanente no histórico. |
| **4. Enviar** | `$ git push` | Repositório Remoto | Envia os novos *commits* para o servidor remoto. |

---

### 5. Desfazendo Alterações e Limpeza

| Objetivo | Comando | Observação |
| :--- | :--- | :--- |
| **Descartar Alterações Locais** | `$ git restore <arquivo>` | Descarta **TODAS** as alterações não commitadas. |
| **Remover da Staging Area** | `$ git restore --staged <file>` | Move o arquivo da *Staging Area* de volta para a Área de Trabalho. |
| **Alterar Última Mensagem** | `$ git commit --amend -m "nova msg"` | Altera a mensagem do *commit* mais recente. |
| **Arquivar Modificações** | `$ git stash` | Salva temporariamente as modificações não commitadas. |

#### Git Reset (Desfazer Commits)

Utiliza o *hash* do *commit* para retornar a um estado anterior.

| Tipo de Reset | Comando | Comportamento |
| :--- | :--- | :--- |
| **Soft** | `$ git reset --soft <hash>` | Move *commits* posteriores para a **Área de Preparação**. |
| **Mixed (Padrão)** | `$ git reset --mixed <hash>` | Move *commits* posteriores para a **Área de Trabalho**. |
| **Hard** | `$ git reset --hard <hash>` | Ignora e **descarta COMPLETAMENTE** os *commits* posteriores. |

---

### 6. 🌳 Trabalhando com Branches

| Objetivo | Comando | Descrição |
| :--- | :--- | :--- |
| **Listar Branches** | `$ git branch -v` | Lista as *branches* e mostra o último *commit*. |
| **Criar e Mudar** | `$ git checkout -b nome-de-nova-branch` | Cria uma nova *branch* e move o **HEAD** para ela. |
| **Mesclar Branches** | `$ git merge nome-de-nova-branch` | Mescla as alterações da *branch* indicada na *branch* atual. |
| **Excluir Branch** | `$ git branch -d nome-de-branch` | Exclui a *branch* local. |

---

### 7. 📘 Guia Rápido — Correções e .gitignore

#### 7.1. ⚠️ Correção do Erro: `src refspec main does not match any`

Esse erro significa que você tentou dar um `push` antes de criar o primeiro *commit* ou de nomear o *branch* principal como `main`.

| Passo | Comando | Objetivo |
| :--- | :--- | :--- |
| **1. Adicionar** | `$ git add .` | Prepara os arquivos para o *commit*. |
| **2. Commit** | `$ git commit -m "first commit"` | Cria o primeiro ponto no histórico. |
| **3. Renomear** | `$ git branch -M main` | Garante que o *branch* principal se chame `main`. |
| **4. Push** | `$ git push -u origin main` | Envia o novo histórico para o GitHub. |

#### 7.2. 📄 Como criar um `.gitignore`

O arquivo `.gitignore` instrui o Git a **ignorar** arquivos e pastas específicos, impedindo que sejam enviados para o GitHub (como arquivos de build, logs ou senhas).

| Ação | Comando | Exemplo de Uso |
| :--- | :--- | :--- |
| **Criar o Arquivo** | `$ touch .gitignore` | Cria o arquivo na raiz do seu projeto. |
| **Conteúdo Comum** | (Editar o arquivo) | Incluir nomes de diretórios (`/bin/`), extensões (`*.class`) ou arquivos sensíveis (`*.env`). |

**Exemplo de Conteúdo para `.gitignore` (arquivo genérico):**
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
````

-----

### 8\. ⚠️ Solução de Erro Comum: Históricos Não Relacionados

Esse erro (`updates were rejected because the remote contains work that you do not have locally`) acontece na primeira sincronização quando o GitHub tem arquivos que o seu projeto local não tem (ex: README ou LICENSE criados online).

| Situação | Comando | Descrição |
| :--- | :--- | :--- |
| **Integrar** o GitHub com o Local (Forma Segura) | `$ git pull origin main --allow-unrelated-histories` | Baixa o que está no GitHub e permite a fusão de históricos não relacionados. |
| **Sobrescrever** o GitHub com o Local (Forçar) | `$ git push origin main --force` | ⚠️ **ATENÇÃO:** Apaga o histórico e o conteúdo que estava no GitHub. Use com extrema cautela\! |

```
```
