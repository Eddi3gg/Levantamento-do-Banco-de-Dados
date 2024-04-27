# Levantamento-do-Banco-de-Dados
Banco de Dados para o sistema ProSchool, desenvolvimento do nosso sistema: https://github.com/GrazielaSousa/ProSchool







---- TABELAS CRIADAS
CREATE TABLE Cadastro_Alunos
( 
ID_Registro_Aluno int identity,
CPF VARCHAR (11) ,
NOME VARCHAR (100) ,
ENDERECO1 VARCHAR (150) ,
BAIRRO VARCHAR (50) ,
CIDADE VARCHAR (50) ,
ESTADO VARCHAR (2) ,
CEP VARCHAR (8) ,
DATA_NASCIMENTO DATE,
IDADE SMALLINT,
SEXO VARCHAR (1) ,
 ) 


ALTER TABLE Cadastro_Alunos ADD PRIMARY KEY (ID_Registro_Aluno) --DDL para adicionar a chave primaria na tabela Cadastro_Alunos
ALTER TABLE Cadastro_Alunos ADD Login_Registro VARCHAR(20) NULL, Senha_Registro varbinary --DDL para adicionar a coluna Login e Senha
ALTER TABLE Cadastro_Alunos ADD Nome_Responsavel VARCHAR(20) NULL  ----- DDL para adicionar coluna Nome Responsavel


---------------------------------------------------------------------------------------------------------------------------------------------------------------

CREATE TABLE Cadastro_Responsavel
( 
ID_Registro_Responsavel int identity,
CPF VARCHAR (11) ,
NOME VARCHAR (100) ,
DATA_NASCIMENTO DATE,
SEXO VARCHAR (1) ,
 )

 ALTER TABLE Cadastro_Responsavel ADD PRIMARY KEY (ID_Registro_Responsavel) --DDL para adicionar a chave primaria na tabela Cadastro_Respónsavel
 ALTER TABLE Cadastro_Responsavel ADD ID_Registro_Aluno integer ---especifica numeros inteiros, quando for criar uma chave estrangeira bom utilizar.
 ALTER TABLE Cadastro_Responsavel add constraint fk_ID foreign key (ID_Registro_Aluno) references Cadastro_Alunos ------adicionando a chave estrangeiro fazendo a referencia para a tabela Cadastro_Alunos

 ---------------------------------------------------------------------------------------------------------------------------------------------------------------

 create table Login_Aluno
(
ID_Login int identity,
Login_Usu VARCHAR (20),
Senha_Usu VARBINARY,
)

 ALTER TABLE Login_Aluno ADD PRIMARY KEY (ID_Login) --- DDL adicionando a chave primaria

----------------------------------------------------------------------------------------------------------------------------------------------------------------

CREATE TABLE Cadastro_Professores
( 
ID_Registro_Proff int identity,
CPF VARCHAR (11) ,
NOME VARCHAR (100) ,
ENDERECO1 VARCHAR (150) ,
BAIRRO VARCHAR (50) ,
CIDADE VARCHAR (50) ,
ESTADO VARCHAR (2) ,
CEP VARCHAR (8) ,
DATA_NASCIMENTO DATE,
IDADE SMALLINT,
SEXO VARCHAR (1) ,
 )  


Alter Table Cadastro_Professores ADD Primary Key (ID_Registro_Proff) --DDL para adicionar a chave primaria na tabela Cadastro_Professores
alter Table Cadastro_Professores ADD Login_Credencial varchar(20) null, Senha_Registro varbinary --DDL para adicionar a coluna Login e Senha

-----------------------------------------------------------------------------------------------------------------------------------------------------------------

CREATE TABLE Gerenciar_Aluno_Turma
(
RA_Aluno int identity,
Numero_Matricula char,
Data_matricula date,
)

Alter Table Gerenciar_Aluno_Turma ADD Primary Key (RA_Aluno) --DDL para adicionar a chave primaria na tabela Gerenciar_Aluno_Turma
------------------------------------------------------------------------------------------------------------------------------------------------------------------

create table Turmas
(
Codigo_Turma int identity,
Descricao_Curso varchar (100)
)

alter table Turmas ADD PRIMARY KEY (Codigo_Turma) --DDL para adicionar a chave primaria

 alter table Turmas ADD RA_Aluno integer -------quando for criar uma chave estrangeira bom utilizar.
 alter table Turmas add constraint FK_RA foreign key (RA_Aluno) references Gerenciar_Aluno_Turma ------adicionando a chave estrangeiro fazendo a referencia para a tabela Gerenciar_Aluno_Turma

 -----------------------------------------------------------------------------------------------------------------------------------------------------------------

 CREATE TABLE Disciplinas
(
Codigo_Disciplina int identity,
Nome_Disciplina char,
)

Alter Table Disciplinas ADD Primary Key (Codigo_Disciplina)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------


CREATE TABLE Ensino_Online
(
Cod_Ensino int identity,
Materiais char,
Biblioteca char,
Atividades char,
)

