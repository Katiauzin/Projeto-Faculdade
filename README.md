# Projeto-Faculdade

2. PROJETO:

Os proprietários de uma faculdade precisam de um sistema que viabilize o armazenamento de informações sobre seus alunos, cursos, matérias e professores para que seja possível realizar controles básicos como montar turmas e realizar o armazenamento de notas dos alunos.

Análise das Necessidades:

1. Quais são as principais necessidades dos clientes?
	•	Armazenar informações sobre:
	•	Alunos
	•	Professores
	•	Cursos
	•	Disciplinas
	•	Montar turmas.
	•	Registrar e gerenciar notas dos alunos.

a. Quais informações precisam ser armazenadas?
	•	Alunos: ID, nome, data de nascimento, endereço, contato.
	•	Professores: ID, nome, especialidade, contato.
	•	Cursos: ID, nome, descrição.
	•	Disciplinas: ID, nome, carga horária, curso associado.
	•	Turmas: ID, disciplina, professor, semestre.
	•	Notas: Aluno, disciplina, nota obtida.

b. Quais os dados precisam ser guardados?
	•	Dados pessoais e acadêmicos de alunos e professores.
	•	Detalhes de cursos e disciplinas.
	•	Informações sobre turmas e matrículas.
	•	Registros de notas dos alunos.

c. O que será feito com os dados posteriormente?
	•	Gestão Acadêmica:
	•	Montagem de turmas.
	•	Atribuição de professores a disciplinas.
	•	Matrícula de alunos em turmas.
	•	Avaliação:
	•	Registro e consulta de notas.
	•	Relatórios e Consultas:
	•	Emissão de boletins.
	•	Análises estatísticas.

2. Quais tabelas precisam ser criadas para que todas as informações sejam armazenadas?
	1.	Alunos
	2.	Professores
	3.	Cursos
	4.	Disciplinas
	5.	Turmas
	6.	Matrículas
	7.	Notas

3. Quais atributos cada tabela deve ter?
	•	Tabela Alunos:
	•	id_aluno (INT, PK)
	•	nome (VARCHAR)
	•	data_nascimento (DATE)
	•	email (VARCHAR)
	•	telefone (VARCHAR)
	•	endereco (VARCHAR)
	•	Tabela Professores:
	•	id_professor (INT, PK)
	•	nome (VARCHAR)
	•	especialidade (VARCHAR)
	•	email (VARCHAR)
	•	telefone (VARCHAR)
	•	Tabela Cursos:
	•	id_curso (INT, PK)
	•	nome (VARCHAR)
	•	descricao (TEXT)
	•	Tabela Disciplinas:
	•	id_disciplina (INT, PK)
	•	nome (VARCHAR)
	•	carga_horaria (INT)
	•	id_curso (INT, FK)
	•	Tabela Turmas:
	•	id_turma (INT, PK)
	•	id_disciplina (INT, FK)
	•	id_professor (INT, FK)
	•	semestre (VARCHAR)
	•	Tabela Matrículas:
	•	id_matricula (INT, PK)
	•	id_aluno (INT, FK)
	•	id_turma (INT, FK)
	•	Tabela Notas:
	•	id_nota (INT, PK)
	•	id_matricula (INT, FK)
	•	nota (DECIMAL)

4. Qual o tipo de dados de cada atributo definido?

(Já especificado acima nos atributos de cada tabela.)

5. Quais são os relacionamentos a serem criados entre as tabelas?
	•	Cursos e Disciplinas: Um curso possui várias disciplinas (1:N).
	•	Disciplinas e Turmas: Uma disciplina pode ter várias turmas (1:N).
	•	Professores e Turmas: Um professor pode lecionar em várias turmas (1:N).
	•	Turmas e Matrículas: Uma turma pode ter vários alunos matriculados (1:N).
	•	Alunos e Matrículas: Um aluno pode estar matriculado em várias turmas (1:N).
	•	Matrículas e Notas: Uma matrícula pode ter várias notas associadas (1:N).

Modelo Conceitual:
	•	Entidades: Aluno, Professor, Curso, Disciplina, Turma, Matrícula, Nota.
	•	Relacionamentos:
	•	Aluno matricula-se em Turma.
	•	Professor leciona Turma.
	•	Turma oferece Disciplina.
	•	Disciplina pertence a Curso.
	•	Matrícula registra Aluno em Turma.
	•	Nota associa-se à Matrícula.

Modelo Lógico:
	•	Normalização das tabelas.
	•	Definição de chaves primárias (PK) e estrangeiras (FK).

Modelo Físico (código SQL):

CREATE TABLE Cursos (
    id_curso INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT
);

CREATE TABLE Disciplinas (
    id_disciplina INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    carga_horaria INT NOT NULL,
    id_curso INT,
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);

CREATE TABLE Professores (
    id_professor INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    especialidade VARCHAR(100),
    email VARCHAR(100),
    telefone VARCHAR(15)
);

CREATE TABLE Turmas (
    id_turma INT PRIMARY KEY,
    semestre VARCHAR(6) NOT NULL,
    id_disciplina INT,
    id_professor INT,
    FOREIGN KEY (id_disciplina) REFERENCES Disciplinas(id_disciplina),
    FOREIGN KEY (id_professor) REFERENCES Professores(id_professor)
);

CREATE TABLE Alunos (
    id_aluno INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE,
    email VARCHAR(100),
    telefone VARCHAR(15),
    endereco VARCHAR(200)
);

CREATE TABLE Matriculas (
    id_matricula INT PRIMARY KEY,
    id_aluno INT,
    id_turma INT,
    FOREIGN KEY (id_aluno) REFERENCES Alunos(id_aluno),
    FOREIGN KEY (id_turma) REFERENCES Turmas(id_turma)
);

CREATE TABLE Notas (
    id_nota INT PRIMARY KEY,
    nota DECIMAL(5,2),
    id_matricula INT,
    FOREIGN KEY (id_matricula) REFERENCES Matriculas(id_matricula)
);

Link do GITHUB contendo o código SQL:

GitHub Repository

Vídeo Explicativo:

Link para o vídeo explicativo no YouTube

5. AUTOAVALIAÇÃO

Se eu fosse a pessoa que usaria este sistema, a base de dados estaria adequada para meu uso?

Resposta:

Sim, a base de dados foi projetada para atender às necessidades principais identificadas pelos proprietários da faculdade. Ela permite armazenar e gerenciar eficientemente informações sobre alunos, professores, cursos, disciplinas, turmas e notas. Os relacionamentos entre as tabelas facilitam a montagem de turmas e o registro de notas, atendendo aos controles básicos requisitados.
