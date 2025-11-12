## 🖥️ Frontend – STP Technology

A parte web do STP Technology foi construída em HTML, CSS e JavaScript, organizada em várias páginas temáticas. Cada tela tem um papel dentro da jornada do aluno (do cadastro até o estudo guiado e quizzes).

---

### 🧾 cadastro.html — Tela de cadastro de usuário

Página onde o usuário cria sua conta na plataforma.

- **Função principal:** cadastro de novos usuários.
- **Campos:**
  - Nome completo (`nomeUsuario`)
  - E-mail (`email`)
  - Senha (`senha`)
- **Ações:**
  - Botão **"Cadastrar"** dispara a lógica de envio dos dados para a API (`/cadastrar`) através do arquivo `../Backend/cadastro.js`.
  - Link **"Já tem conta? Fazer login"** leva para `login.html`.
- **Estilos:** `css/cadastro.css`
- **Integração:** `../Backend/cadastro.js` (responsável por fazer o `fetch` para o backend). :contentReference[oaicite:0]{index=0}

---

### 🔐 login.html — Tela de login

Página de autenticação do usuário.

- **Função principal:** realizar login com e-mail e senha.
- **Campos:**
  - E-mail (`email`)
  - Senha (`senha`)
- **Ações:**
  - Botão **"Entrar"** chama a lógica de login em `../Backend/login.js`, que envia os dados para a rota `/login`.
  - Link **"Ainda não possui conta? Cadastrar"** leva para `cadastro.html`.
- **Estilos:** `css/login.css`
- **Integração:** `../Backend/login.js` (faz o POST de login e redireciona pra tela principal ao sucesso). :contentReference[oaicite:1]{index=1}

---

### 🏠 index.html — Tela principal / Home do aluno

É a tela inicial que o usuário vê depois de logar.

- **Função principal:** servir como hub do aluno dentro da plataforma.
- **Elementos principais:**
  - **Header com logo** da STP Technology.
  - **Menu hamburger lateral** com links para:
    - Início (`index.html`)
    - Favoritos (placeholder)
    - Guia de estudo (`guia.html`)
    - Tarefas (`tarefas.html`)
    - Contato (placeholder)
    - Perfil (`perfil.html`)
  - **Seção Guia de estudos:** link para abrir `guia.html`.
  - **Cards das linguagens:**
    - JavaScript → `paginajavascript.html`
    - HTML & CSS → `paginahtml.html`
    - Python → `paginapython.html`
- **Estilos:** `css/style.css`
- **Integração:** `../Backend/index.js` (responsável pelo comportamento do menu e possíveis interações futuras). :contentReference[oaicite:2]{index=2}

---

### 📚 guia.html — Gerador de Guia de Estudos

Página onde o aluno responde algumas perguntas e o sistema gera um plano de estudos personalizado.

- **Função principal:** montar um guia de estudos baseado nas escolhas do aluno.
- **Formulário com 3 perguntas:**
  1. **Objetivo principal** (`objetivo`):
     - Focar em estilização/front
     - Começar do zero em Web
     - Lógica e interatividade (JS)
     - IA/automação com Python
  2. **Nível atual** (`nivel`):
     - Iniciante
     - Intermediário
     - Avançado
  3. **Preferência de estudo** (`preferencia`):
     - Mão na massa
     - Conceitos primeiro
     - Misturar os dois
- **Ações:**
  - Botão **"Gerar Guia"** monta o resumo e o plano na seção de resultado.
  - Botão **"Limpar"** reseta o formulário.
- **Área de resultado:**
  - Bloco **"Seu guia de estudos"** com um resumo e a lista de recomendações geradas dinamicamente.
- **Estilos:** `css/guia.css`
- **Integração:** `../Backend/guia.js` (processa as respostas e escreve o plano em `#plano`). :contentReference[oaicite:3]{index=3}

---

### 👤 perfil.html — Página de perfil do usuário

Tela onde o usuário visualiza e gerencia seus dados cadastrais.

- **Função principal:** exibir e permitir edição/remoção do perfil.
- **Campos exibidos:**
  - Nome (`#nome`)
  - E-mail (`#email`)
  - Ambos iniciam como `"Carregando..."` e são preenchidos via JavaScript.
- **Ações:**
  - **Editar Perfil:** libera os campos para edição e mostra o botão **"Salvar Alterações"**.
  - **Salvar Alterações:** envia as mudanças para o backend (rota de update de usuário).
  - **Excluir Conta:** chama a rota de deleção do usuário no backend.
