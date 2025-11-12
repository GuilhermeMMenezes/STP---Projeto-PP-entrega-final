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

<h2>A API utiliza, no mínimo, as tabelas:</h2>
´´
create table usuario(
id int auto_increment unique,
nomeUsuario varchar(255) not null,
email varchar(255) unique not null primary key,
senha varchar(255) not null
);
´´
´´
create table tarefas(
 id INT AUTO_INCREMENT PRIMARY KEY,
nomeTarefa varchar(255) not null,
descricao varchar(255) not null,
 created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
´´

<h2>Rotas API</h2<

Post/cadastrar:
´´
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
´´

Post/login:
´´
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
´´

post/tarefas:
´´
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
´´
get/tarefas:
´´
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
´´

get/perfil/:email:
´´
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
´´

delete/usuario:email:
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
