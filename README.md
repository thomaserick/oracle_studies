# Getting Started Oracle

# Resumo

## Instalação

[Download Oracle XE](https://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html)

[Download para SQL DEVELOPER](https://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html)

## SQL(Structure Query Language)

- Surgiu em 1974 nos laboratórios da IBM(Califórnia)
- Chamada anterior de SEQUEL (Structured Query English Language)

## PL/SQL (Procedural Language extension to SQL)

- Introduzida em 1988
- é uma extensão da linguagem padrão SQL para o SGBD Oracle
- Permite que a manipulação de dados seja incluída em unidades de programas

## Tablespace

- São agrupamentos lógicos.
- Elas ajudam a organizar o banco.
- Uma tablespace está vinculada a um ou mais datafile. (que são os arquivos físicos no Sistema Operacional.)

## DB Relacional

- É a arquitetura na qual os dados são armazenados em tabelas que se relacionam entre si
- Permite controle de redundância de dados
- Garante integridade dos dados
- Garente privacidade
- Otimização de espaço de Armazenamento
- Performece de acesso a informações
- Cada tabela tem seu nome único

## Tipos de Entidades

- Forte
  - Independe de quaisquer outras para existir
- Fraca

  - Depende de outra entidade para exister

- Associativa

  - Surge quando há a necessidade de associar um entidade a um relacionamento existente

  ## Cardinalidades

  - 1 para 1(1-1)
  - 1 para muitos(1-N)
  - Muitos para Muitos(N-N)

## ACID (Propriedade das transações)

- (A)tomicidade
  - Uma transação é uma unidade atômica de processamento, ou ela é executada na sua totalidade ou então nada é executardo.
- (C)onsistência
  - Mantem a consistência do Banco de Dados.
- (I)solamento
  -Transação nao torna visivel para as outras ate que seja encerrada com sucesso.
- (D)urabilidade
  -As alterações feitas por uma transação devem persistir, mesmo se houver falhas subsequentes no sistema.

## CRUD (4 operações basicas)

- Create
- Read
- Update
- Delete

## Constraints

- Utilizadas para especificar regras de armazenamentos de dados nas tabelas e garantir integridade.
- Tipos
  - NOT NULL
  - UNIQUE
  - PRIMARY KEY
  - FOREIGN KEY
  - DEFAULT
  - INDEX

### Criando uma Tablespace

```
create tablespace curso
datafile
'C:\oraclexe\app\oracle\oradata\XE\curso.dbf'
size 100m autoextend on next 50m maxsize 500m
online
permanent
extent management local autoallocate
segment space management auto;

-- criando usuario

   create user aluno
          identified by aluno
          default tablespace curso
          temporary tablespace TEMP;
  -- permissao para aluno
  grant create session, connect, resource to aluno;

  alter user aluno quota unlimited on curso;

--deletar user
  drop user aluno;

--deletar tablespace
DROP TABLESPACE curso
  INCLUDING CONTENTS and  DATAFILES
    CASCADE CONSTRAINTS;




```

**Helpers**

- [Format GitHub](https://help.github.com/en/articles/basic-writing-and-formatting-syntax)