- **Estilos:** `css/perfil.css`
- **Integração:** `../Backend/perfil.js` (carrega dados do perfil, habilita edição, faz update e delete). :contentReference[oaicite:4]{index=4}

---

### 🌐 paginahtml.html — Página de conteúdo: HTML & CSS

Seção com materiais recomendados para estudo de HTML e CSS.

- **Função principal:** agrupar indicações de:
  - **Cursos** (Gustavo Guanabara, Otavio Miranda, Matheus Battisti)
  - **Jogos** (Flexbox Froggy, CSS Battle, CSS Dinner)
  - **Atividades** (Codecademy, exercícios do Guanabara, CodeChef)
- **Estrutura:**
  - Blocos de `<details>` organizados em três categorias:
    - Cursos
    - Jogos
    - Atividades
  - Cada item contém descrição do recurso e botão **"Começar" / "Jogar" / "Acessar"** com link externo.
- **Extra:** botão no topo para **"Fazer o Quiz de HTML & CSS"**, levando para `quizHTML.html`.
- **Estilos:** `css/pagina das linguagens/paginahtml.css` :contentReference[oaicite:5]{index=5}

---

### 💛 paginajavascript.html — Página de conteúdo: JavaScript

Seção focada em recomendações de estudo de JavaScript.

- **Função principal:** listar recursos para aprender JS via cursos, jogos e atividades.
- **Categorias:**
  - **Cursos:** Guanabara, Academind, Matheus Battisti.
  - **Jogos:** CodeCombat, Mimo, CodeWars (descrição estilo gamificado).
  - **Atividades:** HackerRank, exercícios do Guanabara, Codecademy.
- **Estrutura:** semelhante à de HTML & CSS (vários `<details>` em categorias).
- **Estilos:** `css/pagina das linguagens/paginajavascript.css`
- **Navegação:** botão **"Voltar"** que leva para `index.html`. :contentReference[oaicite:6]{index=6}

---

### 🐍 paginapython.html — Página de conteúdo: Python

Página com trilhas e recursos para estudar Python.

- **Função principal:** fornecer:
  - **Cursos:** Guanabara, Otávio Miranda, Erik Frits.
  - **Jogos:** Mimo, CodeCombat, Codedex.
  - **Atividades:** HackerRank (Python), Beecrowd, LeetCode.
- **Estrutura:** mesma ideia das outras linguagens: categorias de Cursos, Jogos e Atividades com descrições e botões de acesso.
- **Estilos:** `css/pagina das linguagens/paginapython.css`
- **Navegação:** link **"Voltar"** retorna para `index.html`. :contentReference[oaicite:7]{index=7}

---

### 🧩 quizHTML.html — Quiz de HTML & CSS

Tela de quiz interativo para avaliar o conhecimento do aluno.

- **Função principal:** aplicar perguntas de múltipla escolha e exibir resultado.
- **Componentes:**
  - Card de quiz com:
    - Título **"Quiz de Programação"**
    - Barra de progresso (`#progressFill`, `#metaText`)
    - Área de pergunta (`#questionArea`)
  - Navegação:
    - Botão **"Anterior"**
    - Botão **"Próxima"**
    - Botão **"Finalizar"** (aparece ao final)
  - Card de resultado:
    - Texto de pontuação (`#scoreText`)
    - Feedback detalhado (`#feedback`)
- **Ações:**
  - **Refazer** o quiz.
  - Voltar ao guia (`index.html`).
- **Estilos:** `css/quiz/quizes.css`
- **Integração:** `../Backend/quizHtml.js` (monta as perguntas, controla navegação e cálculo da nota). :contentReference[oaicite:8]{index=8}

---

### 🧩 quizjavascript.html — Quiz de JavaScript

Tela de quiz específica para JavaScript, com a mesma estrutura do quiz de HTML & CSS.

- **Função principal:** aplicar um conjunto de questões de JavaScript.
- **Componentes:**
  - Mesmo layout de card, barra de progresso, área de perguntas e seção de resultado.
- **Ações:**
  - Navegação entre perguntas.
  - Finalização com cálculo de score.
  - Botão para refazer o quiz.
  - Link para voltar ao guia.
- **Estilos:** `css/quiz/quizes.css`
- **Integração:** `../Backend/quizJavaScript.js` (responsável pela lógica do quiz de JS). :contentReference[oaicite:9]{index=9}

---

---

### 🐍🧩 quizpython.html — Quiz de Python

Página de quiz específica para a linguagem Python, seguindo o mesmo design e estrutura dos outros quizzes da plataforma.

