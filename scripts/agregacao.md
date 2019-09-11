- AVG

```
select * from senso;
```

- AVG Retorna a média dos valores em um grupo. Valores nulos são ignorados

```
select AVG(populacao) as media from senso
where ano='2014';
```

- AVG MEDIA POR ESTADO

```

SELECT estado,AVG(POPULACAO) FROM senso
WHERE ANO='2014'
GROUP BY estado
ORDER BY 2 desc;
```

- AVG MEDIA POR ESTADO com sigla estado

```
SELECT a.cod_UF,b.sigla_uf,AVG(a.POPULACAO) media
FROM senso a
inner join uf b
on a.cod_UF=b.cod_uf
WHERE a.ano='2014'
GROUP BY a.cod_UF,b.sigla_uf
ORDER BY 3 desc;
```

- AVG MEDIA POR REGIAO

```
SELECT a.regiao,AVG(a.POPULACAO)
FROM senso a
WHERE a.ano='2014'
group by a.regiao
ORDER BY 2 DESC;
```

- MIN Retorna o valor mínimo na expressão.

```

select MIN(a.populacao) from senso a
WHERE a.ano='2014';
```

- MIN POR ESTADO

```
SELECT a.estado,MIN(a.POPULACAO)
FROM senso a
WHERE a.ano='2014'
GROUP BY estado;
```

- MIN POR REGIAO

```

SELECT a.regiao,MIN(POPULACAO)
FROM senso a
WHERE a.ano='2014'
GROUP BY a.regiao
ORDER BY 2;
```

- MAX Retorna o valor máximo na expressão

```
select MAX(populacao) from senso a
WHERE a.ano='2014';
```

- MAX POR ESTADO

```
SELECT a.estado,MAX(a.POPULACAO) FROM senso a
WHERE a.ano='2014'
GROUP BY a.estado
ORDER BY 2 desc;
```

- MAX POR SIGLA ESTADO

```
SELECT b.sigla_uf,MAX(a.POPULACAO)AS maximo
FROM senso a
INNER JOIN uf b
ON a.cod_uf=b.cod_uf
WHERE a.ano='2014'
GROUP BY b.sigla_uf
ORDER BY 2;
```

- SUM POR ESTADO

```

SELECT a.cod_uf,SUM(a.POPULACAO) FROM senso a
WHERE a.ano='2014'
GROUP BY a.cod_uf
ORDER BY 2 desc;
```

- SUM POR REGIAO

```
SELECT b.sigla_uf,sum(a.POPULACAO)AS maximo
FROM senso a
INNER JOIN uf b
ON a.cod_uf=b.cod_uf
WHERE a.ano='2014'
GROUP BY b.sigla_uf
ORDER BY 2;
```

- COUNT Retorna o número de itens de um grupo

```

select COUNT(*) from senso a
WHERE a.ano='2014';
```

- COUNT Retorna o número de cidades por ano

```
select a.ano,COUNT(*) qtd_cidades from senso a
group by a.ano
ORDER BY a.ano ASC;
```

-Descobrindo qtd estados

```
select count(distinct cod_uf) from senso;
```

- exemplo

```
select count(cod_uf) from senso;
```

- COUNT POR ESTADO

```
SELECT a.estado,COUNT(\*) FROM senso a
where ano='2014'
GROUP BY a.estado
ORDER BY 2 desc;
```

- COUNT POR REGIAO

```
SELECT a.regiao,COUNT(\*) FROM senso a
where ano='2014'
GROUP BY a.regiao
ORDER BY 2 desc;
```

- Usando varias funçoes de agregacao

```

select avg(a.populacao)media_pop,
min(a.populacao)minimo_pop,
max(a.populacao)maximo_pop,
sum(a.populacao)total_pop,
COUNT(\*) qtd_cidades
from senso a
where a.ano='2014';
```

- POR ESTADO

```
SELECT a.estado,
avg(a.populacao)media_pop,
min(a.populacao)minimo_pop,
max(a.populacao)maximo_pop,
sum(a.populacao)total_pop,
COUNT(\*) qtd_cidades
FROM senso a
where a.ano='2014'
GROUP BY a.estado
ORDER BY 2 desc;
```

- Apresentar nome da cidade com maior populacao de cada estados

```
select a.estado,a.nome_mun,a.populacao
from
(
select b.estado, MAX(b.populacao) as populacao from senso b
where b.ano='2014'
group by b.estado
) b
join senso a
on a.estado = b.estado
and a.populacao = b.populacao
where a.ano='2014'
order by a.populacao desc;
```

- Apresentar nome da cidade com maior populacao de cada estados

```
select a.estado,a.nome_mun,a.populacao
from
(
select b.estado, min(b.populacao) as populacao from senso b
where b.ano='2014'
group by b.estado
) b
join senso a
on a.estado = b.estado
and a.populacao = b.populacao
where a.ano='2014'
order by a.populacao desc;
```

- Apresentar nome da cidade com minimo populacao de cada estados

```
select a.estado,a.nome_mun,a.populacao
from
(
select b.estado, MIN(b.populacao) as populacao from senso b
where b.ano='2014'
group by b.estado
) b
join senso a
on a.estado = b.estado
and a.populacao = b.populacao
where a.ano='2014'
order by a.populacao desc;
```

- STDDEV Retorna o desvio padrão estatístico de todos os valores da expressão
  especificada

```
select STDDEV(a.populacao) from senso a
where a.ano='2014';
```

-- STDDEV_POP Retorna o desvio padrão estatístico para a população de todos os

```
select STDDEV_POP(populacao) from senso;
```

- COMPARANDO CRESCIMENTO pop DA CIDADES ref anos 2010 a 2014

```
SELECT a.nome_mun,
a.populacao as senso_2010,
b.populacao as senso_2014,
(100/a.populacao)\*(b.populacao)-100 as percentual
from senso a
inner join senso b
on a.cod_mun=b.cod_mun
where a.ano='2010'
and b.ano='2014';
```

- COMPARANDO CRESCIMENTO POPULACAO POR ESTADO ref anos 2010 a 2014

```

SELECT a.estado,
sum(a.populacao) as senso_2010,
sum(b.populacao) as senso_2014,
(100/sum(a.populacao))\*(sum(b.populacao))-100 as percentual
from senso a
inner join senso b
on a.cod_mun=b.cod_mun
where a.ano='2010'
and b.ano='2014'
group by a.estado;
```

- VAR_POP Retorna a variância estatística de todos os valores da expressão especificada

```
SELECT VAR_POP(POPULACAO) FROM senso
where ano='2014';
```

- VAR_POP COM GROUP BY

```
SELECT estado,VAR_POP(POPULACAO) FROM senso
GROUP BY estado;
```

- VAR_SAMP Retorna a variância estatística para o preenchimento

```
SELECT VAR_SAMP(POPULACAO) FROM senso;
```

- VAR_SAMP COM GROUP BY

```
SELECT estado,VAR_SAMP(POPULACAO) FROM senso
GROUP BY estado;
```

- GROUP BY WITH ROLLUP

```

SELECT a.estado,COUNT(*) FROM senso a
where ano='2014'
GROUP BY rollup(a.estado);
```

- GROUP BY WITH ROLLUP

```
SELECT a.estado,a.REGIAO,sum(a.POPULACAO) FROM senso a
where ano='2014'
GROUP BY rollup(a.estado,a.REGIAO);
```
