- Procedures

```
CREATE OR REPLACE
PROCEDURE PROC_DET_FUNC
IS
  CURSOR emp_cur
  IS
    SELECT first_name, last_name, salary FROM HR.EMPLOYEES;
    --RECEBENDO VALORES DO CURSOR
    emp_rec emp_cur%rowtype;
BEGIN
  FOR emp_rec IN emp_cur
  LOOP
    dbms_output.put_line('Nome do funcionario: ' || emp_rec.first_name);
    dbms_output.put_line('Sobrenome do funcionario: ' ||emp_rec.last_name);
    dbms_output.put_line('Salário do funcionario: ' ||emp_rec.salary);
    dbms_output.put_line('---------------------------------------------');
  END LOOP;
END;
```

- Executando procedure

```
SET serveroutput on
begin
 PROC_DET_FUNC;
end;
```

- Outra forma de execucao

```
EXECUTE PROC_DET_FUNC;
```

- Procedure para retornar informações

```
CREATE OR REPLACE PROCEDURE PROC_INF_DEPTO
IS
  CURSOR FUN_CURSOR
  IS
    SELECT a.DEPARTMENT_ID,b.DEPARTMENT_NAME,SUM(salary)SALARIO FROM HR.EMPLOYEES a
    inner join HR.DEPARTMENTS b
        on a.department_id=b.department_id
    group by a.DEPARTMENT_ID,b.DEPARTMENT_NAME;

    FUN_REC FUN_CURSOR%rowtype;
BEGIN
  FOR FUN_REC IN FUN_CURSOR
  LOOP
    dbms_output.put_line('Codigo Depto: ' || FUN_REC.DEPARTMENT_ID ||
     '. Nome Depto: ' ||FUN_REC.DEPARTMENT_NAME || '. Total Salário do Depto: ' ||FUN_REC.salario);
  END LOOP;
  exception
  when others then
  dbms_output.put_line('Erro: '||sqlerrm);
END;

```

- EXECUTANDO

```
EXECUTE PROC_INF_DEPTO;
```

- PROCEDURE CALCULADORA

```
CREATE OR replace PROCEDURE proc_calc(operacao IN VARCHAR, --A ADICAO --D DIVISAO --S -SUBTR M --MULTIPL
                                      pnum1    IN NUMBER,
                                      pnum2    IN NUMBER,
                                      retorno OUT NUMBER)

IS
MSG_OUTRAS EXCEPTION;
BEGIN

 IF operacao='A' THEN
    retorno := pnum1 + pnum2;
  ELSIF operacao='S' THEN
    retorno := pnum1 - pnum2;
  ELSIF operacao='M' THEN
    retorno := pnum1*pnum2;
  ELSIF operacao='D' THEN
    retorno := pnum1/pnum2;
    else
    raise MSG_OUTRAS;
END IF;
  EXCEPTION
  WHEN MSG_OUTRAS THEN
    dbms_output.put_line('Erro nao catalogado');

  WHEN OTHERS THEN
    dbms_output.put_line('erro: '||SQLERRM);
  END;
```

- EXECUTANDO PROCEDURE

```
  DECLARE
  retorno number:=0;
  BEGIN
    proc_calc ('x',10,3,retorno);
    dbms_output.put_line(retorno);
  END;
```
