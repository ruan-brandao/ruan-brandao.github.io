---
layout: post
title:  "Como fazer bons commits no Git"
date:   2020-02-04 21:15:00
tags:   Git
image: paper-pencil.jpg
image-description: Lápis apoiado sobre um bloco de notas
image-author: Jan Kahánek
image-author-link: https://unsplash.com/@honza_kahanek?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge
comments: true
---

Git é uma ferramenta muito importante para se desenvolver software de qualidade hoje em dia e seu uso se tornou
um padrão bastante difundido na indústria. Ele tem diversas funcionalidades que facilitam nossa vida no
dia a dia fazendo código, e uma das principais funcionalidades oferecidas é a de **commits**.

Git é uma importante ferramenta de **documentação**. O histórico de commits de um projeto é um ótimo lugar para acompanhar como o código e o software em si evoluíram ao longo do tempo. Ter isso à disposição é bastante útil em diversos casos.

Nesse texto você vai conhecer melhar essa funcionalidade de Git e ver boas práticas de como utilizá-la.

# O que é um commit e pra que ele serve

Git é uma ferramenta de controle de versão. Ou seja, é uma ferramenta que serve para controlar um projeto de software e as mudanças que ocorrem neste projeto ao longo do tempo, e o commit é a peça fundamental para isso.

Um commit serve como um **ponto de retorno** no projeto. O Git possui ferramentas que possibilitam acessar o projeto exatamente como ele estava quando cada commit foi feito. Isso traz várias vantagens, como dar mais segurança para fazer modificações no sistema (afinal, se a mudança estiver incorreta, é possível reverter o commit e voltar o  código do projeto para como ele estava antes do commit ser feito) ou facilitar na correção de bugs, pois é possível executar o projeto localmente em um commit anterior à introdução de algum bug específico no código.

Isso mostra como Git é uma ferramenta importantíssima de **documentação** em um projeto de software. Precisa ver quando uma funcionalidade foi incluída no projeto, ou quando foi realizada a migração de uma biblioteca externa para uma biblioteca própria? O histórico de commits do projeto está lá para ajudar.

Porém, para colher esses benefícios, é necessário que o projeto tenha um bom histórico de commits. Essas são algumas dicas para fazer bons commits que ajude a pessoa que precise mexer no código em algum momento do futuro.

## Como fazer um commit

Fazer um commit tem dois passos principais: escolher quais mudanças serão incluídas no commit e criar o commit em si.

Você pode utilizar comando `git status` para checar quais arquivos foram alterados no projeto desde o último commit.

```
On branch my-branch-name
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html
	modified:   index.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	images/my-image.png
```

Sabendo quais arquivos foram modificados, você pode usar o comando `git add` para adicionar um arquivo ao próximo commit. Nesse mesmo exemplo, caso queira criar um commit com os arquivos `index.html` e `index.css`, é possível fazer isso executando o comando `git add` para esses dois arquivos:

```
git add index.html
git add index.css
```

Além disso, caso queira fazer um commit incluindo todos os arquivos que foram modificados, é possível fazer isso executando o comando `git add .`.

Utilizando `git status` também é possível ver quais arquivos foram adicionados para o próximo commit na seção `changes to be committed`:

```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
  modified:   index.html
  modified:   index.css
  new file:   my-image.png

```

Tendo selecionado os arquivos para o commit, podemos executar o comando `git commit` para criar o commit em si. Esse comando vai abrir um editor de texto com um arquivo contendo as mudanças do commit, no seguinte formato:

```

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch translate-nerves-page
# Changes to be committed:
#       modified:   index.html
#       modified:   index.css
#       new file:   my-image.png
```

Neste ponto, devemos usar o editor para escrever a mensagem do commit, utilizando uma linha em branco para separar o título e o corpo da mensagem.

```
Título da mensagem de commit

Corpo da mensagem do commit. Este é um texto opcional que serve
para explicar com mais detalhes a mudança que está sendo feita.
Aqui é importante focar em o que está sendo feito e por que
esta mudança está sendo feita.

Pule uma linha antes de começar um novo parágrafo e quebre as
linhas em aproximadamente 72 caracteres.

- É ok utilizar uma lista de tópicos

- Geralmente se usa hífen (-) ou asterisco (*) seguido de um
  espaço para marcar um novo tópico na lista.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch translate-nerves-page
# Changes to be committed:
#       modified:   index.html
#       modified:   index.css
#       new file:   my-image.png
```

Caso não queira adicionar um corpo à mensagem do commit, também é possível utilizar a comando de commit com a flag `-m` passando o título da mensagem entre aspas:

```
git commit -m "Título da mensagem do commit"
```

