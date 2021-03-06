- PROCEDURE PARA COPIA DE MATERIAL

```
CREATE OR REPLACE PROCEDURE PROC_COPIA_MAT (V_EMP_DE IN NUMBER,
                                            V_EMP_PARA IN NUMBER,
                                            V_MAT IN NUMBER)
                IS
    --EXCESSOES
    V_EXECPT_EMP_DE EXCEPTION;
    V_EXECPT_EMP_PARA EXCEPTION;
    V_EXECPT_EMP_MAT_DE EXCEPTION;
    V_EXECPT_EMP_MAT_PARA EXCEPTION;
    --VARIAVES DE APOIO CONTROLE
    V_CONT_EMP_DE NUMBER;
    V_CONT_EMP_PARA NUMBER;
    V_CONT_EMP_MAT_DE NUMBER;
    V_CONT_EMP_MAT_PARA NUMBER;

 BEGIN
    --VERIFICA SE EMPRESA ORIGEM EXISTE (DE)
    SELECT COUNT(*) QTD INTO V_CONT_EMP_DE FROM EMPRESA WHERE COD_EMPRESA=V_EMP_DE;
    IF (V_CONT_EMP_DE=0) THEN
        RAISE V_EXECPT_EMP_DE;
    END IF;

       --VERIFICA SE EMPRESA DESTINO EXISTE (PARA)
    SELECT COUNT(*) QTD INTO V_CONT_EMP_PARA FROM EMPRESA WHERE COD_EMPRESA=V_EMP_PARA;
    IF (V_CONT_EMP_PARA=0) THEN
        RAISE V_EXECPT_EMP_PARA;
    END IF;

     --VERIFICA SE MATERIAL ORIGEM EXISTE
    SELECT COUNT(*) QTD INTO V_CONT_EMP_MAT_DE FROM MATERIAL WHERE COD_EMPRESA=V_EMP_DE AND COD_MAT=V_MAT;
    IF (V_CONT_EMP_MAT_DE=0) THEN
        RAISE V_EXECPT_EMP_MAT_DE;
    END IF;

         --VERIFICA SE MATERIAL DESTINO EXISTE
    SELECT COUNT(*) QTD INTO V_CONT_EMP_MAT_PARA FROM MATERIAL WHERE COD_EMPRESA=V_EMP_PARA AND COD_MAT=V_MAT;
    IF (V_CONT_EMP_MAT_PARA=1) THEN
        RAISE V_EXECPT_EMP_MAT_PARA;
    END IF;


    INSERT INTO MATERIAL
    SELECT V_EMP_PARA,COD_MAT,DESCRICAO,PRECO_UNIT,COD_TIP_MAT FROM MATERIAL
    WHERE COD_MAT=V_MAT AND COD_EMPRESA=V_EMP_DE;

    COMMIT;
    DBMS_OUTPUT.PUT_LINE('COPIA REALIZADA COM SUCESSO!');

 EXCEPTION
 WHEN V_EXECPT_EMP_DE THEN
      DBMS_OUTPUT.PUT_LINE('ATEN플O! EMPRESA ORIGEM NAO EXISTE');

 WHEN V_EXECPT_EMP_PARA THEN
      DBMS_OUTPUT.PUT_LINE('ATEN플O! EMPRESA DESTINO NAO EXISTE');

 WHEN V_EXECPT_EMP_MAT_DE THEN
      DBMS_OUTPUT.PUT_LINE('ATEN플O! MATERIAL NAO EXISTE NA EMPRESA ORIGEM');

  WHEN V_EXECPT_EMP_MAT_PARA THEN
       --RAISE_APPLICATION_ERROR(-20999,'ATEN플O! MATERIAL JA EXISTE NA EMPRESA DESTINO', FALSE);
       DBMS_OUTPUT.PUT_LINE('ATEN플O! MATERIAL JA EXISTE NA EMPRESA DESTINO');

 WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('OCORREU UM ERRO - '||SQLCODE||' -ERROR- '||SQLERRM);

END;
```

- EXECUTANDO PREOCEDURE

```
SET SERVEROUTPUT ON


EXECUTE PROC_COPIA_MAT (1,2,1);
EXECUTE PROC_COPIA_MAT (1,2,2);

SELECT * FROM MATERIAL;
```

