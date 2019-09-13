- Case

```
SELECT A.FIRST_NAME,A.SALARY,
CASE WHEN A.SALARY<5000 THEN 'Baixo'
     WHEN A.SALARY<10000 THEN 'Medio'
      WHEN A.SALARY<15000 THEN 'Medio Alto'
      ELSE   'Alto' END FAIXA
FROM HR.EMPLOYEES A
ORDER BY A.SALARY DESC;


SELECT A.FIRST_NAME,A.MANAGER_ID,
    CASE WHEN A.MANAGER_ID IS NULL THEN 'Gerente'
        ELSE 'Subordinado' END HIERARQ
    FROM HR.EMPLOYEES A;


select * from hr.LOCATIONS

SELECT UNIQUE COUNTRY_ID ID,
       CASE COUNTRY_ID
         WHEN 'AU' THEN 'Australia'
         WHEN 'BR' THEN 'Brazil'
         WHEN 'CA' THEN 'Canada'
         WHEN 'CH' THEN 'Switzerland'
         WHEN 'CN' THEN 'China'
         WHEN 'DE' THEN 'Germany'
         WHEN 'IN' THEN 'India'
         WHEN 'IT' THEN 'Italy'
         WHEN 'JP' THEN 'Japan'
         WHEN 'MX' THEN 'Mexico'
         WHEN 'NL' THEN 'Netherlands'
         WHEN 'SG' THEN 'Singapore'
         WHEN 'UK' THEN 'United Kingdom'
         WHEN 'US' THEN 'United States'
       ELSE 'Outros'
       END COUNTRY
FROM hr.LOCATIONS
ORDER BY COUNTRY_ID;


```

- NULLIF

```
SELECT NULLIF(100,100) FROM DUAL;

SELECT NULLIF(100,10) FROM DUAL;
-mao serve pra tratar retorno NULL
SELECT A.FIRST_NAME,A.COMMISSION_PCT,NULLIF(A.COMMISSION_PCT,0)
 FROM HR.EMPLOYEES A;

```