## Quanto código deve ir em um commit?

Um ponto importante para um bom commit é que ele seja objetivo. Um bom commit existe para fazer uma coisa, pois isso ajuda a entender melhor como o projeto evoluiu ao longo do tempo, além de fazer com que seja mais fácil reverter o commit caso algo dê errado.

Por exemplo, imagine que você precisa implementar uma funcionalidade nova em um projeto e começa a escrever o código para isso. Então, depois de um tempo, você percebe que o código para essa funcionalidade precisa chamar um módulo em outra parte do sistema, mas esse módulo está muito confuso e difícil de entender. Como você já tá com a mão na massa, decide fazer uma rápida refatoração nesse módulo, e depois volta pro código da funcionalidade.

Código feito, você decide escrever os testes automatizados. O processo corre bem, você faz os testes, mas percebe que tem uma configuração que está desativada no projeto e que melhora o modo como o resultado dos testes é mostrado depois que eles rodam. Então, você já aproveita e ativa isso no projeto.

Agora sim. Código feito, hora de fazer o commit.

Nesse caso faz sentido criar três commits diferentes: um alterando a configuração de testes, um com a refatoração e outro com a funcionalidade em si (incluindo os testes). Isso pode parecer redundante, mas melhora o histórico de commits do projeto. Separar os commits por mudança faz com que seja mais fácil reverter alguma dessas mudanças no futuro, caso necessário.

Se, por exemplo, o time decidir que não faz sentido manter essa configuração de testes no projeto, ou se surgir algum bug causado pela refatoração, é possível reverter o commit que faz apenas isso.

Sendo assim, é importante o commit fazer apenas uma mudança. Seja ela de uma linha ou de vários arquivos. O principal a se ter em mente é que o commit pode ser acessado no futuro e, se necessário, pode ser revertido. Ter isso em mente ajuda a medir o quanto é suficiente para um commit.

## Mensagem do commit

A mensagem do commit é onde podemos escrever o que o commit faz. Ter uma mensagem boa é muito importante para um bom commit, pois isso torna muito mais fácil entender o que aconteceu no projeto ao se ler o seu histórico. A mensagem do commit se divide em duas partes: título e corpo.

### Título

O título da mensagem do commit consiste de uma frase sucinta que diz **o que** o commit faz. Ele deve ser sucinto, descritivo e específico.

Por exemplo, veja estes três commits:

```
623509 estiliza botões
f12144 correção de bug
23c30c refatorando
```

Essas mensagens, apesar de descreverem o que o commit faz, são muito genéricas. Compare com este exemplo:

```
623509 Estiliza botões da página de login
f12144 Corrige bug de entrega de emails duplicada
23c30c Refatora módulo UserAccount
```

Ter um título específico ajuda a diferenciar commits similares pela mensagem. Se numa semana de pagar dívidas técnicas o time faz 10 commits diferentes com refatorações em várias partes do código, ter 10 commits diferentes com a mensagem `Refatorando` vai tornar a leitura do histórico de commits do projeto bem confusa. Mas se cada commit de refatoração inclui na mensagem qual código dentro do projeto foi refatorado, isso torna os commits mais descritivos e o histórico mais fácil de entender.

O Git não impõe um limite de caracteres no título do commit, ainda assim, a boa prática é que ele não tenha mais de 50 caracteres. Isso faz com que o histórico seja mais legível e incentiva a pessoa que está fazendo o commit a parar e pensar em um jeito sucinto de descrever o que o commit faz. Inclusive, a interface do GitHub avisa dessa prática quando tentamos criar um commit por lá com um título longo.

![Imagem de um campo de texto com o título "Commit message" contendo a mensagem "Long commit subject message to show that GitHub will collapse it when it has more than 72 characters" e um texto de aviso com a mensagem "Pro tip! Great commit summaries contain fewer than 50 characters. Place extra information in the extended description"]({{site.baseurl}}/images/git-commits/long-commit-message.png)

Além disso, ao exibir commits cujo título tenha mais de 72 caracteres, a interface do GitHub não vai exibir o título inteiro do commit, mostrando apenas o começo dela e colocando reticências para mostrar o título completo.

![Imagem de um commit no GitHub com a mensagem "Long commit subject message to show that GitHub will collapse it when..."]({{site.baseurl}}/images/git-commits/collapsed-commit-message.png)

Então, mesmo que seja necessário fazer um título de commit com mais de 50 caracteres, considere 72 como o número limite. Se estiver difícil resumir tudo que o commit faz nessa quantidade de caracteres, pode ser um sinal de que o commit está fazendo muitas mudanças no projeto. Nesse caso, faz sentido separar isso em commits menores.

