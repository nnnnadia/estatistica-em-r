## 1 CONHECENDO OS DADOS

### 1.1 Dataset do projeto

> `[ ]: sessionInfo()`

---

> `[ ]: library()`

> `[ ]: library(dplyr)`

---

> `[ ]: ??select`

> `[ ]: ??arrange`

---

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

---

> `[ ]: library(glue)`

> `[ ]: glue('De {min(dados$Idade)} até {max(dados$Idade)} anos')`

##### Variáveis quantitativas contínuas
> `[ ]: glue('De {min(dados$Altura)} até {max(dados$Altura)} metros')`

![Esquema de classificação de uma variável](https://caelum-online-public.s3.amazonaws.com/1177-estatistica-parte1/01/img001.png)

## 2 DISTRIBUIÇÃO DE FREQUÊNCIAS

### 2.1 Distribuição de frequências para variáveis qualitativas

##### Método 1
> `[ ]: table(dados$Sexo)`

> `[ ]: prop.table(table(dados$Sexo)) * 100`

> `[ ]: dist_freq_qualitativas <- cbind(freq = table(dados$Sexo), percent = prop.table(table(dados$Sexo)) * 100)`

> `[ ]: colnames(dist_freq_qualitativas) <- c('Frequência', 'Porcentagem (%)')`

> `[ ]: rownames(dist_freq_qualitativas) <- c('Masculino', 'Feminino')`

> `[ ]: dist_freq_qualitativas`


##### Método 2
> `[ ]: frequencia <- table(dados$Sexo, dados$Cor)`

> `[ ]: rownames(frequencia) <- c('Masculino', 'Feminino')`

> `[ ]: colnames(frequencia) <- c('Indígena', 'Branca', 'Preta', 'Amarela', 'Parda')`

> `[ ]: frequencia <- cbind(frequencia)`

> `[ ]: frequencia`

---

> `[ ]: percentual <- prop.table(frequencia) * 100`

> `[ ]: percentual`

---

> `[ ]: list(c(1, 2, 3, 4), c(5, 6, 7))`

> `[ ]: medias <- tapply(dados$Renda, list(dados$Sexo, dados$Cor), mean)`

> `[ ]: rownames(medias) <- c('Masculino', 'Feminino')`

> `[ ]: colnames(medias) <- c('Indígena', 'Branca', 'Preta', 'Amarela', 'Parda')`

> `[ ]: medias`

### 2.2 Distribuição de frequências para variáveis quantitativas (classes personalizadas)

~~~r
[ ]:  min(dados$Renda)
~~~

~~~r
[ ]:  max(dados$Renda)
~~~

~~~r
[ ]:  classes <- c(0, 1576, 3152, 7880, 15760, 200000)
~~~

~~~r
[ ]:  labels <- c('E', 'D', 'C', 'B', 'A')
~~~

~~~r
[ ]:  frequencia <- table(
      cut(
        x = dados$Renda,
        breaks = classes,
        labels = labels,
        include.lowest = TRUE
      )
    )

    frequencia
~~~

~~~r
[ ]:  percentual <- prop.table(frequencia) * 100

      percentual
~~~

~~~r
[ ]:  dist_freq_quantitativas_2 <- cbind(
        'Frequência' = frequencia,
        'Porcentagem (%)' = percentual
      )
      dist_freq_quantitativas_2
~~~

~~~r
[ ]:  dist_freq_quantitativas_2[
        order(row.names(dist_freq_quantitativas_2)),
      ]
~~~

### 2.3 Distribuição de frequências para variáveis quantitativas (classes de amplitude fixa)

##### Passo 1 - Definindo o número de classes

~~~r
[ ]:  n <- nrow(dados)
      n
~~~

~~~r
[ ]:  k <- 1 + (10 / 3) * log10(n)
      k
~~~

~~~r
[ ]:  k <- round(k)
      k
~~~

##### Passo 2 - Criar a tabela de frequências
~~~r
[ ]:  labels <- c(
        '      0.00 |—|  11,764.70', 
        ' 11,764.70  —|  23,529.40', 
        ' 23,529.40  —|  35,294.10', 
        ' 35,294.10  —|  47,058.80', 
        ' 47,058.80  —|  58,823.50', 
        ' 58,823.50  —|  70,588.20', 
        ' 70,588.20  —|  82,352.90', 
        ' 82,352.90  —|  94,117.60', 
        ' 94,117.60  —| 105,882.00', 
        '105,882.00  —| 117,647.00', 
        '117,647.00  —| 129,412.00', 
        '129,412.00  —| 141,176.00', 
        '141,176.00  —| 152,941.00', 
        '152,941.00  —| 164,706.00', 
        '164,706.00  —| 176,471.00', 
        '176,471.00  —| 188,235.00', 
        '188,235.00  —| 200,000.00'
      )
~~~

~~~r
[ ]:  frequencia <- table(
        cut(
          x = dados$Renda,
          breaks = k,
          labels = labels,
          include.lowest = TRUE
        )
      )
      frequencia
~~~

~~~r
[ ]:  percentual <- prop.table(frequencia) * 100
      percentual
~~~

~~~r
[ ]:  dist_freq_quantitativas_3 <- cbind(
        'Frequência' = frequencia,
        'Porcentagem (%)' = percentual
      )
      dist_freq_quantitativas_3
~~~

### Histograma

~~~r
[ ]:  options(repr.plot.width = 7, repr.plot.height = 4)
~~~

~~~r
[ ]:  hist(dados$Altura)
~~~

~~~r
[ ]:  hist(
        x = dados$Altura,
        breaks = 'Sturges',
        col = 'lightblue',
        main = 'Histograma das Alturas',
        xlab = 'Altura',
        ylab = 'Frequências',
        prob = TRUE,
        las = 1
      )
~~~

---

~~~r
[ ]:  library(ggplot2)
~~~

~~~r
[ ]:  ggplot(dados, aes(x = Altura)) + 
        geom_histogram(binwidth = 0.02, color = "black", alpha = 0.9) + 
        ylab("Frequência") + 
        xlab("Alturas") + 
        ggtitle('Histograma das Alturas') +
        theme(
          plot.title = element_text(size = 14, hjust = 0.5),
          axis.title.y = element_text(size = 12, vjust = +0.2),
          axis.title.x = element_text(size = 12, vjust = -0.2),
          axis.text.y = element_text(size = 10),
          axis.text.x = element_text(size = 10)
        )
~~~

~~~r
[ ]:  formatos <- theme(
        plot.title = element_text(size = 14, hjust = 0.5),
        axis.title.y = element_text(size = 12, vjust = +0.2),
        axis.title.x = element_text(size = 12, vjust = -0.2),
        axis.text.y = element_text(size = 10),
        axis.text.x = element_text(size = 10)
      )
~~~

~~~r
[ ]:  ggplot(dados, aes(x = Altura, y = ..density..)) + 
        geom_histogram(binwidth = 0.02, color = "black", alpha = 0.9) + 
        geom_density(color = 'green') +
        ylab("Frequência") + 
        xlab("Alturas") + 
        ggtitle('Histograma das Alturas') +
        formatos
~~~

---

~~~r
[ ]:  bar_chart <- data.frame(dist_freq_quantitativas_2)

      bar_chart
~~~

~~~r
[ ]:  ggplot(bar_chart, aes(x = row.names(bar_chart), y = `Frequência`)) + 
        geom_bar(stat = "identity") + 
        ylab("Frequência") + 
        xlab("Classes de Renda") + 
        ggtitle('Gráfico Classes de Renda') +
        formatos
~~~