- PROCEDURE ORDEM_PROD (OBJETIVO GERAR ORDENS DE PRODUCAO DE ACORDO COM DEMANDA DE VENDAS POR EMPRESA)

```
CREATE OR REPLACE PROCEDURE PROC_PLAN_ORDEM (P_EMP NUMBER,
                                             P_MES  VARCHAR2,
                                             P_ANO  VARCHAR2)
IS
  V_EXCEPT_EXISTE_PEDIDO EXCEPTION;
  V_CONTA_PED NUMBER;
 BEGIN

 --VERIFICANDO SE EXISTE PEDIDOS ABERTO PARA MES E ANO SELECIONADO
    SELECT COUNT(*) QTD INTO V_CONTA_PED
	FROM PED_VENDAS A
	INNER JOIN PED_VENDAS_ITENS B
	ON A.NUM_PEDIDO=B.NUM_PEDIDO
    AND A.COD_EMPRESA=B.COD_EMPRESA
	WHERE A.SITUACAO='A' --ABERTO
    AND A.COD_EMPRESA=P_EMP
	AND TO_CHAR(A.DATA_ENTREGA,'MM')=P_MES
    AND TO_CHAR(A.DATA_ENTREGA,'YYYY')=P_ANO;

    --SE FOR IGUAL NAO ZERO NAO TEM E TERMINA
    IF V_CONTA_PED=0
	THEN
		RAISE V_EXCEPT_EXISTE_PEDIDO;
	END IF;


    --SELECIONANDO PEDIDOS PARA GERAR ORDENS DE PRODUÇÃO DE ACORDO COM A DEMANDA.
			INSERT INTO ORDEM_PROD
			SELECT A.COD_EMPRESA,
                   NULL,
                   B.COD_MAT,
                   SUM(B.QTD) AS QTD_PLAN,
                   0 QTD_PROD,
			       '01/'||P_MES||'/'||P_ANO AS DATA_INI,
                   LAST_DAY('01/'||P_MES||'/'||P_ANO) AS DATA_FIM,
                   'A'
			FROM PED_VENDAS A
				INNER JOIN PED_VENDAS_ITENS B
				ON A.NUM_PEDIDO=B.NUM_PEDIDO
                AND  A.COD_EMPRESA=B.COD_EMPRESA
				WHERE A.COD_EMPRESA=P_EMP
				AND TO_CHAR(A.DATA_ENTREGA,'MM')=P_MES
                AND TO_CHAR(A.DATA_ENTREGA,'YYYY')=P_ANO
                AND A.SITUACAO='A' --APENAS PEDIDO EM ABERTO
				GROUP BY A.COD_EMPRESA, B.COD_MAT, NULL, 0, '01/'||P_MES||'/'||P_ANO,
                LAST_DAY('01/'||P_MES||'/'||P_ANO), 'A';

               DBMS_OUTPUT.PUT_LINE('INSERT ORDEM PROD REALIZADO');

                --ATUALIZA STATUS PEDIDO DE A PARA P
               UPDATE PED_VENDAS  SET SITUACAO='P'
               WHERE COD_EMPRESA=P_EMP
               AND TO_CHAR(DATA_ENTREGA,'MM')=P_MES
               AND TO_CHAR(DATA_ENTREGA,'YYYY')=P_ANO
               AND SITUACAO='A';

               DBMS_OUTPUT.PUT_LINE('STATUS ATUALIZADO DE ABERTO PARA PLANEJADO');

 EXCEPTION
 WHEN V_EXCEPT_EXISTE_PEDIDO THEN
      DBMS_OUTPUT.PUT_LINE('ATENÇÃO! NAO EXISTE PEDIDOS ABERTO PARA PLANEJAMENTO!');

  WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('OCORREU UM ERRO - '||SQLCODE||' -ERROR- '||SQLERRM);

END;

EXECUTE PROC_PLAN_ORDEM (1,'01','2018');
EXECUTE PROC_PLAN_ORDEM (1,'02','2018');
EXECUTE PROC_PLAN_ORDEM (2,'03','2018');
EXECUTE PROC_PLAN_ORDEM (1,'04','2018');
```
