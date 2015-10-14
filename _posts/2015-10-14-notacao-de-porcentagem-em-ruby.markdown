---
layout: post
title:  "Notação de '%' em Ruby"
date:   2015-10-14 00:00:00
comments: true
---

Uma das coisas mais legais de começar a programar em Ruby é ir percebendo, com o passar do tempo, as particularidades da linguagem. Uma de suas características mais interessantes, a meu ver, é a quantidade de pequenas features que servem para simplificar a vida do programador, ou mesmo para diminuir a quantidade de código necessário para fazer coisas simples.

Um exemplo bastante conhecido do que eu mencionei é a [sintaxe de hash introduzida no Ruby 1.9](http://ruby-doc.org/core-2.2.3/Hash.html). É um detalhe pequeno, mas que torna uma coisa corriqueira como a criação de um hash tendo símbolos como chaves algo mais prático. Outra feature bastante conhecida é a **notação de porcentagem ("%")**.

O exemplo mais conhecido dessa notação é o `%w`, utilizado para a criação de arrays de palavras. Onde isso:

{% highlight ruby %}
%w(one two three four)
#=> ["one", "two", "three", "four"]
{% endhighlight %}

É equivalente a isso:

{% highlight ruby %}
["one", "two", "three", "four"]
#=> ["one", "two", "three", "four"]
{% endhighlight %}

Porém, além deste exemplo, existem outros delimitadores para facilitar nossa vida em diferentes. São os seguintes:

### %q
O primeiro, e mais simples, é o `%q`, utilizado para criar strings sem interpolação. Sua contraparte maiúscula `%Q`, que pode ser substituída por `%`, aceita interpolação.

{% highlight ruby %}
animal = 'dog'
p %q[The quick brown fox jumps over the lazy #{animal}]
p %Q[The quick brown fox jumps over the lazy #{animal}]
p %[The quick brown fox jumps over the lazy #{animal}]

#=> "The quick brown fox jumps over the lazy \#{animal}"
#=> "The quick brown fox jumps over the lazy dog"
#=> "The quick brown fox jumps over the lazy dog"
{% endhighlight %}

### %w
É a já mencionada notação para criação de arrays de palavras. Assim como no caso anterior, apenas a versão maiúscula `%W` aceita interpolação.

### %r
Esta notação é utilizada para a criação de [expressões regulares](http://ruby-doc.org/core-2.2.3/Regexp.html). Algo importante a ser dito é que, ao contrário dos casos anteriores, esta notação aceita interpolação e **não possui** versão maiúscula.

{% highlight ruby %}
animal = 'dog'
p %r{mice|cat|#{animal}}
#=> /mice|cat|dog/
{% endhighlight %}

### %s
Esta notação é utilizada para criar [símbolos](http://ruby-doc.org/core-2.2.3/Symbol.html). Ela também não possui contraparte maiúscula, porém **não aceita** interpolação.

{% highlight ruby %}
animal = 'dog'
p %s!animal!
p %s!#{animal}!
#=> :animal
#=> :"\#{animal}"
{% endhighlight %}

### %i
Esta expressão literal foi implementada no Ruby 2.0 e é bem similar ao `%w`, porém cria um array de **símbolos**. Do mesmo modo que o `%w`, possui uma versão maiúscula que aceita interpolação.

{% highlight ruby %}
animal = 'dog'
p %i<cat rat #{animal}>
p %I<cat rat #{animal}>
#=> [:cat, :rat, :"\#{animal}"]
#=> [:cat, :rat, :dog]
{% endhighlight %}

### %x
A última expressão da lista é a `%x`, que cria um comando de shell. Tal qual o `%r`, este delimitador não possui versão maiúscula e aceita interpolação.

{% highlight ruby %}
p %x|echo #{ 2 + 3 }|
#=> "5\n"
{% endhighlight %}

### Delimitadores

Note que em cada exemplo utilizei um tipo de caractere diferente para delimitar a expressão. Fiz isso propositadamente para demonstrar que a esta notação aceita qualquer caractere que não seja alfanumérico ou multibyte como delimitador. Se para abrir a expressão se usa `(`, `[`, `{` ou `<` o delimitador para fechar a expressão será o caractere de fechamento correspondente (`)`, `]`, `}` e `>` respectivamente). Caso seja usado algum outro caractere válido (como nos casos que usei `|` e `!`), então o delimitador final será o mesmo caractere que iniciou a expressão.

Achou o post útil? Achou algum erro no conteúdo? Quer falar sobre a Vida, o Universo e Tudo Mais? Deixe seu feedback nos comentários e até o próximo post.