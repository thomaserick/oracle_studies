```
SET SERVEROUTPUT ON
<<BLOCOPRINCIPAL>> --declaracao de label de escopo
DECLARE
V_NUM1 NUMBER := 100;
BEGIN
DECLARE
V_NUM1 NUMBER := 50;
BEGIN
DBMS_OUTPUT.PUT_LINE('Impressão 1 '||BLOCOPRINCIPAL.V_NUM1);
DBMS_OUTPUT.PUT_LINE('Impressão 2 '||V_NUM1);
END;
DBMS_OUTPUT.PUT_LINE('Impressão 3 '||V_NUM1);
END;
```
