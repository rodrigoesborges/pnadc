
<!-- README.md is generated from README.Rmd. Please edit that file -->

# pnadc

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
<!-- badges: end -->

O objetivo desse pacote é automatizar algumas análises feitas com os
microdados da PNAD Contínua.

> Ainda em fase MEGA-EXPERIMENTAL. A API VAI MUDAR

## Instalação

``` r
install.packages("pnadc")
```

## Como usar

O pacote foi pensado para que poassa ser usadao assim:

### Ler dados da PNAD Continua

``` r
library(pnadc)
# Vai baixar numa pasta "dados" na raiz do projeto.
# Isso não vai ser possível de alterar pelo pacote para dar uma 
# estrutura de trabalho homogênea e que possa ser confiada
download_pnad(2019, 4)

# Aqui ainda tem que pensar se vai deixar possível 
# mudar as variaveis que lê ou se travamos naquelas mais usadas
pnad2019_4 <- ler_pnad(2019, 4)
# Outra opção é não ter essa função e confiar/importar de PNADcIBGE
```

### Funções de utilidade

A PNAD é uma pesquisa estratificada e em geral é analisada usando o
pacote `survey`. Mas esse pacote é muito lento para realizar alguns
cálculos e principalemente para fazer análises exploratórias.

``` r
pnad2019_4 %>% 
  # Na verdade um contador respeitando os pesos
  proporcao(sexo)

# Deve funcionar com group_by
pnad2019_4 %>% 
  grou_by(regiao) %>% 
  proporcao(sexo)
```

O ideal era que essas funções de utilidade não se contivessem apenas a
dados relativos mas também fossem capazes de somar totais.

``` r
pnad2019_4 %>% 
  # Na verdade um somador respeitando os pesos e as projeções de pop
  total(sexo)

# Deve funcionar com group_by
pnad2019_4 %>% 
  grou_by(regiao) %>% 
  total(sexo)
```