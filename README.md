## 📚 Guia de Estudos e Consulta: Controle de Versão (VCS) e Git/GitHub

Este documento é um resumo organizado das minhas anotações sobre **Sistemas de Controle de Versão (VCS)**, com foco em **Git** e **GitHub**, e comandos essenciais e fluxos de trabalho.

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

#### 2.2. Fluxo de Conexão Remota

| Ação | Comando | Descrição |
| :--- | :--- | :--- |
| **Clonar Repositório** | `$ git clone <URL>` | Clona um repositório Git existente para uma nova pasta local. |
| **Clonar e Renomear** | `$ git clone <URL> "nome novo"` | Clona o repositório e nomeia a pasta local de destino. |
| **Adicionar Remoto** | `$ git remote add origin <URL Github>` | Conecta o repositório local a um remoto, geralmente chamado **`origin`**. |
| **Listar Remotos** | `$ git remote` | Mostra o nome do repositório remoto (ex: `origin`). |
| **Baixar e Mesclar** | `$ git pull` | "Puxa" as alterações do repositório remoto para o local (**`fetch`** e **`merge`**). |
| **Baixar (Apenas Fetch)** | `$ git fetch origin` | Verifica se há atualizações no remoto sem mesclá-las no branch atual. |
| **Enviar Alterações** | `$ git push -u origin main` | "Empurra" os *commits* do repositório local para o remoto (na branch `main`). |
| **Mesclar** | `$ git merge origin/main` | Mescla alterações baixadas do remoto (`origin/main`) para o branch local atual. |

---

### 3. 🛡️ Autenticação no GitHub

O acesso ao GitHub para operações como `git clone` ou `git push` requer autenticação.

#### 3.1. Autenticação via Chave SSH (Recomendado)

O protocolo **SSH** permite a conexão e autenticação no GitHub sem a necessidade de fornecer credenciais repetidamente.

| Ação | Comando Git Bash | Observações |
| :--- | :--- | :--- |
| **Verificar Chaves** | `$ ls -a ~/.ssh` | Lista os arquivos existentes no diretório `.ssh`. |
| **Gerar Nova Chave** | `$ ssh-keygen -t ed25519 -C "email github"` | Cria um par de chaves (**privada** e **pública**). |
| **Exibir Chave Pública** | `$ cat id_ed25519.pub` | Copie o conteúdo para colar no GitHub (**Settings** $\rightarrow$ **Access** $\rightarrow$ **SSH...**). |
| **Iniciar `ssh-agent`** | `$ eval "$(ssh-agent -s)"` | Inicia o agente para gerenciar as chaves. |
| **Adicionar Chave Privada** | `$ ssh-add ~/.ssh/id-ed25519` | Adiciona a chave privada ao agente SSH. |

#### 3.2. Personal Access Token (PAT)

Token gerado no GitHub para autenticação em vez da senha. É solicitado no primeiro acesso.

* **Para salvar o token temporariamente:** `$ git config --global credential.helper cache`
* **Para salvar o token permanentemente:** `$ git config --global credential.helper store`
* **Verificar armazenamento:** `$ git config --global --show-origin credential.helper`

---

### 4. 📝 Desfazendo Alterações e Limpeza

| Objetivo | Comando | Observação |
| :--- | :--- | :--- |
| **Descartar Alterações Locais** | `$ git restore <arquivo>` | Descarta **TODAS** as alterações não commitadas no arquivo, retornando ao último *commit*. |
| **Remover da Staging Area** | `$ git restore --staged <file>` | Remove o arquivo da *Staging Area* de volta para a Área de Trabalho (*Working Area*). |
| **Alterar Última Mensagem** | `$ git commit --amend -m "nova msg"` | Altera a mensagem do *commit* mais recente. |
| **Remover Versionamento** | `$ rm -rf .git` | Deve ser usado para apagar o repositório Git localmente. |
| **Arquivar Modificações** | `$ git stash` | Salva temporariamente as modificações não commitadas, limpando a área de trabalho. |
| **Ignorar Arquivos** | Criar arquivo `.gitignore` | Arquivos/pastas listados aqui não serão rastreados pelo Git. |
| **Pastas Vazias** | N/A | Git **NÃO** rastreia pastas/diretórios vazios. |

