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
  - Transação nao torna visivel para as outras ate que seja encerrada com sucesso.
- (D)urabilidade
  - As alterações feitas por uma transação devem persistir, mesmo se houver falhas subsequentes no sistema.

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

# Scripts

- SELECT USER FROM DUAL; (Tabela Virtual do oracle)

**Dar permissão das tabelas para Aluno**

```
GRANT select ON HR.COUNTRIES TO ALUNO WITH GRANT OPTION;
GRANT select ON HR.DEPARTMENTS TO ALUNO WITH GRANT OPTION;
GRANT select ON HR.EMPLOYEES TO ALUNO WITH GRANT OPTION;
GRANT select ON HR.JOB_HISTORY TO ALUNO WITH GRANT OPTION;
GRANT select ON HR.JOBS TO ALUNO WITH GRANT OPTION;
GRANT select ON HR.LOCATIONS TO ALUNO WITH GRANT OPTION;
GRANT select ON HR.REGIONS TO ALUNO WITH GRANT OPTION;
```

## Operadores

### Exercícios

- [Comparação](https://github.com/thomaserick/oracle_studies/blob/master/scripts/comparacao.md)
- [Matemáticos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicos.md)
- [Lógica](https://github.com/thomaserick/oracle_studies/blob/master/scripts/logica.md)

## Linguagem

- DML (Data Manipulation Language)

  - Gerenciamento de dados do banco
    - SELECT
    - INSERT
    - UPDATE
    - DELETE

* DDL (Data Definition Language)

  - Estrutura de dados ou esquemas
    - CREATE
    - ALTER
    - DROP
    - TRUNCATE

* DCL (Data Control Language)

  - Definir acesso/controle dos dados/objetos
    - GRANT -> Atribui privilégios de acesso do usuário a objetos do banco de dados
    - REVOKE -> remove os privilégios de acesso aos objetos obtidos pelo GRANT

* TCL (Transaction Control Languade)
  - START TRANSACTION
  - COMMIT
  - SAVEPOINT
  - ROLLBACK

### Exercícios

- [DML](https://github.com/thomaserick/oracle_studies/blob/master/scripts/dml.md)
- [DDL](https://github.com/thomaserick/oracle_studies/blob/master/scripts/ddl.md)
- [DCL_GRANT](https://github.com/thomaserick/oracle_studies/blob/master/scripts/dclGrant.md)
- [DCL_Revoke](https://github.com/thomaserick/oracle_studies/blob/master/scripts/dclRevoke.md)
- [TCL](https://github.com/thomaserick/oracle_studies/blob/master/scripts/tcl.md)

## Linguagem SQL

## Operador

- [UNION](https://github.com/thomaserick/oracle_studies/blob/master/scripts/union.md)

  - Usado para combinar o conjunto de resultados de duas ou mais instruções.
  - As colunas devem ter tipos de dados semelhantes

- [UNION ALL](https://github.com/thomaserick/oracle_studies/blob/master/scripts/union.md)
  - Permitir valores duplicados

## JOINS (Junções)

- [JOINS(Junções)](https://github.com/thomaserick/oracle_studies/blob/master/scripts/join.md)

  - Registro correspondetes em ambas as tabelas

- [LEFT JOIN](https://github.com/thomaserick/oracle_studies/blob/master/scripts/join.md)

  - Retorna todos os registros da tabela à esquerda

- [RIGHT JOIN](https://github.com/thomaserick/oracle_studies/blob/master/scripts/join.md)

  - Retorna todos os registros da tabela à direita

- [FULL JOIN](https://github.com/thomaserick/oracle_studies/blob/master/scripts/join.md)
  - Retorna todos os registros da tabela à direita e à esquerda

## SUBQUERYS

- [Subquerys](https://github.com/thomaserick/oracle_studies/blob/master/scripts/subquerys.md)

- Uma subconsulta, é uma instrução SELECT que está condicionada dentro de outra SQL

## Funções de Agregação

- Executam um cálculo em um conjunto de valores e retornam um único valor
- ignoram valores nulos
- são usadas com a cláusula GROUP BY

[**AVG**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/agregacao.md)

- Retorna a média dos valores em um grupo.
- valores nulos são ignorados

[**MIN**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/agregacao.md)

- Retorna o valor mínimo na expressão

[**MAX**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/agregacao.md)

- Retorna o valor máxima na expressão

[**SUM**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/agregacao.md)

- Retorna a soma de todos os valores ou somente os valores DISTINCT na expresão

[**COUNT**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/agregacao.md)

- Retorna o número de itens de um grupo

[**STDDEV**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/agregacao.md)

- Retorna o desvio padrão estatístico de todos os valores da expressão especifica

[**VARIANCE**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/agregacao.md)

- Determina a variância de n,ignorando valores nulos

## Funções de Caracteres

[**ASCII**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Retorna o valor do código ASCII do caracter mais à esquerda

[**LTRIM**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Retorna uma expressão de caracter após remover espaços em branco à esquerda

[**RTRIM**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Retorna uma expressão de caracter após remover espaços em branco à direita

[**TRIM**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Trunca espaços em branco

[**CONCAT**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Faz a concatenação de odis ou mais valores

[**REPLACE**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Substitui todas as ocorrências de um valor por outro valor

[**RPDA/LPAD**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Repete um valor da cadeia de caracteres um número específico de vezes

[**UPPER**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Converte caracteres minusculos em maiúsculos

[**LOWER**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Converte caracteres maiúsculos em minúsculos

[**REVERSE**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Inverte um valor da cadeia de caracteres

[**LENGHT**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Retorna o numero de caracteres, excluindo os espaços em braco

[**SUBSTR**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Retorna um substring de caracteres com dados de caracteres

[**INITCAP**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Impõe uma letra maiúscula na primeira letra de cada palavra

[**TRANSLATE**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Substitui um caracter por outro

[**DECODE**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Decodifica a expressão se for verdade o valor da expressão

[**INSTR**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/caracteres.md)

- Devolve a posição da primeira ocorrência de string2 dentro de string1

## Funções de Classificação

[**RANK**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/classificacao.md)

- Retorna um valor de classificação em cada linha

[**NTILE**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/classificacao.md)

- Distribui as linahs de uma partição ordenada em um número de grupos especificado.

[**DENSE_RANK**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/classificacao.md)

- Retorna a classificação de linha dentro da partição de um conjunto de resultados

[**ROW_NUMBER**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/classificacao.md)

- Retorna o número sequencial de uma linha em uma partição de um conjunto de resultados

## Funções de Controle de Fluxo

[**CASE**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/controleFluxo.md)

- Case operador

[**NULLIF()**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/controleFluxo.md)

- Return NULL

## Funções Matemáticas

[**ABS**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Retorna um valor absoluto(positivo) da expressão numérica

[**DBMS_RANDOM**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Retorna um valor float pseudoaleatório de 0 a 1

[**ROUND**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Arredonda o valor

[**TRUNC**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Trunca as casas decimais de um valor

[**SQRT**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Retorna a raiz quadrada de um expressão

[**SIGN**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Retorna -1 para negativo, 0 neutro , 1 positivo

[**POWER**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Eleva a potência de n o valor

[**MOD**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Retorna a sobra de uma expressão

[**EXP**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/matematicas.md)

- Devolve o valor elevado a N

## Funções de Criptografia

[**RAWTOHEX**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/criptografia.md)

- Converte os caracteres para Hexadecimal

[**\*DBMS_OBFUSCATION_TOOLKIT**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/criptografia.md)

- Disponibiliza o método MD5

[**UTL_RAW**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/criptografia.md)

- Manipulação de dados, tendo como foco a conversão dos tipos.

## Funções de Limite

[**ROWNUM**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/limite.md)

- Limit de registro

## Funções de Conversão

[**CAST**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/conversao.md)

- Converte uma expressão de um tipo de dados em outro

[**TO_CHAR(data)**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/conversao.md)

- Converte data em String

[**TO_DATE(string)**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/conversao.md)

- Converte Strinf em data

[**NVL()**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/conversao.md)

- Tratar valor nulo

## Funções de Data Hora

[**ADD_MONTHS**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/dataHora.md)

- Adiciona n meses no calendário à data.

[**MONTHS_BETWEEN\***](https://github.com/thomaserick/oracle_studies/blob/master/scripts/dataHora.md)

- Determina numero de meses entre data1 e data2

[**LAST_DAY**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/dataHora.md)

- Devolve o último dia do mês de data1

[**NEXT_DAY**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/dataHora.md)

- Devolve a data do próximo dia da semana especificado por c

## Funções de Sistema

[**USER**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/infoSystem.md)

- Nome do utilizador Oracle que abriu a sessão

[**UID**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/infoSystem.md)

- Mostra o número que a base de dados atribuiu ao utilizador

[**USEREN(arg)**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/infoSystem.md)

- Envolve dados da sess~~ao atual,os valores de argumento podem ser vários

[## Views](https://github.com/thomaserick/oracle_studies/blob/master/scripts/views.md)

- Tabela definida como tabela virtual
- **Vantagens**

  - Reuso
  - Segurança
  - Simplificação do código

## TEMP TABLE

[**TEMPORARY**](https://github.com/thomaserick/oracle_studies/blob/master/scripts/tempTable.md)

- Tabela criada será temporária, expira assim que a sessa ou transação terminar.

## PL/SQL

- É uma linguagem de programação preceduralda Oracle
- É case-insentive

  - loop
  - while
  - for
  - arrays

### Estrutura de Bloco PL/SQL

```
DELCARE(opcional)
*variaveis
BEGIN(obrigatório)
- instruções PL/SQL

EXCEPTION(opcional)
*Ações a serem desempenhadas

END;(obrigatorio)

```

### Tipos de Blocos

- Anônimo

```
BEGIN
 - statements
[EXCEPTION]
END;
```

- Procedimento

```
PROCEDURE name
IS
BEGIN
-statements
[EXCEPTION]
END;
```

- Função

```
FUNCTION name
RETURN datatype
IS BEGIN
-statements
RETURN value;
[EXCEPTION]
END;
```

### Conjunto de Caracteres

- Letras
- Digitos
- Símbolos
  - ; -> Termina os statements e declarações
  - % -> Indicador de atributo
  - @ -> Indicador de localização
  - <<e>> -> Delimitadores de labels
  - := -> Atribuição de valor a variavel
  - => -> Operador de associação
  - .. -> Operador de range

### Variáveis

- Adote padrões para dar nomes a varáveis
- Iniciar uma variavel ":=" ou DEFAULT

### Atributos

- [TYPE](https://github.com/thomaserick/oracle_studies/blob/master/scripts/atributo.md)
  - Campo
- [ROWTYPE](https://github.com/thomaserick/oracle_studies/blob/master/scripts/atributo.md)
  - Tabela toda

### Tipo de registros

- É uma coleção de valores individuais relacionados de alguma forma.

### Escopo de Variaveis

- Podemos referenciar a variável.

  - [Local](https://github.com/thomaserick/oracle_studies/blob/master/scripts/escopo.md)

    - Bloco onde esta declarado

  - [Global](https://github.com/thomaserick/oracle_studies/blob/master/scripts/escopo.md)
    - Para todos seus sub-blocos

### Estrutura IF

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/ifElse.md)

### Estrutura Case

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/case.md)

### Estrutura GoTo

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/goto.md)

### Estrutura LOOP

- Estrutura de repetição

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/loop.md)

### Estrutura LOOPFOR

- Estrutura de repetição
- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/loopFor.md)

### Estrutura LOOPWHILE

- Estrutura de repetição

  - Condition - Condição que será testada a cada interação do loop.

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/loopWhile.md)

### Excessões

- Existe 3 tipos de excessões

  - Erros predefinidos da Oracle

    - no_data_found
      - SELECT não retornou dados
    - too_many_rows
      - SELECT retornou mais de uma linha
    - value_error
      - Houve tentativa de operação ilegal
    - invalid_number
      - A conversão de uma string para um numero, falhou
    - zero_divide
      - ocorreu uma tentativa de dividir por zero
    - dup_val_on_index
    - cursor_already_open
      - Houve uma tentativa de abrir um cursor que foi aberto anteriormente
    - not_logger_on
      - Uma chamada de banco de dados foi feita sem o usuário conectado
    - transacton_becked_out
      - Uma parte remota de uma transação teve "rollback"
    - login_danied
      - Um login no banco de dados falhou
    - program_error
      - A PL/SQL encontrou um problema interno
    - storage_error
      - A PL/SQL ficou sem memória ou memória esta corrompida

  - Erros nao definidos da Oracle
  - Erros definidos pelo usuário

  - SQLCODE
    - Retorna um valor numérico para o codigo de erro
  - SQLERRM
    - Retorna um caracter contendo a mensagem associada com o número do erro

### Cursores

- Cursor Implicito
  - DML e comandos SELECT
- Cursor Explícito
  - Definidos pelo usuário para manipular registros SELECT

### Functions

- É semelhante a uma procedure
- Sempre retorna infomações

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/functions.md)

### Procedures

- Bloco de instruções que executa uma ou mais tarefas
- Contém cabeçalho e corpo
- Parâmetros

  - IN
  - OUT
  - IN OUT

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/procedures.md)

### Triggers

- Tipos

  - ROW LEVEL
    - Usada para gravação de logs,Verificação de dados
  - STATEMENT
    - Tem a finalidade de tratar a execução de ações sobre tabelas

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/triggers.md)

### Packages

- Coleção de Objetos PL/SQL , contém:

  - Procedures
  - Functions
  - Cursores
  - Declarações

## PIVOT

- Informações em um relatório com referência cruzadas com formato de planilha apartir de qualquer tabela relacional.
- Transforma linhas em Colunas

- [exemplos](https://github.com/thomaserick/oracle_studies/blob/master/scripts/pivot.md)

## Projeto - Mini Erp MultiEmpresas

- [Diagrama](https://github.com/thomaserick/oracle_studies/blob/master/helpers/miniErp.png)

- [Tabelas](https://github.com/thomaserick/oracle_studies/blob/master/scripts/miniErpTables.md)

- [Triggers](https://github.com/thomaserick/oracle_studies/blob/master/scripts/miniErpTriggers.md)

- [Procedures](https://github.com/thomaserick/oracle_studies/blob/master/scripts/miniErpProcedures.md)

- [Views](https://github.com/thomaserick/oracle_studies/blob/master/scripts/miniErpViews.md)

**Helpers**

- [Format GitHub](https://help.github.com/en/articles/basic-writing-and-formatting-syntax)
