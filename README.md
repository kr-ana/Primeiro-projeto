# Primeiro-projeto
Agendamentos de Consultas Médicas Online

PROBLEMA: Pacientes enfrentam dificuldades para marcar consultas médicas, muitas vezes tendo que ligar para clínicas, esperar atendimento ou enfrentar enormes filas.

SOLUÇÃO: Desenvolver um sistema web que permita aos pacientes agendarem consultas com médicos de forma prática, visualizando horários disponíveis, especialidades e recebendo confirmações automáticas por e-mail ou SMS.

Seleção da plataforma: 

Plataforma web
• Acessível a qualquer paciente com internet.
• Clínicas podem administrar o sistema de qualquer lugar.
• Compatível com computadores e smartphones via navegador.

Definição das tecnologias: 
Camada	Tecnologia
Frontend 	                        React.js (interface responsiva)
Backend	                        Node.js + Express
Banco de Dados	                        PostgreSQL
ORM	                        Sequelize (para modelagem e acesso)
Hospedagem	                        Vercel (frontend) / Render (backend e banco)
Gerenciador de versão	                         Git + GitHub

Criação de diagramas com as inicias UML e MER:

Diagrama de Casos de Uso: Cadastro de pacientes, médicos e especialidades
[Diagrama_Casos_Uso_Consultas_Medicas (1).docx](https://github.com/user-attachments/files/20743159/Diagrama_Casos_Uso_Consultas_Medicas.1.docx)

Diagrama de sequência: Agendamento de consultas; confirmação/ cancelamento

[Diagrama_Sequencia_Agendamento.docx](https://github.com/user-attachments/files/20743161/Diagrama_Sequencia_Agendamento.docx)

Modelo Entidade-Relacionamento (MER): visualização de agenda 

[MER_Consultas_Medicas.docx](https://github.com/user-attachments/files/20743162/MER_Consultas_Medicas.docx)

Elaboração do cronograma inicial:

[Cronograma_Projeto_Consultas_Online.xlsx](https://github.com/user-attachments/files/20743164/Cronograma_Projeto_Consultas_Online.xlsx)

Sistema de Agendamentos de Consultas Médicas Online

Nesta etapa do projeto, iniciamos o desenvolvimento prático do sistema de agendamentos médicos. Serão apresentados: A estrutura inicial do banco de dados, com scripts de criação e inserção de dados; os primeiros wireframes das telas, definindo a interface visual do sistema e a versão inicial das APIs e backend, com funcionalidades básicas para receber, processar, salvar e retornar informações ao usuário.
Esses elementos formam a base para as próximas fases de integração e testes.

1.	Versão inicial do banco de dados:

1.1 Script DDL - Criação das Tabelas
   sql
-- Crtação das tabelas principais
CREATE TABLE pacientes (
id SERIAL PRIMARY KEY,
none VARCHAR (100) NOT NULL,
email VARCHAR (100) UNIQUE NOT NULL,
telefone VARCHAR(15),
data_nascimento DATE,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
):
CREATE TABLE medicos (
;
id SERIAL PRIMARY KEY,
none VARCHAR (100) NOT NULL
email VARCHAR (100) UNIQUE NOT NULL,
especialidade VARCHAR(100) NOT NULL,
telefone VARCHAR(15),
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
CREATE TABLE consultas (
id SERIAL PRIMARY KEY,
id_paciente INT NOT NULL,
id_medico INT NOT NULL,
data_hora TIMESTAMP NOT NULL,
status VARCHAR(20) DEFAULT Agendada, -- Pode ser Agendada, Cancelada, Concluida
observacoes TEXT,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
FOREIGN KEY (id_paciente) REFERENCES pacientes(id),
FOREIGN KEY (id_medico) REFERENCES medicos (id)
);

1.2. Script DML - Inserção de Dados Iniciais
  sql
-- Inserção de médicos
INSERT INTO medicos (nome, email, especialidade, telefone)
VALUES
("Dra. Beatriz Ramos', 'beatriz.ramos@clinica.com', 'Cardiologista', '(11)98888-1001'),
('Dr. Eduardo Martins', 'eduardo.martins@clinica.com', 'Dermatologista', .(11)98888-1002');
-- Inserção de pacientes
INSERT INTO pacientes (nome, email, telefone, data_nascimento)
VALUES
('Lucas Ferreira', 'lucas.ferreira@gmail.com', '(11)98765-4321', '199992-03-15'),
('Aline Castro', 'aline.castro@gmail.com', '(11)97654-3210, '1988-07-08');

Parâmetros para Conexão ao Banco (Sequelize)
No Node.js com Sequelize, arquivo .env e outro config/database.js como exemplo:
.env
    ini
DB_HOST=your-db-host.com
DB_PORT=5432
DB_USER=postgres
DB_PASS=yourpassword
DB_NAME=Consultas_online

config/database.js
 js
require('dotenv').config();
module.exports = }
development: {
username: process.env.DB_USER,
password: process.env.DB_PASS,
database: process.env.DB_NAME,
host: process.env.DB_HOST,
port: process.env.DB_PORT,
dialect: 'postgres',
}3
}

2.	Versão inicial de telas
   
   2.1 Tela de Login
  	A tela de login exibe o logo do sistema na parte superior e logo abaixo os tipos de usuários (Paciente/ Médico/ Administrador), campos de e-mail e password (e-mail e senha), botão log in (entrar), e Forgot password? (Esqueceu a senha?) e campo para cadastro;
 
   ![image](https://github.com/user-attachments/assets/e53417de-7a89-451c-b002-84e918645644)

2.2 Tela de Cadastro
  	A tela de cadastro exibe o logo do sistema na parte superior e logo abaixo os tipos de usuários (Paciente/ Médico), campos: Nome completo; Data de Nascimento; CPF, E-mail, Senha, Confirmação de senha e para médicos especialidade e o número do CRM e botão para cadastro.
  
   Paciente	![image](https://github.com/user-attachments/assets/df3373f3-742c-4e33-9c35-0793b1878341)
   
   Medico ![image](https://github.com/user-attachments/assets/889e9424-2725-4568-a198-f24d34019ebd)

2.3 Tela Inicial do Paciente (Dashboard)
  	A tela do paciente exibe o logo, saudação, próximas consultas, botão para agendar nova consulta e histórico de atendimentos.
  
   ![image](https://github.com/user-attachments/assets/dd132264-213e-4401-94d2-8b67c1b89155)

2.4 Tela de Agendamento (Dashboard)
  	A tela de agendamento exibe o logo, campo para escolher a especialidade do médico, selecionar médico e logo abaixo o calendário com horários disponíveis e botão para confirmar o agendamento e após a confirmação uma mensagem é enviada por e-mail/SMS.

   ![image](https://github.com/user-attachments/assets/05f25f30-ac23-4d67-ac2e-108fd7ff4cc0)

2.5 Tela de Médico (Dashboard Médico)
  	A tela exibe nome do médico a especialidade, lista de consultas marcadas, opção para aceitar/rejeitar consulta, ver perfil de paciente e atualizar disponibilidade	

  ![image](https://github.com/user-attachments/assets/4d7592a3-a0cd-4e6a-aaae-5c5272ccbc90)

2.6 Tela de Administrador (Dashboard Administrador)
  	A tela exibe um painel de controle com cabeçalho contendo logo, saudação, notificações e botão de sair. Um menu lateral permite acesso rápido ao dashboard, gerenciamento de usuários (médicos e pacientes), consultas, relatórios e configurações. O corpo principal mostra um resumo com indicadores (pacientes, médicos, consultas, status) e uma tabela de próximas consultas. Inclui botões para cadastrar médicos e usuários e exportar relatórios.

   ![image](https://github.com/user-attachments/assets/900e84a5-f70a-47b4-9df4-20f2f5b3c53b)

4.   API e Backend
   Objetivo:
Permitir interação dinâmica entre usuários e o sistema. A API precisa:

3.1	 Receber instruções do usuário
     POST /consultas (agendar), GET /medicos (listar médicos)
    javascript
// POST /consultas
app.post('/consultas', async (req, res) => }
const { pacienteId, medicoId, dataHora } = req.body;
const consultaExistente = await Consulta.findOne({ where: { medicoId, dataHora } });
if (consultaExistente) return res.status(409).json({ mensagem: 'Horário indisponível.
const novaConsulta = await Consulta.create({ pacienteId, medicoId, dataHora, status:
res.status(201).json(novaConsulta);
});
'confirmа});

3.2	 Manipular e validar dados
   Validar horário disponível, confirmar paciente e médico existentes
   Payload Recebido (JSON do Frontend):
    json
{
}
"pacienteId": 1,
"medicoId": 5,
"especialidade": "Cardiologia",
"data": "2025-07-01",
"hora": "14:00"

   Validação dos Dados Recebidos
   js
// Exemplo usando express-validator
const { body, validationResult } = require('express-validator');
router.post('/agendar',[
body('pacienteId').isInt(),
body('medicoId').isInt(),
body('especialidade').isString(),
body('data').isIS08601(),
body('hora').matches(/^([0-1]\d[2[0-3]):([0-5]\d)$/)
], async (req, res) => {
const errors = validationResult(req);
if (!errors.isEmpty()) {
}
});
return res.status(400).json({ erros: errors.array() });
// Prossiga com o agendamento...

Verificação de Disponibilidade
Verificar se o médico está disponível na data e hora solicitadas:
js
const consultaExistente = await Consulta.findOne({
where: {
medicoId: req.body.medicoId,
data: req.body.data,
hora: req.body.hora
}
});
if (consultaExistente) {
return res.status(409).json({ erro: "Horário já agendado para esse médico." });
}

Gravação da Consulta no Banco de Dados
 js
const novaConsulta = await Consulta.create({
pacienteId: req.body.pacienteId,
medicoId: req.body.medicoId,
especialidade: req.body.especialidade,
data: req.body.data,
});
hora: req.body.hora
res.status(201).json({ mensagem: "Consulta agendada com sucesso!", consulta: novaConsulta });

Persistir ou consultar no banco
Modelo Sequelize (Consulta.js)
 js
// models/Consulta.js
module.exports = (sequelize, DataTypes) => {
const Consulta = sequelize.define("Consulta", {
pacienteId: {
}
type: DataTypes.INTEGER,
allowNull: false
medicoId: {
},
type: DataTypes.INTEGER,
allowNull: false
especialidade: {
},
type: DataTypes.STRING,
allowNull: false
data: {
},
type: DataTypes.DATEONLY,
allowNull: false
hora: {
type: DataTypes.TIME,
allowNull: false
};
}
});
return Consulta;

Persistir Dados: Salvar uma nova consulta
Rota POST para salvar no banco
 js
// routes/consultas.js
const express = require('express');
const router = express.Router();
const { Consulta } = require('../models');
// POST /consuLltas
router.post('/', async (req, res) => {
try {
const { pacienteId, medicoId, especialidade, data, hora } = req.body;
const novaConsulta = await Consulta.create({
pacienteId,
medicoId,
especialidade,
data,
});
});
hora
res.status(201).json({ mensagem: "Consulta salva com sucesso!", consulta: novaconsulta });
} catch (error) {
res.status(500).json({ erro: "Erro ao salvar consulta.", detalhes: error.message });
}
module.exports = router;

Buscar consultas de um paciente
Rota GET para consultar
 js
// GET /consultas/paciente/:id
router.get('/paciente/:id', async (req, res) =>
try {
const consultas = await Consulta.findAll({
});
where: { pacienteid: req.params.id {
res.status(200).json(consultas);
} catch (error) {
{
res.status(500).json({ erro: "Erro ao buscar consultas.", detalhes: error.message });
}
});

Integração com o Sequelize
Conexão com o banco (Exemplo com PostgreSQL)
 js
// config/database.js
const { Sequelize } = require('sequelize');
const sequelize = new Sequelize('nome_do_banco', 'usuario', 'senha', {
});
host: 'localhost',
dialect: 'postgres',
module.exports = sequelize;

Inicializar os modelos

 // models/index.js
const Sequelize = require('sequelize');
const sequelize = require('../config/database');
const Consulta = require('./Consulta') (sequelize, Sequelize.DataTypes);
sequelize.sync(); // cria as tabelas se não existirem
module.exports = { Consulta };

Resumo: Tratamento do Payload

 Etapa;      Descrião
Validação:   Garante que os dados recebidos têm o formato esperado
Verificação de disponibilidade:  Evita agendamento em horários já ocupados
Criação da consulta:  Registra a consulta no banco de dados
Confirmação ao paciente: Opcional, mas importante para experiência do usuário

3.3 Retornar informações para o usuário
Confirmação por E-mail ou SMS
•	Nodemailer para e-mail.
•	Twilio ou SMSDev para SMS

const nodemailer = require('nodemailer');
const transporter = nodemailer.createTransport({
service: 'gmail',
auth: {
user: 'suaClinica@gmail.com',
pass: 'senha
}
});
await transporter.sendMail({
});
from: 'suaClinica@gmail.com',
to: 'paciente@email.com',
subject: 'Confirmação de Consulta',
text: `Sua consulta foi agendada para ${req.body.data} às ${req.body.hora}.`

Resultado Final
•	Persistência de consultas médicas em PostgreSQL.
•	Consulta de agendamentos com base no paciente.
•	Conexão ORM segura e padronizada com Sequelize.
•	Total integração com sua stack web (React frontend + API REST backend).

4	Retornar informações para usuário
JSON de sucesso, erro, ou os dados solicitados
Payload de entrada:
json
}
}
"pacienteId": 1,
"medicoId": 2,
"especialidade": "Dermatologia",
"data": "2025-06-25",
"hora": "10:30"

Backend: Rota POST /consultas com retorno informativo
js
// routes/consultas.js
const express = require('express');
const router = express. Router();
const { Consulta } = require('../models');
// Rota para criar nova consulta
router.post('/', async (req, res) => {
try {
const { pacienteId, medicoId, especialidade, data, hora } = req.body;
// Validação básica
if (!pacienteId || !medicoId || !especialidade || !data || !hora) {
}
return res.status(400).json({ mensagem: "Todos os campos são obrigatórios." });
// Criação da consulta
const novaConsulta = await Consulta.create({
});
pacienteId,
medicoId,
especialidade,
data,
hora
// Retorno para o usuário (confirmação)
res.status(201).json({
});
mensagem: "Consulta agendada com sucesso!",
consulta: novaConsulta
} catch (erro) {
res.status (500).json({ mensagem: "Erro ao agendar consulta.", detalhes: erro.message });
}
});
module.exports = router;

Retorno para o usuário (JSON de resposta):
json
}
"mensagem": "Consulta agendada com sucesso!"
"consulta": {
"id": 15,
"pacienteId": 1,
"medicoId": 2,
"especialidade": "Dermatologia",
"data": "2025-06-25",
"hora": "10:30:00",
"createdAt": "2025-06-17T18:45:00.000Z",
"updatedAt": "2025-06-17718:45:00.000Z"
}

Retorno em uma rota GET
js
// GET /consultas/paciente/:id
router.get('/paciente/:id', async (req, res) => {
try {
const consultas = await Consulta.findAll({
where: { pacienteId: req.params.id }
});
if (consultas.length === 0) {
}
return res.status(404).json({ mensagem: "Nenhuma consulta encontrada para este paciente." };res.status (200).json({
});
mensagem: "Consultas encontradas com sucesso!",
consultas
} catch (error) {
res.status (500).json({ mensagem: "Erro ao buscar consultas.", detalhes: error.message });
}
});

Benefícios para o usuário
•	Recebe mensagens claras de sucesso ou erro.
•	Confirmação com os detalhes da consulta agendada.
•	Listagem fácil das consultas anteriores ou futuras.















