---
title: "Seeking Help"
teaching: 10
exercises: 10
questions:
- "How can I get help in R?"
objectives:
- "To be able read R help files for functions and special operators."
- "To be able to use CRAN task views to identify packages to solve a problem."
- "To be able to seek help from your peers."
keypoints:
- "Use `help()` to get online help in R."
---





## Lendo arquivos de ajuda
R, e todo pacote, fornece arquivos de ajuda para funções. Para procurar ajuda sobre uma função de uma função específica que está em um pacote carregado no seu namespace (sua seção interativa do R):


~~~
?function_name
help(function_name)
~~~
{: .r}

Isso irá carregar uma página de ajuda no RStudio (ou um texto no próprio R).

Cada página de ajuda é dividida nas seções:

 - Description: Uma descrição estendida sobre o que a função faz.
 - Usage: Os argumentos da função e seus valores padrões.
 - Arguments: Uma explicação dos dados que cada argumento espera receber.
 - Details: Qualquer detalhe importante para estar atento.
 - Values: Os dados que a função retorna.
 - See Also: Qualquer função relacionada você pode achar útil.
 - Examples: Alguns exemplos sobre como usar a função.

Diferentes funções podem ter diferentes seções, mas essas são as principais para se prestar atenção.

> ## Dica: Lendo arquivos de ajuda
>
> Um dos aspectos mais assustadores do R é seu imenso número de funções disponíveis. 
> Seria improvável, se não impossível, lembrar corretamente como utilizar cada função
> você utiliza. Felizmente, os arquivos de ajuda existem para que você não precise 
> fazer isso!
{: .callout}

## Operadores Especiais
Para procurar ajuda sobre operadores especiais, use os termos:


~~~
?"+"
~~~
{: .r}

## Conseguindo ajuda sobre pacotes

Muitos pacotes vem com “vignettes”: tutoriais e exemplos de documentações estendidos. Sem qualquer argumento, `vignette()` listará todas vignettes para todos pacotes instalados; `vignette(package="package-name")` listará todas as vignettes disponíveis para `package-name`, e `vignette("vignette-name")` abrirá a vignette especificada.

Se um pacote não possui vignettes alguma, você geralmente pode achar ajuda digitando `help("package-name")`.

## Quando você meio que lembra a função

Se você não tem certeza em qual pacote uma certa função está, ou como ela é especificamente escrita você pode fazer uma busca fuzzy:


~~~
??function_name
~~~
{: .r}

## Quando você não tem ideia por onde começar

Se você não sabe qual pacote ou função você precisa, a lista de tópicos do CRAN ([CRAN Task Views](https://cran.r-project.org/web/views/)) é uma lista especialmente mantida de pacotes agrupados em áreas. Esse pode ser um bom ponto de partida.

## Quando o seu código não funciona: procurando ajuda com outras pessoas

Se você está tendo trabalho usando alguma função, em  90% das vezes, a resposta que você procura já foi respondida em [Stack Overflow](http://stackoverflow.com/). Você pode procurar usando o campo [r].

Se você não consegue encontrar a resposta, existem algumas funções úteis para ajudá-lo a tirar sua dúvida com outras pessoas:


~~~
?dput
~~~
{: .r}

Irá retornar o banco de dados com o qual você está trabalhando em um formato que ele possa ser copiado e colado por qualquer um em suas sessões em R.


~~~
sessionInfo()
~~~
{: .r}



~~~
R version 3.3.0 (2016-05-03)
Platform: x86_64-apple-darwin13.4.0 (64-bit)
Running under: OS X 10.11.6 (El Capitan)

locale:
[1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8

attached base packages:
[1] stats     graphics  grDevices utils     datasets  base     

other attached packages:
[1] checkpoint_0.3.18 stringr_1.2.0     knitr_1.15.1     

loaded via a namespace (and not attached):
[1] magrittr_1.5  tools_3.3.0   stringi_1.1.2 methods_3.3.0 evaluate_0.10
~~~
{: .output}

Irá imprimir a sua atual versão do R, bem como os pacotes que você tem carregados. Isso pode ser útil para ajudar outras pessoas a reproduzirem e corrigirem seus problemas.

> ## Desafio 1
>
> Olhe a ajuda da função `c()`. Que tipo de vetor você espera criar se você usar os
> seguintes comandos:
> 
> ~~~
> c(1, 2, 3)
> c('d', 'e', 'f')
> c(1, 2, 'f')
> ~~~
> {: .r}
> > ## Solução do desafio 1
> >

> > A função `c()` cria um vetor, no qual todos elementos são do mesmo tipo. No
> > primeiro caso, os elementos são numéricos, no segundo, eles são caracteres, e no
> > terceiro eles são caracteres: os valores numéricos foram "forçados" a serem
> > caracteres.
> {: .solution}
{: .challenge}

> ## Desafio 2
>
> Olhe a ajuda para a função `paste`. Você precisará dela mais adiante. Qual a
> diferença entre os argumentos `sep` e `collapse`?
>
> > ## Solução do desafio 2
> >
> > Para ver a ajuda da função `paste()`, use:
> > 
> > ~~~
> > help("paste")
> > ?paste
> > ~~~
> > {: .r}
> > A diferença entre `sep` e `collapse` é um pouco
> > delicada. O argumento `sep` especifica qual separador de caractere deve ser usado
> > quando você passa vários *argumentos* diferentes para `paste()`,
> > e.g. `paste('a', 'b', sep=',')`. Por outro lado, `collapse` especifica
> > qual separador de caracteres deve ser usado quando um conjunto de strings é  
> > combinado, quando todos são especificados como partes do mesmo *vetor*,
> > e.g. `paste(c('a','b'), collapse=',')`. (Para mais informações,
> > vá para o final da página de ajuda da função `?paste` e veja os
> > exemplos, ou tente `example('paste')`.)
> {: .solution}
{: .challenge}

> ## Desafio 3
> Use a função help para achar a função (e seus parâmetros associados) que pode ser
> usada para carregar dados de um arquivo csv no qual as colunas são delimitadas com
> "\t" (tab) e decimais são pontos “.”. Essa verificação para separadores decimais é
> importante, especialmente se você está trabalhando com colaboradores internacionais,
> porque países diferentes possuem diferentes convenções para o ponto decimal (isto é,
> vírgula ou ponto). Dica: use ??csv para buscar funções relacionadas com csv.
> > ## Solução do desafio 3
> >
> > A função padrão em R para ler arquivos delimitados por tab com um ponto  
> > como separador decimal é read.delim(). Você pode também fazer isso com
> > `read.table(file, sep="\t")` (o ponto é o separador decimal *default*
> > para `read.table()`, embora você possa mudar o argumento 
> > `comment.char` também se seus dados contém
> > caracteres hash (#)
> {: solution}
{: .challenge}

## Outras opções de ajuda

* [Quick R](http://www.statmethods.net/)
* [RStudio cheat sheets](http://www.rstudio.com/resources/cheatsheets/)
* [Cookbook for R](http://www.cookbook-r.com/)