### Corpo da mensagem

Além do título, a mensagem de um commit pode ter uma descrição longa, ou corpo da mensagem. Aqui é o lugar para explicar de modo mais detalhado o que o commit faz. O corpo da mensagem pode ser um texto longo, então aqui vale escrever como um texto comum. Se necessário você pode utilizar parágrafos, deixar links de serviços úteis para a compreensão do commit (uma tarefa no gerenciador de tarefas que o time usa, por exemplo) ou até utilizar listas de tópicos. O importante aqui é comunicar bem.

Um ponto importante do corpo da mensagem é que ela deve focar em dizer **o que** foi feito no commit e **por que** essa mudança aconteceu. Pode parecer tentador explicar como a mudança foi feita, mas, na maioria dos casos, essa informação já está presente no código do commit (acessível pelo comando `git diff`). Explicar isso também no corpo da mensagem, além de ser redundante, pode tornar esse texto desnecessariamente longo e dificultar a localização de alguma informação importante e que não está disponível em outro lugar.

Mesmo tendo o corpo da mensagem à disposição, é importante lembrar que uma boa mensagem aqui não retira a necessidade de um bom título. Alguns comandos que mostram o histórico de um projeto, como `git log --oneline` e `git shortlog`, mostram apenas o título do commit, sendo o corpo da mensagem mais específico para quando olhamos o histórico de uma forma mais completa ou quando vemos o commit individualmente. O corpo da mensagem é importante, mas não substitui um bom título.

Também vale dizer que nem todo commit precisa ter uma mensagem longa, em alguns casos apenas o título já é suficiente para explicar o que o commit faz. Por exemplo, um commit que corrige um erro de digitação no guia de contribuição de um projeto pode ter uma mensagem de commit apenas com o título, sem deixar de comunicar bem o que o commit faz.

```
a73197 Corrige erro de digitação no guia de contribuição
```

O ponto principal aqui é prover contexto para quem olhar esse commit no futuro saber **o que** está sendo mudado e **por que** essa mudança aconteceu.

## Estilo

Algumas dicas pequenas de como escrever um commit, mas que ajudam a manter um bom histórico em um projeto.

#### Comece o título com letra maiúscula

Começar o título com letra maiúscula é uma boa prática de escrita padrão e ajuda na leitura do histórico de commits.

#### Não utilize ponto final no título do commit

Novamente, aqui se aplica a regra padrão de escrita. O título do commit, por ser um título, não precisa terminar com ponto final.

#### Utilize uma linha em branco para separar título e corpo do commit

Utilizar essa linha em branco antes do corpo do commit facilita a leitura da mensagem. Além disso, algumas ferramentas como `git log`, `git shortlog` e `git rebase` podem se confundir se essa quebra entre título e corpo não for feita.

#### Limite as linhas do corpo do commit a 72 caracteres

Para o corpo da mensagem também vale a regra de limitar o tamanho de cada linha em 72 caracteres. Isso ajuda na legibilidade de mensagens longas e diminui bastante a possibilidade de quebrar a formatação da mensagem quando ela for exibida.

### Utilize o tempo verbal correto para o título da mensagem

Este é um ponto que contribui bastante para melhorar a legibilidade dos commits de um projeto, mas que é fácil de deixar passar.

Ao criar o commit, é comum apenas falar o que _foi feito_ ou o que _está sendo feito_, utilizando para isso verbos no passado ou no gerúndio:

  * `Fixed bug with Y`
  * `Changing behavior of X`
  * `Refatorou classe de autenticação`
  * `Atualizando biblioteca xpto`

Escrever desse modo pode parecer mais natural na hora de compor a mensagem do commit, mas isso pode dificultar a leitura do histórico de commits de um projeto.

Ao fazer commits em inglês, escreva o título no modo **imperativo**:

  * `Refactor subsystem X for readability`
  * `Update getting started documentation`
  * `Remove deprecated methods`
  * `Release version 1.0.0`

Isso vai de acordo com o padrão que o próprio Git segue quando gera uma mensagens de commit automaticamente em casos como no `git merge`:

```
Merge branch 'myfeature'
```

Ou como no `git revert`:

```
Revert "Add the thing with the stuff"

This reverts commit cc87791524aedd593cff5a74532befe7ab69ce9d.
```

Uma dica ao fazer mensagens de commit em inglês, é que um bom título sempre deve completar a frase: `if applied, this commit will`. Por exemplo:

  * if applied, this commit will `refactor subsystem X for readability`
  * if applied, this commit will `update getting started documentation`
  * if applied, this commit will `remove deprecated methods`
  * if applied, this commit will `release version 1.0.0`

