---
layout: post
title:  "Aleatoriedade e Método srand"
date:   2015-08-28 00:30:00
categories: ruby aleatoriedade
comments: true
---

Há alguns dias, programando um [projeto pessoal simples](https://github.com/ruan-brandao/lizard-spock), tive que utilizar números aleatórios. E pesquisando sobre técnicas para testar aleatoriedade me deparei com o método [Kernel#srand](http://ruby-doc.org/core-2.2.3/Kernel.html#method-i-srand). Depois de um pouco de pesquisa, aprendi um pouco sobre como este método funciona.

Antes de explicar o método, vale pontuar algumas coisas sobre aleatoriedade e computadores. Uma das particularidades sobre o tema é que computadores (neste caso especificamente softwares) são incapazes de gerar sequências de números realmente aleatórias. A causa disso, basicamente, é o fato de computadores serem dispositivos determinísticos. Computadores são projetados de modo que rodando o mesmo algoritmo com a mesma entrada de dados cem mil vezes, todas as cem mil execuções devem retornar o mesmo resultado. E, por terem esta natureza determinística, computadores são incapazes de gerar sequências realmente aleatórias.

De modo geral computadores utilizam a seguinte estratégia para gerar números aleatórios:

 - Primeiro, geram um número de seed com base em dados que mudam constantemente como a hora e data atual e ID do processo. 
 - Depois, executam algum algoritmo sobre esse número e, com base neste seed, geram uma sequência de números.

Deste modo, mesmo gerando um número aleatório agora e outro 1 mulissegundo depois, o seed dos dois números será diferente. Assim são gerados números pseudoaleatórios. Números que parecem aleatórios, mas com uma amostra suficientemente grande é possível deduzir qual o próximo número da sequência.

Esta técnica é usada pelo método `rand()` do Ruby. Ele gera um seed novo e o utiliza para gerar uma sequência aleatória de números. E aí entra o método `srand()`. Este método aceita um parâmetro que será utilizado como seed para as gerações de números aleatórios, de modo que o método `rand()` tenha resultados previsíveis. Veja a seguinte demonstração:

{% highlight ruby %}
# Defini o seed como o número 123456
# O método srand me retornou o seed anterior
srand 123456
#=> 218335731078242048432893517997246340016

# Gerei alguns números com base neste seed
[rand, rand, rand]
#=> [0.12696983303810094, 0.966717838482003, 0.26047600586578334]

# Após isso, gerei mais algumas sequências com um seed definido pelo sistema
srand Random.new.seed
#=> 123456
[rand, rand, rand]
#=> [0.6171675580512942, 0.7188160648009547, 0.7563867151524197]
[rand, rand, rand]
#=> [0.32110833704933495, 0.17344055724987273, 0.8876076933859104]
[rand, rand, rand]
#=> [0.23327701614357432, 0.028948756960376132, 0.2978036805728924]

# Agora defino novamente o seed e gero outra sequência, idêntica à primeira
srand 123456
#=> 78381360086382847667411094511927992950
[rand, rand, rand]
#=> [0.12696983303810094, 0.966717838482003, 0.26047600586578334]
{% endhighlight %}

Note que a última sequência gerada (logo após redefinir o seed) é idêntica à primeira, pois nos dois casos o seed utilizado para a geração dos números foi o mesmo.

### PS*
Há equipamentos de hardware que conseguem, com base na observação de acontecimentos físicos, gerar sequencias realmente aleatórias. Porém, para o tópico preferi focar nas características de software.
