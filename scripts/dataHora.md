- Pegando data do servidor

```
select sysdate from dual;
```

- Utilizando mascaras

```
select
  sysdate "Data do servidor",
  to_char(sysdate,'yyyy-mm-dd hh24-mi-ss') "Data formatada",
  to_char(sysdate, 'SCC') "Século"
from dual;
```

- Formatando datas

- MM = Retorna o número representando o mês. Ex: 04

```
select to_char(sysdate, 'MM') as campo from dual;
```

- MON = Retorna a abreviação do mês, por exemplo ‘ABR’

```
select to_char(sysdate, 'MON') as campo from dual;
```

- MONTH = Retorna o nome completo do mês, por exemplo: ‘ABRIL’

```
select to_char(sysdate, 'MONTH') as campo from dual;
```

- DD = retorna o dia da data informada como parâmetro Ex.: 07

```
select to_char(sysdate, 'DD') as campo from dual;
```

- DY = retorna a abreviação do dia da semana. Exemplo: SEG

```
select to_char(sysdate, 'DY') as campo from dual;
```

- YYYY = retorna o ano com 4 dígitos. Exemplo: 2014

```
select to_char(sysdate, 'YYYY') from dual;
```

- YY = retorna os últimos dois números do ano. Exemplo: 14

```
select to_char(sysdate, 'YY') as campo from dual;
```

- AM (ou PM) = retorna se a hora é de manhã (AM) ou a tarde (PM).

```
select to_char(sysdate, 'AM') as campo from dual;
```

- HH = retorna a hora (0 – 12)

```
select to_char(sysdate, 'HH') as campo from dual;
```

- HH24 = retorna a hora (0 – 24)

```
select to_char(sysdate, 'HH24') from dual;
```

- MI = retorna o minuto

```
select to_char(sysdate, 'MI') as campo  from dual;
```

- SS = retorna o segundo

```
select to_char(sysdate, 'SS') as campo  from dual;
```

- Os formatos de data podem ser utilizados em conjuntos como por exemplo:

```
select to_char(sysdate, 'HH24:MI:SS') as campo  from dual
```

- Outro exemplo retornando a data no formato mais comum no Brasil.

```
select to_char(sysdate, 'DD/MM/YYYY HH24:MI:SS') from dual;
```

- Campo tratado

```
select a.first_name,a.hire_date orig,
       to_char(a.hire_date, 'MON')mex_ext,
       to_char(a.hire_date, 'MM')mes_num,
       to_char(a.hire_date, 'MONTH')mes_num,
       to_char(a.hire_date, 'DY')dia_semana
from HR.EMPLOYEES a
```

- Subtraindo dias

```
ALTER SESSION SET nls_date_format = 'dd-mm-yyyy hh24:mi:ss';
```

- Adicionando dias

```
SELECT SYSDATE+5 FROM DUAL;
```

- Diferenca entre os dias

```

SELECT TO_DATE(SYSDATE)-TO_DATE('2018-01-01') DIF_DIAS FROM DUAL;
```

- Adicionando horas

```
ALTER SESSION SET nls_date_format = 'yyyy-mm-dd hh24:mi:ss';
SELECT SYSDATE, SYSDATE+5/24 DATA_HORA_ADD FROM DUAL
```

- Adicionar meses

```


SELECT SYSDATE DATA_ATUAL, ADD_MONTHS(SYSDATE,2)ADD_MESES FROM DUAL;
```

- Subtrair meses

```
SELECT SYSDATE DATA_ATUAL, ADD_MONTHS(SYSDATE,-2)ADD_MESES FROM DUAL;
```

- Qtd de meses entre datas

```
SELECT  first_name,a.hire_date,
         sysdate,
         trunc(months_between(sysdate,a.hire_date)) Meses
FROM HR.EMPLOYEES a;
```

- Ultimo dia mes

```
SELECT  sysdate hoje,last_day(sysdate)Ult_dia from dual;

SELECT  a.hire_date,last_day(a.hire_date)Ult_dia from  HR.EMPLOYEES a;
```

- Next day
  - Cenario para descobrir um data que acontece toda segunda quinta de cada cada mes;
    descobrindo data da proxima segunda feira - 1 – Domingo - 2 – Segunda-Feira - 3 – Terça-Feira - 4 – Quarta-Feira - 5 – Quinta-Feira - 6 – Sexta-Feira - 7 – Sábado.

```
select NEXT_DAY(TRUNC(SYSDATE), 2) from dual;

select NEXT_DAY(NEXT_DAY(TRUNC(SYSDATE), 2),2) from dual;

SELECT TRUNC((MONTHS_BETWEEN(SYSDATE, TO_DATE('05/11/1977','dd/mm/yyyy')))/12) AS idade FROM DUAL;

SELECT TRUNC((MONTHS_BETWEEN(SYSDATE, TO_DATE('05/11/1977','dd/mm/yyyy')))) AS idade_MESES FROM DUAL

```

- Dias de vida

```

SELECT SYSDATE-TO_DATE('05/11/1977','dd/mm/yyyy') FROM DUAL;

```

- Duas de vida

```

SELECT TRUNC(SYSDATE-TO_DATE('05/11/1977','dd/mm/yyyy')) DIAS FROM DUAL;

```
