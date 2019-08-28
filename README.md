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

#Scripts

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

### Comparação

- OPERADOR IGUAL (=)

```
SELECT * FROM HR.EMPLOYEES a
WHERE a.JOB_ID='IT_PROG';
```

- OPERADOR MAIOR (>)

```
SELECT * FROM HR.EMPLOYEES a
WHERE a.HIRE_DATE>'03/02/06'
order by  a.HIRE_DATE asc;
```

- OPERADOR MENOR (<)

```
SELECT * FROM HR.EMPLOYEES a
WHERE a.HIRE_DATE<'03/02/06'
order by  a.HIRE_DATE asc;

```

- OPERADOR MAIOR IGUAL (>=)

```
SELECT * FROM HR.EMPLOYEES a
WHERE a.SALARY>='9000'
order by a.SALARY asc;
```

- OPERADOR MENOR IGUAL (<=)

```
SELECT * FROM HR.EMPLOYEES a
WHERE a.HIRE_DATE<='05/02/06'
order by  a.HIRE_DATE asc;
```

- OPERADOR DIFERENTE (<>)

```
SELECT * FROM HR.EMPLOYEES a
WHERE a.JOB_ID<>'IT_PROG';
```

- COMBINANDO OPERADORES

```
SELECT * FROM HR.EMPLOYEES a
WHERE a.JOB_ID='IT_PROG'
AND a.SALARY>4800
AND a.MANAGER_ID='103';
```

### Matemáticos

- OPERADOR DE ADICAO (+)

```
SELECT 1+3 AS RESULTADO FROM DUAL;

SELECT a.FIRST_NAME,
       a.SALARY,
       a.SALARY+530 as salario_novo
       FROM HR.EMPLOYEES a;
```

- OPERADOR DE SUBTRACAO (-)

```

SELECT 7-4 AS RESULTADO FROM DUAL;

SELECT a.FIRST_NAME,
       a.SALARY,
       a.SALARY-530 as salario_novo
       FROM HR.EMPLOYEES a;
```

- OPERADOR DE MULTIPLICAO (\*)

```
SELECT 7*4 AS RESULTADO FROM DUAL;

SELECT (7*4)*-1 AS RESULTADO FROM DUAL;

SELECT a.FIRST_NAME,
       a.SALARY,
       a.SALARY*1.10 as salario_novo
       FROM HR.EMPLOYEES a;


SELECT a.FIRST_NAME,
       a.SALARY,
       a.SALARY*0.10 as valor_acresc,
       a.SALARY*1.10 as salario_novo
       FROM HR.EMPLOYEES a;
```

- OPERADOR DE DIVISAO (/)

```
SELECT 2/4 AS RESULTADO FROM DUAL;

SELECT 4/2 AS RESULTADO FROM DUAL;

SELECT a.FIRST_NAME,
       a.SALARY,
       a.SALARY/10 as salario_novo
       FROM HR.EMPLOYEES a;
```

- OPERADOR MOD (%)

```
SELECT MOD(10,5) AS RESULTADO FROM DUAL;

SELECT MOD(10,3) AS RESULTADO FROM DUAL;
```

- Exmpressoes

```
select 2*4/3+3 from dual;
select ((2*4)/3)+3 from dual;
```

### Lógica

- Criar Tabela

```
CREATE TABLE senso
 (
ano INT NOT NULL,
cod_uf CHAR(2) NOT NULL,
estado VARCHAR2(50) NOT NULL,
cod_mun CHAR(7) NOT NULL,
nome_mun VARCHAR2(50) NOT NULL,
regiao VARCHAR2(150),
cod_meso_reg CHAR(4),
nome_meso_reg VARCHAR2(100) NOT NULL,
cod_mic_reg CHAR(5) NOT NULL,
nome_min_reg VARCHAR2(50) NOT NULL,
pib DECIMAL(12,3) NOT NULL,
populacao INTEGER NOT NULL,
pib_per_cap DECIMAL(12,3) NOT NULL
);

CREATE TABLE uf
(cod_uf CHAR(2) NOT NULL PRIMARY KEY,
 sigla_uf CHAR(2) NOT NULL,
 estado VARCHAR2(50) NOT NULL
);

```

- OPERADOR (WHERE)

```
	SELECT *
	FROM senso
	WHERE nome_mun='Jundiaí'
	and ano='2014';
```

- OPERADOR (AND)

```
	SELECT *
	FROM senso
	WHERE cod_uf='35'
	AND populacao >50000
	and ano='2014';
```

- OPERADOR (BETWEEN)

```
	select * from senso
	where cod_uf='35'
	and populacao between 5000 and 10000
	and ano='2014'
	order by populacao desc;
```

- OPERADOR (IN)

```
	select * from senso
	where cod_uf in ('35','12')
	and ano='2014';
```

- OPERADOR NOT IN

```
    select * from senso
    where cod_uf not in ('35','12')
    and ano='2014';
```

- LIKE LOCALIZA VALORES QUE CONTENHAM "OR" EM QUALQUER LUGAR

```
    select * from senso
    where nome_mun like ('%or%')
    and ano='2014';
```

- LIKE Encontra quaisquer valores que tenham "r" na segunda posição

```
    select * from senso
    where nome_mun like '_r%'
    and ano='2014';
```

- LIKE Localiza valores que começam com "A" e termina com "o"

```
    		select * from senso
    		where nome_mun like 'A%o'
    		and ano='2014';
```

- LIKE Localiza valores que começam com "A"

```
    	select * from senso
    		where nome_mun like 'A%'
    		and ano='2014';
```

- OPERADOR LIKE CORINGA \_\_

```
    	select * from senso
    		where nome_mun like '_ra%'
    		and ano='2014';
```

- OPERADOR NOT

```
    select ano,cod_uf,estado,nome_mun,populacao from senso
    where nome_mun not like ('A%')
    and cod_uf='35'
    and not populacao<40000
    and ano='2014';

    select ano,cod_uf,estado,nome_mun,populacao from senso
    where nome_mun not like ('A%')
    and cod_uf='35'
    and not populacao>40000
    and ano='2014';

- OPERADOR OR
```

    select * from senso
    where nome_mun like ('A%')
    and (cod_uf='35' or cod_uf='15');

```

- evidencia de erro
```

select \* from senso
where nome_mun like ('A%')
and cod_uf='35'
and cod_uf='15';

```
- OPERADOR IS NOT NULL
```

    select * from senso
    where regiao is not null;

```

- OPERADOR IS NULL
```

    select * from senso
    where regiao is null;

```

- OPERADOR HAVING
```

    select cod_uf,estado,count(*) as qtd
    from senso
    where ano='2014'
    group by cod_uf,estado having count(cod_mun)>500;

```

- OPERADOR HAVING
```

    select cod_uf,estado,count(*)qtd
    from senso
    where ano='2014'
    group by cod_uf,estado having count(cod_mun)<=500
    order by 3 desc ;

```

- OPERADOR HAVING
```

    select cod_uf,estado,count(cod_mun)qtd,
                  sum(populacao)
    from senso
    where ano='2014'
    group by cod_uf,estado having sum(populacao)>5000000;

```



**Helpers**

- [Format GitHub](https://help.github.com/en/articles/basic-writing-and-formatting-syntax)
```
