## 1 CONHECENDO OS DADOS

### 1.1 Dataset do projeto

> `[ ]: sessionInfo()`

> `[ ]: library()`

> `[ ]: library(dplyr)`

> `[ ]: ??select`

> `[ ]: ??arrange`

> `[ ]: dados <- read.csv("dados.csv")`

> `[ ]: dados`

> `[ ]: head(dados, 5)`

### 1.2 Tipos de dados

> 'Em estatística temos duas grandes classificações de variáveis: as qualitativas ou
> categóricas, que são as variáveis que nomeiam os indivíduos. As quantitativas são as
> contagens e mensurações.'

##### Variáveis qualitativas ordinais
> `[ ]: head(dados, 5)`

> `[ ]: select(dados, Anos.de.Estudo)`

> `[ ]: unique(select(dados, Anos.de.Estudo))`

> `[ ]: arrange(unique(select(dados, Anos.de.Estudo)), Anos.de.Estudo)`

> `[ ]: c(arrange(unique(select(dados, Anos.de.Estudo)), Anos.de.Estudo))`

##### Variáveis qualitativas nominais
> `[ ]: c(arrange(unique(select(dados, UF)), UF))`

> `[ ]: c(arrange(unique(select(dados, Sexo)), Sexo))`

> `[ ]: c(arrange(unique(select(dados, Cor)), Cor))`

##### Variáveis quantitativas discretas
> `[ ]: sprintf('De %s até %s anos', min(dados$Idade), max(dados$Idade))`

> `[ ]: library(glue)`

> `[ ]: glue('De {min(dados$Idade)} até {max(dados$Idade)} anos')`

##### Variáveis quantitativas contínuas
> `[ ]: glue('De {min(dados$Altura)} até {max(dados$Altura)} metros')`

![Esquema de classificação de uma variável](https://caelum-online-public.s3.amazonaws.com/1177-estatistica-parte1/01/img001.png)