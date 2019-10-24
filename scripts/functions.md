- Criando funçao para media ponderada;

```
CREATE OR REPLACE FUNCTION Fn_mediaPond
                    (nota1 in number,
                     peso1 in number,
                     nota2 in number,
                     peso2 in number)
return number
is
media_pond number;
begin
        media_pond:=(nota1*peso1+nota2*peso2)/(peso1+peso2);
        return media_pond;
end;
```

- Retornando valor de função

```
select  Fn_mediaPond(10,1,10,1) from SYS.DUAL;

- Retornando atraves de output]
SET SERVEROUTPUT ON
BEGIN
dbms_output.put_line(Fn_mediaPond(5,5,10,1));
END;
```

- Sem parametros

```
CREATE OR REPLACE FUNCTION FnNome
   RETURN varchar IS
   v_nome varchar(20);
BEGIN
   SELECT a.FIRST_NAME
   INTO   v_nome
   FROM   hr.EMPLOYEES a WHERE a.EMPLOYEE_ID=100;

   RETURN v_nome;
END;
```

select FnNome from DUAL;

- Com parametros

```
CREATE OR REPLACE FUNCTION FnNome2(p_id in number)
   RETURN varchar IS
   v_nome varchar(20);
BEGIN
   SELECT a.FIRST_NAME
   INTO   v_nome
   FROM   hr.EMPLOYEES a WHERE a.EMPLOYEE_ID=p_id;

   RETURN v_nome;
END;

select FnNome2(103) from DUAL;

```

- Function simular aumento

```
CREATE OR REPLACE FUNCTION FnAumento(p_pct in number,p_id_func in number)
   RETURN number IS
   v_Sal_novo number(20);
BEGIN
   SELECT ((a.SALARY/100)*p_pct)+a.SALARY
   INTO   v_Sal_novo
   FROM   hr.EMPLOYEES a where a.EMPLOYEE_ID=p_id_func;

   RETURN v_Sal_novo;
END;
```

- Executa a Função

```
select a.FIRST_NAME,
       a.SALARY as sal_antigo,
       FnAumento(10,a.EMPLOYEE_ID) as sal_novo
from  hr.EMPLOYEES a;
```

- Exemplo de Update

```
create table notas
(id_aluno int,
 nota1 number,
 peso1 number,
 nota2 number,
 peso2 number,
 media number
 );

```

- Inserindo dados

```
insert into notas (id_aluno,nota1,peso1,nota2,peso2) values (1,8,4,6,6);
insert into notas (id_aluno,nota1,peso1,nota2,peso2) values (2,10,4,10,6);
insert into notas (id_aluno,nota1,peso1,nota2,peso2) values (3,5,4,5,6);
```

```
select * from notas;
```

- Update

```
UPDATE notas SET media=FN_MEDIAPOND(nota1, peso1, nota2, peso2)
where 1=1;

select * from notas;
```