Já quando for escrever a mensagem do commit em português conjugue o verbo no **presente do indicativo**, utilizando a **terceira pessoa do singular**:

  * `Refatora sistema X para melhorar legibilidade`
  * `Atualiza documentação de instalação do projeto`
  * `Remove métodos obsoletos`

### Commits em português ou em inglês?

Esse é um ponto bastante discutido quando se fala de commits, definir em qual idioma as mensagens serão escritas é muito importante.

Há bons argumentos dos dois lados. Fazer os commits em inglês tem a vantagem de possibilitar que pessoas de diferentes nacionalidades contribuam no projeto, porém exige que todos os membros do time tenham fluência no idioma para que o histórico seja bem escrito e entendido. Por outro lado escrever commits em português permite que pessoas que não possuem fluência em inglês escrevam bons commits, mas pode ser um grande problema caso seja necessário que alguém que não sabe português precise contribuir no projeto.

A meu ver, essa decisão depende totalmente do time. Há casos em que commits em português vão fazer mais sentido e outros casos em que commits em inglês vão fazer mais sentido. O ponto chave aqui é **consistência**. Uma vez que essa decisão foi tomada, ela deve ser seguida. Ter um histórico de projeto que possui commits em inglês **e** em português é um grande problema, pois isso vai  exigir que os membros do time saibam português e inglês para entender o histórico e será um grande problema caso alguém que não sabe português precise contribuir no projeto. A falta de consistência nesse aspecto significa ter as desvantagens de cada caminho, sem ter as vantagens que eles trazem.

```
Neste texto utilizo mensagens de commit em português para fins de didática e para
que o texto também seja compreensível para quem não sabe inglês.
```

### Testes

Afinal, é necessário que os testes estejam passando para que um commit seja feito?

Eu considero importante deixar os testes do projeto passando sem erros antes de fazer um commit. Considerando que um commit é um ponto de retorno para o qual é possível voltar no futuro, ter os testes do projeto passando vai facilitar a vida de quem precisar executar o projeto em algum commit que não seja o mais recente. Além disso, ter testes quebrando pode ser um sinal de que a mudança que o commit pretende fazer não está, de fato, completa.

## Dicas práticas

#### Configurar qual editor usar no Git

Por padrão, o git utiliza o editor de texto do padrão do sistema (que em muitos casos é o `vi`) para editar mensagens de commits. Para utilizar algum outro editor é necessário alterar a configuração `core.editor`. Por exemplo, executando o seguinte comando:

```
git config --global core.editor atom
```

O Git agora vai utilizar o Atom como editor padrão. Isso vale para mensagens de commit e para outras operações do Git, como rebase interativo.

#### Editar mensagem do último commit

Caso você queira editar a mensagem do último commit, utilize o comando `git commit --amend`. Isso vai abrir o seu editor de texto mostrando o último commit e, assim, é possível editar a mensagem. Se não for necessário editar o corpo da mensagem, isso pode ser feito usando:

```
git commit --ammend -m "Nova mensagem para o commit"
```

Uma dica pra lembrar desse comando é que com a opção `--amend` você consegue "emendar" o último commit.

#### Adicionar mais arquivos ao último commit

Para isso, também podemos usar o comando `git commit --amend`.

Faça as mudanças que quer adicionar ao commit mais recente, adicione essas mudanças usando `git add` e então utilize `git commit --amend`. Como citado na seção anterior, isso vai abrir o editor de texto, possibilitando que também edite a mensagem do commit.

Caso queira apenas adicionar mais mudanças ao commit, sem editar a mensagem, é possível fazer isso com `git commit --amend --no-edit`.

## Dicas finais

Escrever commits é algo comum que faz parte do processo de escrever software. Apesar disso, fazer commits bem feitos não é algo trivial. Git é uma ferramenta muito importante de comunicação e se comunicar de maneira efetiva também não é uma tarefa trivial. É bastante importante ter isso em mente ao utilizar o Git.

Fazer bons commits dá trabalho, mas traz benefícios. A pessoa que precisar olhar o projeto vai agradecer, e essa pessoa pode ser você.

Aqui tem algumas fontes que usei pra fazer esse texto e que recomendo bastante para entender mais sobre Git:

  * Livro [Pro Git](https://git-scm.com/book/en/v2)
  * [Git field guide](https://afterhours.io/git-field-guide.html) por [Lucas Mazza](https://twitter.com/lucasmazza/)
  * [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/) por [Chris Beams](https://twitter.com/cbeams)

Gostou do texto? Tem alguma sugestão ou dúvida? Pode usar a caixa de comentários ou falar comigo no [Twitter](https://twitter.com/RuanBrandao). Até mais!