- **Função principal:** aplicar perguntas de múltipla escolha sobre Python e avaliar o conhecimento do aluno.
- **Componentes principais:**
  - Card com:
    - Título **"Quiz de Programação"**
    - Barra e meta de progresso (`#progressFill` e `#metaText`)
    - Área dinâmica das perguntas (`#questionArea`)
  - Navegação:
    - Botão **"Anterior"**
    - Botão **"Próxima"**
    - Botão **"Finalizar"** (visível na última pergunta)
  - Card de resultado:
    - Pontuação final (`#scoreText`)
    - Feedback detalhado (`#feedback`)
    - Botão **"Refazer"**
    - Botão para voltar ao Guia (`index.html`)
- **Estilos:** `css/quiz/quizes.css`
- **Integração:** O comportamento é controlado por `../Backend/quizPython.js` (carregamento das questões, progresso, resultado etc.).  
  :contentReference[oaicite:0]{index=0}
- **Navegação extra:** Botão **"Voltar"** leva de volta para `paginajavascript.html`.

---

### ✔️ tarefas.html — Gerenciador de Tarefas (To-Do List)

Página dedicada ao gerenciamento de tarefas do usuário, integrada diretamente ao backend do STP Technology.

- **Função principal:** permitir ao usuário cadastrar e visualizar suas tarefas.
- **Componentes principais:**
  - **Formulário de criação de tarefas**
    - Campo **Título** (`#nomeTarefa`)
    - Campo **Descrição** (`#descricao`)
    - Botão **"Cadastrar"** (`#tarefa`)
  - **Lista de tarefas**
    - Renderizada dentro de `<ul id="listaTarefas"></ul>`
    - Carregada dinamicamente via fetch na rota `/tarefas`
- **Fluxo de uso:**
  1. Usuário preenche título e descrição.
  2. Clica em **Cadastrar** → frontend chama `../Backend/tarefas.js`.
  3. A rota backend `/tarefas` cria o item no banco.
  4. A lista é atualizada automaticamente.
- **Estilos:** `css/tarefas.css`
- **Integração:** `../Backend/tarefas.js` (responsável por enviar tarefas ao backend e listar todas).  
  :contentReference[oaicite:1]{index=1}
- **Observação:** A página já está conectada diretamente com o servidor Node.js — tudo que é criado aparece também no banco de dados.

---

## 🔗 Fluxo geral do usuário

1. **Cadastro** em `cadastro.html`.
2. **Login** em `login.html`.
3. Ao logar, o usuário acessa a **Home** (`index.html`).
4. De lá, ele pode:
   - Gerar um **Guia de Estudos** em `guia.html`.
   - Acessar as trilhas de **HTML & CSS**, **JavaScript** e **Python**.
   - Fazer os **quizzes** correspondentes.
   - Ver e editar seu **perfil** em `perfil.html`.
5. Toda a parte de autenticação, edição de perfil e exclusão de conta se comunica com a **API Node.js + MySQL** descrita na seção de backend deste README.


# STP Technology – API (Node.js + Express + MySQL)

Este repositório contém a API backend do projeto **STP Technology**, desenvolvida em **Node.js** com **Express** e banco de dados **MySQL**.

A API é responsável por:

- Cadastro de usuários  
- Login/autenticação básica
- Edição de perfil
- Exclusão de perfil 
- Consulta de perfil  
- CRUD básico de tarefas (criar e listar)

---

## 🚀 Tecnologias utilizadas

