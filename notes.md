##### 21/08/2023

CURSO iOS: usando recursos nativos

@01-Conhecendo o projeto

@@01
Apresentação

[00:00] Boas-vindas. Eu sou o Ândriu, instrutor desse curso, onde nós vamos falar sobre frameworks nativos para iOS que são muito utilizados no mercado.
[00:10] E nós vamos utilizar como base esse aplicativo Alura Ponto, onde nós podemos registrar o ponto de trabalho, ou seja, o horário em que o funcionário começa a trabalhar, o horário em que ele vai almoçar, volta do almoço e quando ele termina o expediente.

[00:28] A ideia é iniciar explorando a câmera. Então a ideia desse aplicativo é tirarmos uma selfie e depois utilizarmos essa foto e registrarmos um recibo de ponto, que é o que nós temos na segunda aba do aplicativo.

[00:44] Também vamos aprender a utilizar as fotos da biblioteca para inserir no nosso perfil. E depois nós vamos explorar o Core Data como framework para persistência de informações no nosso device.

[01:01] Então nós temos um problema: quando nós fechamos o aplicativo perdemos todos os recibos que nós temos, e a ideia é utilizarmos o Core Data para salvar esses dados local no nosso device.

[01:15] Então vamos aprender a salvar. Se fecharmos o aplicativo e abrirmos de novo, nós temos todos os recibos. Vamos também aprender a listar os objetos, que é exatamente essa lista com todos os recibos. E também vamos aprender a deletar esses recibos, tudo utilizando frameworks nativos, no caso o Core Data.

[01:42] Então vamos criar uma camada DAO no nosso aplicativo, com todos esses métodos para salvar, deletar, listar. Falaremos também sobre a atualização desses recibos, e tudo de forma nativa e na prática.

[02:00] Esse é o conteúdo que veremos durante esse curso. Eu espero você.

@@02
Projeto inicial

Para iniciar o curso, faça o download do projeto.
Bons estudos!

https://github.com/alura-cursos/2315-Alura-Ponto/archive/511794b6d467a13224bb2ebd644931dac67dfd91.zip

@@03
Conhecendo o projeto

[00:00] Estamos iniciando mais um curso na Alura. Agora falaremos sobre alguns frameworks nativos do iOS, que são muito utilizados, por exemplo, a câmera, como utilizamos a funcionalidade da câmera no nosso aplicativo, como acessamos a biblioteca de imagens para ter acesso às fotos que tiramos e utilizá-las no app.
[00:21] Outro assunto muito importante é como nós podemos persistir dados nosso app para que quando fechemos nós não percamos esses dados. É isso que vamos aprender.

[00:35] Vamos utilizar como base o aplicativo Alura Ponto, que eu vou mostrar para você. É um aplicativo que marca a batida de ponto dos funcionários.

[00:45] Então você pode registrar quando você começa a trabalhar, quando você vai almoçar, quando volta do almoço, no final do seu expediente. Então conseguimos registrar essas horas para ter um controle de quantas horas o funcionário está trabalhando.

[01:00] Vamos utilizar esse app Alura Ponto, que tem essas funcionalidades que eu comentei, por exemplo, o uso da câmera para registrar o ponto. Se eu clico em “Registrar” eu tenho acesso à câmera. Então posso tirar uma foto e registrar o ponto, quando eu aceito a foto que eu tirei.

[01:24] Tem a tela de recibos, onde eu consigo visualizar todas as batidas de ponto que eu fiz. Repare que eu acabei de incluir uma batida de ponto. Eu posso voltar ao início e registrar mais um ponto. Agora na tela de recibos eu tenho duas batidas. Então é um app de controle de horas do funcionário.

[01:51] Existe também a possibilidade de adicionar alguma foto da biblioteca, o que também vamos entender como fazer.

[02:00] E também trabalharemos com a persistência das nossas informações. Assim que eu fechar o app eu ainda tenho essas informações persistidas no meu device, de forma local, utilizando o Core Data. Então aprenderemos a fazer um CRUD dessas informações, localmente, utilizando o Core Data.

[02:21] Esse basicamente é o app com o qual nós vamos trabalhar. Já temos algumas classes prontas para ganharmos tempo.

[02:31] Tenho a seção, onde eu guardo momentaneamente os recibos dos pontos na memória. Nesse momento, se eu fechar o app e abrir de novo eu ainda não persisti, e nós trabalharemos nisso.

[02:47] Tenho também a classe de recibo, eu tenho uma classe de formato data e hora, tenho o controle da home, que é a tela principal, onde temos a possibilidade de registrar o ponto e o horário. E tenho também a tela de recibos, onde temos uma tableview que lista os recibos e um botão onde eu posso então acessar a biblioteca de fotos e adicionar uma foto de perfil.

[03:18] Temos algumas classes prontas, mas ainda teremos bastante trabalho pela frente para conseguir entender e também utilizar esses frameworks da melhor maneira possível.

@@04
Para saber mais: Construção do app

Neste capítulo, apresentamos o projeto Alura Ponto, que é utilizado para registrar os horários de entrada e saída de funcionários.
O Alura Ponto será a base para nossos estudos, e entenderemos como utilizar diversos frameworks nativos para terminar de construir esse aplicativo.

A Apple disponibiliza muitas APIs nativas para se construir apps robustos. Durante esse curso, vamos usar na prática vários deles para que você tenha o primeiro contato com esses recursos.

@@05
Faça como eu fiz: Frameworks nativos

Nesse primeiro capítulo, começamos a entender quais serão os desafios que teremos pela frente. Como foi apresentado, teremos um projeto com algumas views prontas, mas teremos o desafio de implementar as funcionalidades que faltam.

Todos os frameworks que utilizaremos estão listados na página de desenvolvimento da Apple.

https://developer.apple.com/develop/

@@06
O que aprendemos?

Vimos o que será tratado neste curso, conhecemos o projeto e um pouco sobre frameworks nativos.