#### Git Reset (Desfazer Commits)

Utiliza o *hash* (identificador exclusivo) do *commit* para retornar a um estado anterior.

| Tipo de Reset | Comando | Comportamento |
| :--- | :--- | :--- |
| **Soft** | `$ git reset --soft <hash>` | Move *commits* posteriores para a **Área de Preparação** (*Staging Area*). |
| **Mixed (Padrão)** | `$ git reset --mixed <hash>` | Move *commits* posteriores para a **Área de Trabalho** (*Working Area*) como arquivos modificados (ou **untracked**). |
| **Hard** | `$ git reset --hard <hash>` | Ignora e **descarta COMPLETAMENTE** os arquivos e *commits* posteriores ao *hash*. |

---

### 5. 🌳 Trabalhando com Branches

| Objetivo | Comando | Descrição |
| :--- | :--- | :--- |
| **Listar Branches** | `$ git branch -v` | Lista as *branches* e mostra o último *commit* de cada uma. |
| **Mudar Branch** | `$ git branch -M main` | Muda o nome da *branch* atual (ex: de `master` para `main`). |
| **Criar e Mudar** | `$ git checkout -b nome-de-nova-branch` | Cria uma nova *branch* e move o **HEAD** (ponteiro) para ela. |
| **Mesclar Branches** | `$ git merge nome-de-nova-branch` | Mescla as alterações da *branch* indicada na *branch* atual. |
| **Excluir Branch** | `$ git branch -d nome-de-branch-que-quero-excluir` | Exclui a *branch* local (somente se as alterações já foram mescladas). |
| **Clonar Branch Específica** | `$ git clone <URL> --branch <nome> --single-branch` | Clona o repositório baixando apenas a *branch* especificada. |
| **Mostrar Diferenças** | `$ git diff` | Mostra as diferenças entre o *working directory* e o *staging area*, ou entre branches. |

> 📌 **Nota sobre Branches**: Uma nova *branch* se inicia apontando para o mesmo *commit* da *branch* onde você estava quando ela foi criada.

---

### 6. 🔄 Atualização de Repositório e Conflitos

A distinção entre `fetch` e `pull` e a gestão de conflitos são fundamentais ao trabalhar em equipe.

| Conceito/Ação | Comando | Descrição |
| :--- | :--- | :--- |
| **`git fetch` vs. `git pull`** | `$ git fetch` | **Baixa** as alterações do repositório remoto, mas **NÃO** as mescla no seu *branch* local. Apenas atualiza as referências remotas (ex: `origin/main`). |
| | `$ git pull` | É um atalho que executa **`git fetch`** seguido por **`git merge`** (ou **`git rebase`**). Baixa e mescla as alterações automaticamente. |
| **Conflito (*Conflict*)** | N/A | Ocorre quando as mesmas linhas de código são modificadas de formas diferentes em *branches* que estão sendo mesclados (`merge` ou `pull`). |
| **Resolução de Conflitos** | Editar o arquivo, `$ git add .`, `$ git commit -m "Resolvendo conflitos"` | Remover as marcações `<<<<<<<`, `=======`, `>>>>>>>` no arquivo e salvar o código desejado. |

### 7. 🏷️ Tags e Histórico

Tags são usadas para marcar pontos específicos no histórico do seu projeto, como *releases* (versões estáveis).

| Objetivo | Comando | Descrição |
| :--- | :--- | :--- |
| **Criar Tag Leve** | `$ git tag v1.0.0` | Cria uma tag simples, como um ponteiro. Usada para marcar um *commit* específico. |
| **Criar Tag Anotada** | `$ git tag -a v1.0.0 -m "Versão de lançamento 1.0.0"` | Cria uma tag que armazena informações extras (autor, data, mensagem). Mais segura. |
| **Listar Tags** | `$ git tag` | Lista todas as tags criadas no repositório. |
| **Enviar Tags para o Remoto** | `$ git push origin --tags` | As tags **não** são enviadas automaticamente pelo `git push` normal. |