- [Node.js](https://nodejs.org/)
- [Express](https://expressjs.com/)
- [MySQL](https://www.mysql.com/)
- [cors](https://www.npmjs.com/package/cors)

---

## 📁 Estrutura básica

```bash
./
├── server.js        # Servidor Express com as rotas da API
├── db-config.js     # Configuração de conexão com o MySQL
└── package.json
``
<h2>A API utiliza, no mínimo, as tabelas:</h2>
``
create table usuario(
id int auto_increment unique,
nomeUsuario varchar(255) not null,
email varchar(255) unique not null primary key,
senha varchar(255) not null
);
``
``
create table tarefas(
 id INT AUTO_INCREMENT PRIMARY KEY,
nomeTarefa varchar(255) not null,
descricao varchar(255) not null,
 created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
``

<h2>Rotas API</h2<

##Post/cadastrar:
``
app.post('/cadastrar', (req, res) => {
    const {nomeUsuario, email ,senha} = req.body

    const query = 'insert into usuario (nomeUsuario, email, senha) values (?,?,?)'

    connection.query(query, [nomeUsuario, email , senha], (err, results) => {
        if (err) {
            return res.status(500).json({ success: false, message: 'Erro ao cadastrar usuario' });
          }
          res.json({ success: true, message: 'usuario cadastrado com sucesso!'});
    })

})
``

##Post/login:
``
app.post('/login', (req, res) => {
  const { email, senha } = req.body;

  if (!email || !senha) {
    return res.status(400).json({ success: false, message: 'Campos obrigatórios.' });
  }

  const query = 'SELECT * FROM usuario WHERE email = ? AND senha = ?';
  connection.query(query, [email, senha], (err, rows) => {
    if (err) {
      console.error(err);
      return res.status(500).json({ success: false, message: 'Erro no servidor.' });
    }

    if (rows && rows.length > 0) {
      return res.json({ success: true, message: 'Login bem-sucedido!' });
    } else {
      return res.json({ success: false, message: 'Usuário ou senha incorretos!' });
    }
  });
});
``

##post/tarefas:
``
app.post('/tarefas', (req, res) => {
  const { nomeTarefa, descricao } = req.body;
  if (!nomeTarefa || !descricao) {
    return res.status(400).json({ success:false, message:'Campos obrigatórios' });
  }

  const sql = 'INSERT INTO tarefas (nomeTarefa, descricao) VALUES (?, ?)';
  connection.query(sql, [nomeTarefa, descricao], (err, result) => {
    if (err) {
      console.error('ERRO SQL INSERT:', err);
      return res.status(500).json({ success:false, message:'Erro ao cadastrar tarefa' });
    }
    res.json({ success:true, message:'OK', data:{ id: result.insertId, nomeTarefa, descricao } });
  });
});
``
##get/tarefas:
``
app.get('/tarefas', (req, res) => {
  const sql = 'SELECT id, nomeTarefa, descricao, created_at FROM tarefas ORDER BY id DESC';
  connection.query(sql, (err, rows) => {
    if (err) {
      console.error('ERRO SQL SELECT:', err);
      return res.status(500).json({ success:false, message:'Erro ao listar tarefas' });
    }
    res.json({ success:true, data: rows });
  });
});
``

##get/perfil/:email:
``
app.get('/perfil/:email', (req, res) => {
  const email = req.params.email;

  const sql = 'SELECT id, nomeUsuario, email FROM usuario WHERE email = ?';

  connection.query(sql, [email], (err, rows) => {
    if (err) {
      console.error('ERRO SQL SELECT:', err);
      return res.status(500).json({ success:false, message:'Erro ao buscar usuário' });
    }

    if (rows.length === 0) {
      return res.status(404).json({ success:false, message:'Usuário não encontrado' });
    }

    res.json({ success:true, data: rows[0] });
  });
});
``

##delete/usuario:email:
``
app.delete('/usuario/:email', (req, res) => {
  const email = req.params.email;

  const sql = 'DELETE FROM usuario WHERE email = ?';

  connection.query(sql, [email], (err, result) => {
    if (err) {
      console.error('Erro ao deletar usuário:', err);
      return res.status(500).json({ success: false, message: 'Erro ao deletar usuário' });
    }

    if (result.affectedRows === 0) {
      return res.status(404).json({ success: false, message: 'Usuário não encontrado' });
    }

    res.json({ success: true, message: 'Usuário deletado com sucesso' });
  });
});

``

put/usuario/:email:
``
app.put('/usuario/:email', (req, res) => {
  const emailAtual = req.params.email;     
  const { nomeUsuario, emailNovo } = req.body;

  if (!nomeUsuario || !emailNovo) {
    return res.status(400).json({ success:false, message:'Nome e e-mail são obrigatórios.' });
  }

  const sql = 'UPDATE usuario SET nomeUsuario = ?, email = ? WHERE email = ?';

  connection.query(sql, [nomeUsuario, emailNovo, emailAtual], (err, result) => {
    if (err) {
      console.error('Erro ao atualizar usuário:', err);
      if (err.code === 'ER_DUP_ENTRY') {
        return res.status(409).json({ success:false, message:'Este e-mail já está em uso.' });
      }
      return res.status(500).json({ success:false, message:'Erro ao atualizar usuário.' });
    }

    if (result.affectedRows === 0) {
      return res.status(404).json({ success:false, message:'Usuário não encontrado.' });
    }

    res.json({ success:true, message:'Usuário atualizado com sucesso.' });
  });
});
``
