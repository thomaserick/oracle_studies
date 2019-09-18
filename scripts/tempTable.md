- A cláusula indica que os dados devem ser excluídos no final da transação ou no final da sessão.

```
CREATE GLOBAL TEMPORARY TABLE minha_temp (
  id           NUMBER,
  nome  VARCHAR2(20)
)
ON COMMIT DELETE ROWS;

```

- Inserindo, mas nao realizando commit,

```
INSERT INTO minha_temp VALUES (1, 'Teste1');
INSERT INTO minha_temp VALUES (2, 'Teste2');
INSERT INTO minha_temp VALUES (3, 'Teste3');
```

- Analisando counteudo

```
SELECT COUNT(*) FROM minha_temp;
select * from minha_temp;
```

- Commit and check contents.

```
COMMIT;
```

- Analisando counteudo

```
SELECT COUNT(*) FROM minha_temp;
```

- A cláusula indica que as linhas devem persistir além do final da transação.Eles serão removidos apenas no final da sessão.

```
CREATE GLOBAL TEMPORARY TABLE minha_temp (
  id           NUMBER,
  nome  VARCHAR2(20)
)
ON COMMIT PRESERVE ROWS;
```

- Inserindo, realizando commit,

```
INSERT INTO minha_temp VALUES (1, 'Teste1');
INSERT INTO minha_temp VALUES (2, 'Teste2');
INSERT INTO minha_temp VALUES (3, 'Teste3');
commit;
```

- Analisando counteudo

```
SELECT COUNT(*) FROM minha_temp;
```

- Desconecta

```
SELECT COUNT(*) FROM minha_temp;
```

- Carregando uma tabela temp com dados de uma tabela normal

```
CREATE global temporary TABLE empregados_temp
(
  EMPLOYEE_ID NUMBER(6, 0) NOT NULL
, FIRST_NAME VARCHAR2(20 BYTE)
, LAST_NAME VARCHAR2(25 BYTE) NOT NULL
, COMMISSION_PCT NUMBER(2, 2)
) ON COMMIT DELETE ROWS;
```

- Inserindo registros na temp

```
insert into empregados_temp
select a.EMPLOYEE_ID,a.FIRST_NAME,a.LAST_NAME,a.COMMISSION_PCT
from HR.EMPLOYEES a;
```

- Verificando dados antes do committ

```
select count(*) from empregados_temp;

commit;
```

- Verificando dados apos do commit

```
select count(*) from empregados_temp;

drop table empregados_temp;
drop table minha_temp;
```
