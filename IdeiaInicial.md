# **Projeto: Plataforma de Monitoria Universitária**

## **1. Objetivo do Sistema**
Criar uma plataforma que gerencie o **processo de monitoria** dentro da faculdade, facilitando:

- Divulgação de vagas de monitoria  
- Candidatura de alunos às vagas disponíveis  
- Gestão do processo seletivo (aprovação/reprovação)  

---

## **2. Principais Entidades**
Mapeamento das entidades que compõem o banco de dados do sistema.

### **2.1. Usuários**
| Campo | Tipo | Descrição |
|--------|------|-----------|
| id | PK | Identificador único |
| nome | String | Nome completo |
| email | String | Email institucional |
| senha | String (hash) | Senha criptografada |
| tipo | Enum | admin, aluno, monitor |
| curso | String | Curso do aluno |
| matricula | String | Matrícula do aluno |
| telefone | String | Contato |
| data_cadastro | Date | Data de registro |

---

### **2.2. Disciplinas**
| Campo | Tipo | Descrição |
|--------|------|-----------|
| id | PK | Identificador único |
| nome | String | Nome da disciplina |
| codigo | String | Código da disciplina |
| descricao | String | Breve descrição |
| professor_responsavel | String | Nome do professor responsável |

---

### **2.3. Vagas**
| Campo | Tipo | Descrição |
|--------|------|-----------|
| id | PK | Identificador único |
| disciplina_id | FK | Relaciona com a disciplina |
| descricao | String | Descrição da vaga |
| status | Enum | aberta, em análise, fechada |
| requisitos | Array | Lista de habilidades necessárias |
| data_abertura | Date | Data de abertura |
| data_fechamento | Date | Data de fechamento |
| monitor_id | FK | Relaciona com o aluno aprovado |

---

### **2.4. Candidaturas**
| Campo | Tipo | Descrição |
|--------|------|-----------|
| id | PK | Identificador único |
| vaga_id | FK | Relaciona com a vaga |
| aluno_id | FK | Relaciona com o aluno |
| status | Enum | pendente, aprovado, rejeitado |
| data_candidatura | Date | Data da candidatura |
| documentos | String | Link para documentos |

---

## **3. Principais Funcionalidades de Back-End**

### **3.1. Autenticação e Autorização**
- Login e registro de usuários  
- Middleware de autenticação por **JWT**  
- Controle de permissões baseado no tipo de usuário:
  - **Admin:** Gerenciar disciplinas, aprovar candidatos, abrir vagas  
  - **Monitor:** Editar agenda, responder dúvidas, ver lista de alunos interessados  
  - **Aluno:** Candidatar-se a vagas, visualizar disponibilidade  

---

### **3.2. Gestão de Vagas**
- Criar, editar, listar e excluir vagas  
- Garantir que **uma disciplina tenha apenas um monitor aprovado**  
- Controle de status das vagas (aberta, em análise, fechada)  

---

### **3.3. Processo Seletivo**
- Registro da candidatura de alunos  
- Upload de documentos comprobatórios  
- Alteração de status da candidatura  
- Histórico de candidaturas  


### **3.4. Dashboard Administrativo**
- Painel com estatísticas:
  - Vagas abertas/fechadas  
  - Número de candidatos por disciplina  
  - Desempenho dos monitores  

---

## **4. Fluxos Principais**

### **4.1. Fluxo de Candidatura**
1. Aluno faz login  
2. Visualiza vagas abertas  
3. Envia candidatura com habilidades e documentos  
4. Admin/professor avalia a candidatura  
5. Se aprovado → aluno se torna monitor da disciplina  



## **5. Tecnologias Recomendadas**

### **5.1. Back-End**
- **Node.js (Express)** ou **Django (Python)**  
- **Autenticação:** JWT  
- **ORM:** Prisma (No