Alter Table Ensino_Online ADD  Nota_Avaliacao char		-- DDL adicionar coluna
Alter Table Ensino_Online ADD Primary Key (Cod_Ensino) --DDL para adicionar a chave primaria na tabela Gerenciar_Aluno_Turma

---------------------------------------------------------------------------------------------------------------------------------------------------------------------

-----------------------------------------CRIANDO RELACIONAMENTO EM DEMAIS TABELAS.-----------------------------------------------------------------------------------



  -- Nessa linha foi realizado uma alteração na tabela Gerenciar_Aluno_Turma adicionando uma nova ID_REGISTRO_ALUNO para se tornar uma chave estrangeira, criando uma referencia para a tabela Cadastro_Alunos.
 alter table Gerenciar_Aluno_Turma ADD ID_Registro_Aluno integer
 alter table Gerenciar_Aluno_Turma ADD Constraint RA_FK FOREIGN KEY (ID_Registro_Aluno) references Cadastro_Alunos

 --  DA MESMA FORMA PARA OS DEMAIS !
 alter table Gerenciar_Aluno_Turma ADD CO_Registro_Aluno integer
 alter table Gerenciar_Aluno_Turma ADD Constraint CO_RA_FK FOREIGN KEY (CO_Registro_Aluno) references Gerenciar_Turmas_Professores_Disciplina
 --------------------------------------------------------------------------------------------------------------------------------------------

 alter table Turmas ADD CO_Turmas integer
 alter table Turmas ADD Constraint CO_Turmas_FK FOREIGN KEY (CO_Turmas) references Gerenciar_Turmas_Professores_Disciplina

 ---------------------------------------------------------------------------------------------------------------------------------------------
  alter table Disciplinas ADD CO_Disciplina integer
 alter table Disciplinas ADD Constraint CO_Disciplinas_FK FOREIGN KEY (CO_Disciplina) references Gerenciar_Turmas_Professores_Disciplina
 ---------------------------------------------------------------------------------------------------------------------------------------------

  alter table Cadastro_Professores ADD CO_Cadastro_Professores integer
 alter table Cadastro_Professores ADD Constraint CO_Cadastro_Professores_FK FOREIGN KEY (CO_Cadastro_Professores) references Gerenciar_Turmas_Professores_Disciplina

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------

  alter table Ensino_Online ADD ID_Turmas integer
 alter table Ensino_Online ADD Constraint ID_Turmas_FK FOREIGN KEY (ID_Turmas) references Turmas





 -----------------------------------------CRIANDO RELACIONAMENTO EM DEMAIS TABELAS.-----------------------------------------------------------------------------------



  -- Nessa linha foi realizado uma alteração na tabela Gerenciar_Aluno_Turma adicionando uma nova ID_REGISTRO_ALUNO para se tornar uma chave estrangeira, criando uma referencia para a tabela Cadastro_Alunos.
 alter table Gerenciar_Aluno_Turma ADD ID_Registro_Aluno integer
 alter table Gerenciar_Aluno_Turma ADD Constraint RA_FK FOREIGN KEY (ID_Registro_Aluno) references Cadastro_Alunos

 --  DA MESMA FORMA PARA OS DEMAIS !
 alter table Gerenciar_Aluno_Turma ADD CO_Registro_Aluno integer
 alter table Gerenciar_Aluno_Turma ADD Constraint CO_RA_FK FOREIGN KEY (CO_Registro_Aluno) references Gerenciar_Turmas_Professores_Disciplina
 --------------------------------------------------------------------------------------------------------------------------------------------

 alter table Turmas ADD CO_Turmas integer
 alter table Turmas ADD Constraint CO_Turmas_FK FOREIGN KEY (CO_Turmas) references Gerenciar_Turmas_Professores_Disciplina

 ---------------------------------------------------------------------------------------------------------------------------------------------
  alter table Disciplinas ADD CO_Disciplina integer
 alter table Disciplinas ADD Constraint CO_Disciplinas_FK FOREIGN KEY (CO_Disciplina) references Gerenciar_Turmas_Professores_Disciplina
 ---------------------------------------------------------------------------------------------------------------------------------------------

  alter table Cadastro_Professores ADD CO_Cadastro_Professores integer
 alter table Cadastro_Professores ADD Constraint CO_Cadastro_Professores_FK FOREIGN KEY (CO_Cadastro_Professores) references Gerenciar_Turmas_Professores_Disciplina

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------

  alter table Ensino_Online ADD ID_Turmas integer
 alter table Ensino_Online ADD Constraint ID_Turmas_FK FOREIGN KEY (ID_Turmas) references Turmas
 ---------------------------------------------------------------------------------------------------------------------------------------------------------------------
   alter table Ensino_Online ADD ID_Disciplinas integer
 alter table Ensino_Online ADD Constraint ID_Disciplinas_FK FOREIGN KEY (ID_Disciplinas) references Turmas

 ---------------------------------------------------------------------------------------------------------------------------------------------------------------------
   alter table Ensino_Online ADD ID_Disciplinas integer
 alter table Ensino_Online ADD Constraint ID_Disciplinas_FK FOREIGN KEY (ID_Disciplinas) references Turmas

