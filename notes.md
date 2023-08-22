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

@02-Utilizando a câmera

@@01
Projeto da aula anterior

Se você deseja começar o curso a partir desta aula, pode fazer o download do projeto desenvolvido até o momento.

@@02
Câmera do iOS

[00:00] Começaremos explorando a funcionalidade da câmera no nosso aplicativo. A ideia é utilizarmos o iPhone físico para testar essa funcionalidade.
[00:13] Infelizmente no simulador nós não conseguimos testar todos os recursos disponíveis no iOS, e a câmera é um deles. Por isso eu estou com meu iPhone e vamos testar assim que implementarmos essa funcionalidade.

[00:31] Primeiramente eu tenho aqui esse botão “registrarButton”. Eu vou começar buildando o app, pode ser no simulador mesmo, porque ainda não implementamos. Mas a ideia é implementarmos a partir desse clique a chamada para essa funcionalidade da câmera.

[00:53] Só que antes precisamos visualizar e verificar se existe esse recurso. Quando eu clicar em “Registrar Ponto” esse método registrarButton é disparado.

[01:09] Eu vou começar verificando se é possível abrir a câmera, ou seja, se eu estou com o device físico mesmo. Então vou fazer um if UIImagePickerController, que é a classe que nos dá acesso às funcionalidades da câmera e da biblioteca.

[01:26] Eu tenho esse método isSourceTypeAvailable(.camera), e eu posso passar um dos tipos que eu quero verificar. Eu quero verificar se a câmera está disponível. Se estiver, vamos implementar alguma coisa para chamar a câmera.

[01:45] Começaremos criando uma classe chamada "câmera" para não deixarmos essas funcionalidades todas amontoadas no View Controller .

[01:54] É uma boa prática você sempre distinguir quais são as responsabilidades de cada classe e tentar extrair isso sempre que possível para não deixar o View Controller com muita responsabilidade.

[02:09] Então eu vou criar uma nova classe. Sobre a pasta “Model” clico com o botão direito e escolho “Novo Arquivo”. Seleciono “Swift File” e dou um “Next”. Vou chamar de “Camera”.

[02:25] Neste arquivo, vou criar minha classe: class Camera: NSObject. E vou implementar alguns métodos. O primeiro método que eu vou implementar será um método para abrir câmera func abrirCamera.

[02:49] Eu vou precisar receber por parâmetro o View Controller, porque ele tem acesso ao método present, onde de fato conseguimos abrir o UIImagePickerController, que é o Controller da câmera.

[03:06] Então vou pedir no parâmetro um Controller, func abrirCamera(_ controller: UIViewController, _ imagePickerController, que é a classe responsável por gerenciar a câmera e a biblioteca de imagens.

[03:24] No fim das contas o que eu vou fazer é controller.present(imagePicker, animate: true, completion: nil) para exibir na tela. No fim das contas é isso que faremos.

[03:36] Só que antes disso precisamos configurar algumas coisas como, por exemplo, se é possível editar a foto ou não, qual câmera eu quero abrir, se é a frontal ou a traseira. Então temos algumas configurações.

[03:50] A imagePickerController tem um método chamado allowsEditing = true, que é permitir edição da foto. E vou passar como verdadeiro.

[03:58] Eu tenho também o tipo que eu quero exibir nesse imagePickerController, se é a câmera ou a biblioteca, então também preciso configurar. Eu vou passar imagePicker.sourceType = .camera.

[04:15] Por enquanto está bom só para testarmos. Depois faremos mais algumas configurações.

[04:20] Voltando no “HomeView Controller”, eu vou criar um novo método chamado func tentaAbrirCamera(). E dentro do botão eu chamo esse método.

[04:40] Eu vou criar uma variável private e eu vou colocar a keyword lazy, e vou instanciar: private lazy var camera = Camera.

[04:51] O lazy é uma variável preguiçosa. Isso quer dizer que ela só será instanciada de verdade quando ela for chamada, quando ela for requisitada em algum ponto do nosso código. Caso contrário, ela não é inicializada. Por isso é uma variável lazy, preguiçosa. Isso ajuda no gerenciamento de memória.

[05:13] E eu vou criar também um private lazy var controladorDeImagem = UIImagePickerController. Tenho essas duas variáveis que vamos utilizar.

[05:31] No tentaAbrirCamera eu vou chamar a camera.abrirCamera e vou passar um controller, que é o próprio “HomeViewController”. Então vou passar ele mesmo e o próprio controlador de imagem, camera.abrirCamera(self, controladorDeImagem).

[05:52] Agora vamos rodar o aplicativo, eu vou rodar no meu iPhone, e vamos verificar se precisamos fazer mais alguma configuração ou se só isso já basta para que consigamos então abrir a câmera.

[06:08] Já buildei o app no meu iPhone, vamos clicar em “Registrar Ponto”. E nós temos um crash. Vamos ver o que aconteceu. Ele está falando que ele precisa de acesso para o uso da câmera. Então vamos utilizar o arquivo “info.plist” para pedir acesso ao usuário.

[06:35] Este é um ponto muito importante, porque muitos recursos que o iOS tem, como câmera, mapa, push notification, várias coisas precisam da autorização do usuário para conseguir utilizar, por questão de segurança. E a câmera é um deles.

[06:54] Então como é que eu faço para pedir essa autorização para o usuário? Eu tenho um arquivo chamado “info.plist”, onde nós temos algumas configurações. Eu preciso adicionar uma nova configuração para pedir essa informação.

[07:13] Vou clicar no sinal de mais ao lado de “Information Property List”, e eu tenho exatamente a configuração que precisamos colocar. Então eu vou chamar o Privacy, e eu tenho vários métodos que permitem utilizarmos esses recursos. Tem a câmera, contato, calendário, Bluetooth, enfim, várias permissões que podemos utilizar.

[07:43] Eu vou utilizar a “Privacy – Camera Usage Description”, então seleciono e preciso colocar um valor para ela. O valor na verdade é a mensagem que queremos colocar.

[07:54] Qual é a mensagem que eu quero colocar para o usuário para ele entender que eu preciso utilizar aquele recurso? Eu vou colocar “Alura Ponto necessita de acesso à câmera para registrar o ponto eletrônico”.

[08:20] Então configuramos através do arquivo “info.plist”. Agora eu vou rodar mais uma vez o aplicativo para testarmos.

[08:33] Vou abrir o aplicativo mais uma vez. Cliquei em “Registrar Ponto” e agora sim ele traz essa janela alert falando que o Alura Ponto gostaria de acessar a câmera e tem a mensagem que colocamos.

[08:58] Vou clicar em "Ok" para conseguirmos acesso à câmera. Repara que ele abriu diretamente a câmera frontal, então essa é uma configuração que podemos melhorar.

[09:11] Eu vou tirar uma foto e clicar em “Use Photo”. Mas, por enquanto, não configuramos nada para recebermos a foto que tiramos. Então esse é um ponto de melhoria que veremos a seguir.

@@03
Utilizando a foto

[00:00] Já estamos com acesso à câmera ao clicar em “Registrar Ponto”.
[00:11] Ainda precisamos fazer alguns ajustes de usabilidade como, por exemplo, abrir a câmera no modo frontal, já que precisamos tirar uma selfie para registrar o ponto.

[00:22] E também, quando clicamos em “Usar foto” nós ainda não estamos fazendo nada, não estamos gerando recibo. Então é outro ajuste que faremos.

[00:33] Em relação à usabilidade, de abrir a câmera frontal, vamos abrir a classe da câmera, que é responsável por gerenciar e abrir a câmera ou a biblioteca quando nós implementarmos. Nós estamos concentrando as configurações nessa classe Camera.

[00:54] Existe uma propriedade do imagePicker, que é cameraDevice. Nós podemos utilizar essa propriedade para passar qual tipo nós queremos.

[01:05] Então nós vamos verificar se existe a câmera frontal, então UIImagePickerController, então vamos verificar a disponibilidade do recurso.

[01:18] Se houver câmera frontal nós vamos utilizar. Se não, utilizaremos a câmera traseira mesmo. É dessa forma que fazemos essa validação, imagePicker.cameraDevice = UIImagePickerController.isCameraDeviceAvailable(.front) ? .front : .rear.

[01:32] Vou rodar mais uma vez o projeto para fazer o teste e verificar se estamos abrindo o app com a câmera frontal. Buildei no meu iPhone, vou clicar em “Registrar Ponto”. Agora sim então já estamos abrindo com a câmera frontal. Já é um ponto bem importante em questão de usabilidade.

[01:59] O próximo ponto é em relação a quando clicamos no botão “Usar Foto”. Precisamos obter essa imagem para manuseá-la de alguma forma.

[02:09] Para fazer isso precisaremos implementar um protocolo de delegate, dessa classe UIImagePickerController. Lá tem um método que é disparado quando clicamos em “Usar Foto”. E é isso que faremos agora.

[02:26] A ideia então é criar uma extensão para implementar esse protocolo. Tanto faz se eu colocar uma vírgula e implementar, ou criar uma extensão da classe câmera e implementar esse protocolo: extension Camera: UIImagePickerControllerDelegate.

[02:45] E também precisamos implementar um outro protocolo, que é o UINavigationControllerDelegate.

[02:53] Então já implementamos esse protocolo. Agora nós temos acesso a um método chamado didFinishPicking, então vamos utilizá-lo. Então é didFinishPickingMediaWithInfo, que na verdade é quando clicamos em “Usar Foto”, então esse método é disparado.

[03:19] Nós temos acesso a um parâmetro, que é esse Info, que é um dicionário do UIImagePickerController, e o tipo Any.

[03:30] Então ele retorna um tipo meio estranho, não é uma image, que é o que precisamos. Então faremos um tratamento para tentar fazer um cast desse estranho que estamos recebendo para uma UIImage.

[03:46] A primeira coisa que faremos é fechar o Picker de foto, então vou fazer picker.dismiss(animated: true). E em seguida farei uma verificação: guard let foto = info[.]. E eu vou acessar uma propriedade desse dicionário que é editedImage. E eu vou tentar converter isso para UIImage. Se eu não conseguir, eu dou o return do meu guard let e escapo a função. Se eu conseguir fazer isso significa que eu já tenho acesso à foto.

[04:31] Então vou colocar um print com o nome dessa constante que nós criamos para tentar fazer o cast, só para ver se já estamos conseguindo ter acesso a essa foto, print(foto).

[04:43] Coloquei um breakpoint na linha de código de print(foto) , ou seja, eu quero que meu código pare a execução nesse ponto para conseguirmos ver o que está retornando da câmera.

[04:53] Vou rodar mais uma vez o projeto no meu iPhone e vamos fazer então esse teste. Clico em “Registrar Ponto”, tiro uma foto, clico em “Usar foto”, e não está acontecendo nada.

[05:14] Primeiro ponto: nós estamos implementando o protocolo de UIImagePickerControllerDelegate, porém, não citamos esse valor, ou seja, nós não indicamos qual a classe que vai implementar esse protocolo.

[05:29] Como fazer isso? Faremos imagePicker.delegate = self. Ou seja, essa classe que está implementando o protocolo delegate do UIImagePickerController.

[05:43] Vamos rodar novamente. Vou subir o app de novo. E agora vamos então fazer o teste. Cliquei em “Registrar Ponto”, tirei a foto, cliquei em “Usar foto”. Agora sim, disparou o método, porque nós setamos a variável de delegate.

[06:11] Então nós já temos acesso à foto. Repara que ele não está null. Vou até apagar o debug e inspecionar o valor desta variável: po foto. E vemos então que ele retorna de fato um UIImage. Então nós já temos a imagem para manipularmos.

[06:35] O próximo passo é de alguma forma devolvermos essa imagem para o “ViewController”, que é onde de fato vamos manejar a imagem e criar o recibo.

[06:53] Na Camera eu vou criar um protocolo, usando um design pattern chamado delegate: protocol CameraDelegate: AnyObject.

[07:07] E vou criar um método: func didFinishFoto. Ou seja, acabei de selecionar a foto, ou fechar o componente de foto. E vou devolver um UIImage: func didFinishFoto(_ image: UIImage).

[07:30] Como é que eu utilizo então esse protocolo? Para utilizar esse design pattern que se chama delegate, eu vou criar uma variável chamada delegate, do tipo do meu protocolo: weak var delegate: CameraDelegate?. É exatamente o que fizemos para utilizar o imagePickerController.

[07:49] Só que agora vamos utilizar isso na "HomeViewController". Vou criar uma extensão, e vou implementar esse protocolo que eu acabei de criar: extension HomeViewController: CameraDelegate. E vou ter acesso ao método didFinishFoto.

[08:11] Eu vou criar o meu recibo. Ou seja, acabei de selecionar a foto, significa que eu bati o ponto. Então eu vou criar o meu recibo. O status, por enquanto, eu vou passar como false. Vou passar a data e hora atual, e a foto é a imagem que eu acabei de receber, que é esse image, let recibo = Recibo(status:false, data: Date(), foto: image).

@@04
Testando a câmera

[00:00] Para finalizar então, agora nós precisamos adicionar esse recibo que nós acabamos de criar. Ou seja, quando fazemos uma selfie e clicamos em confirmar nós criamos o objeto recibo que precisamos adicionar na seção, onde nós temos a listaDeRecibos.
[00:20] Eu vou gerar um build no iPhone. E a lista que precisamos preencher é a lista da tela de recibo, onde nós vamos listar os recibos, que por enquanto está vazia.

[00:39] No aplicativo, vou clicar em “Registrar Ponto”, tirar uma foto e clicar em “Usar foto”. E a lista de recibos continua vazia, porque nós ainda não estamos adicionando o recibo na lista da seção. Faremos isso agora.

[00:59] A primeira coisa que eu vou fazer é vir na "HomeViewController", e embaixo de onde nós criamos o objeto recibo eu vou chamar a seção e chamar o método adicionar recibo, passando o recibo que nós criamos: Secao.shared.addRecibos(recibo).

[01:27] Eu vou renomear o método didFinishFoto. Então vou na Camera e renomear para didSelectFoto. Para cair nesse método precisamos setar o delegate da câmera, que é o que falta fazer.

[01:49] No "HomeViewController", nós temos o camera.delegate = self, ou seja, vai chamar esse método quando for disparado. Então logo depois que pegamos a foto vamos chamar a variável delegate e o método didSelectFoto. Então vou passar a foto que nós estamos recuperando da câmera.

[02:15] Chamando essa variável delegate que nós criamos com a implementação do nosso protocolo, ele vai vir na home e vai então disparar esse método, onde nós criamos o recibo.

[02:31] Eu vou rodar mais uma vez no iPhone para testarmos e vermos se a implementação está realmente funcionando.

[02:43] Vou clicar em “Registrar ponto”, tirar a foto e agora nos recibos temos nosso primeiro recibo de ponto. Então já estamos adicionando o recibo na lista.

[03:02] O importante dessa aula foi nós entendermos como utilizar a classe UIImagePickerController. Há diversos métodos, dá para fazer bastante coisa com essa classe, aprendemos a tirar foto.

[03:18] E a ideia é darmos sequência no nosso projeto onde vamos aprender a escolher uma foto da biblioteca. De repente não quero tirar uma foto na hora e quero adicionar uma foto da biblioteca em qualquer outro aplicativo, também temos esse recurso através da classe UIImagePickerController.

[03:38] Para o nosso contexto será importante para setarmos uma foto de perfil. Para bater o ponto realmente precisa abrir a câmera na hora. Mas na tela de recibos conseguimos utilizar esse exemplo para implementar a biblioteca de imagem do iOS.

@@05
Verificando a disponibilidade do recurso

Qual a importância da implementação do método isSourceTypeAvailable da classe UIImagePickerController?

O método isSourceTypeAvailable define o tipo de dado (câmera ou biblioteca) que será aberto.
 
Alternativa correta
O método isSourceTypeAvailable verifica se está disponível o uso da câmera, evitando possíveis crashes no aplicativo.
 
Alternativa correta! Correto. É importante implementar esse método, pois ou a câmera pode já estar em uso por outro app ou a biblioteca de fotos pode estar vazia. Como esse método retorna um boolean, conseguimos tratar caso ocorra algum problema.
Alternativa correta
A implementação desse método é utilizada para evitar crash quando o app estiver funcionando no simulador do XCode.
 
Alternativa correta
O método isSourceTypeAvailable recupera a foto tirada com a câmera do iOS e nos devolve em formato de dictionary.

@@06
Faça como eu fiz: Uso da câmera / biblioteca de imagens

O uso da classe UIImagePickerController nos oferece a possibilidade de utilização tanto da câmera, quanto da biblioteca de imagem do iOS.
Como podemos ter acesso aos eventos de uso da câmera para tirar uma foto ou a escolha de uma imagem da biblioteca?

Opinião do instrutor

Para ter acesso aos eventos de escolha de foto, é necessário implementarmos o protocolo de delegate UIImagePickerControllerDelegate. Através dele, podemos implementar o método didFinishPickingMediaWithInfo que nos devolve informações da imagem selecionada.

@@07
O que aprendemos?

Nesta aula, aprendemos sobre:
Implementação da classe UIImagePickerController:
A classe '''UIImagePickerController''' nos oferece o uso da câmera para tirar fotos, gravar filmes e escolher itens da biblioteca de mídia do usuário.
O tipo SourceType.Camera fornece, aos dispositivos que suportam captura de mídia, o uso da câmera ou gravação de vídeos.

#### 22/08/2023

@03-Biblioteca de fotos

@@01
Projeto da aula anterior

Se você deseja começar o curso a partir desta aula, pode fazer o download do projeto desenvolvido até o momento.

https://github.com/alura-cursos/2315-Alura-Ponto/archive/c5d55d13e856d15d1b14423e43a759f0911cce7f.zip

@@02
Biblioteca de fotos do iOS

[00:00] Já aprendemos a acessar a câmera do iPhone e tirar a foto, vamos seguir com as implementações, só que agora vamos aprender a acessar a biblioteca de imagens do iOS.
[00:11] Nós temos a aba de recibos, onde nós podemos escolher uma imagem de perfil do usuário que utiliza esse app. Quando eu clico sobre o espaço para a foto eu abro um UIAlertController. E eu tenho duas opções: uma é “Cancelar” e outra é a “Biblioteca de fotos”. Quando seleciono uma imagem eu posso setar então a imagem de perfil na tela de recibos.

[00:35] Dividiremos esse vídeo em duas etapas. A primeira é criação desse menu, que é um UIAlertController. E a segunda etapa é de fato a utilização do UIImagePickerController para ter acesso à biblioteca de fotos.

[00:50] Ao clicar em cima do ícone da foto de perfil é disparado o método escolherFotoButton. E a ideia é criarmos esse menu, esse UIAlertController com essas opções.

[01:05] No ReciboViewController, vou vou criar um novo método chamado mostraMenuEscolhaDeFoto. E vou chamar esse método na ação do botão escolher foto. Dentro desse método eu vou começar a criar o meu menu, que é um UIAlertController. E vou passar um título e uma mensagem nesse menu.

[01:31] O título vai ser “Seleção de foto”. E a mensagem que eu vou colocar nesse menu será “Escolha uma foto da biblioteca”, let menu = UIAlertController(title: “Seleção de Fotos”, message: “Escolha uma foto da biblioteca”, preferredStyle: UIAlertController.Style).

[01:49] E é muito importante o tipo desse menu. Nós temos um actionSheet, que é esse menu que vamos utilizar que sobe, aparecendo de baixo para cima. Ou nós temos o Alert, que aparece geralmente no meio da tela. Nesse caso nós vamos optar pelo actionSheet.

[02:07] Depois que nós criamos o menu vamos adicionar algumas opções nele, que são na verdade os botões, as ações que esse menu vai ter. Então vou fazer menu.addAction, e vou inicializar esse UIAlertAction, passando um título.

[02:24] A primeira opção vai ser “Biblioteca de fotos”, o estilo será o default e esse handler é uma closure, onde eu posso nomear esse primeiro parâmetro, e vou colocar, por exemplo, action. Mas o que importa é o que faremos dentro dele.

[02:48] Vai ser disparado quando eu selecionar uma opção no menu. Então eu cliquei em cima de “Biblioteca de fotos”. Tudo que eu implementar aqui será chamado.

[03:03] Vamos começar fazendo algumas verificações. A primeira é se temos acesso, se temos o recurso da biblioteca de fotos, igual nós fizemos com a câmera, em que nós fizemos uma validação para verificar se existe o recurso.

[03:24] Nós fizemos o if na home. Se tivermos o recurso da câmera disponível nós fazemos o que precisamos. E faremos a mesma coisa agora. Faremos essa validação para verificar se existe esse recurso.

[03:43] Então if UIImagePickerController.isSourceTypeAvailable. Nesse caso, em vez da câmera vamos usar a biblioteca de fotos: if UIImagePickerController.isSourceTypeAvailable(.photoLibrary). Se tivermos esse recurso disponível vamos implementar a chamada para a biblioteca de fotos.

[04:05] Continuaremos utilizando a classe da câmera para essas responsabilidades de tirar e escolher foto. Dessa forma conseguimos extrair um pouco dessa lógica do View Controller, para não deixar o View Controller massivo, e deixamos isso numa classe específica. Vamos mexer nessa classe Camera daqui a pouco. E vamos chamar então o método que nós vamos criar.

[04:34] Eu vou precisar ter acesso à câmera, então já vou criar o atributo: private lazy var camera = Camera().

[04:43] Lembrando que esse lazy é uma variável preguiçosa, ou seja, essa variável só vai ser instanciada quando ela for utilizada. Isso ajuda no gerenciamento de memória.

[04:56] E eu também vou criar uma variável que vai ser o gerenciador de imagem. O nome que nós demos foi “controladorDeImagem”, então vai ficar private lazy var controladorDeImage = UIImagePickerController(). Temos já essas duas variáveis, então agora podemos utilizar dentro do nosso menu.

[05:30] A ideia é implementarmos um novo método na classe da câmera, onde nós vamos chamar a biblioteca. O nome desse método vai ser abrirBibliotecaFotos, e eu vou precisar receber por parâmetro o UIView Controller, porque eu quero exibir essa galeria de fotos. E eu também vou precisar novamente do image picker, que é o UIImagePickerController:

[06:04] Nós vamos fazer algumas configurações parecidas com o método abrir câmera. Por exemplo, vamos settar o imagePicker.delegate. Vamos permitir edição na foto, então imagePicker.allowsEditing = true.

[06:19] E o mais importante, é essa linha sourceType, onde configuramos como câmera, mas agora queremos acessar a biblioteca, então imagePicker.sourceType = .photoLibrary.

[06:30] Depois disso podemos chamar o Controller, que nós estamos recebendo o parâmetro, e vamos chamar o método present, onde vamos passar o imagePicker de forma animada, e no completion não vamos fazer nada.

[06:48] Com isso vamos voltar então no recibo e utilizar a variável câmera que nós utilizamos. Vamos começar citando o delegate, e depois vamos abrir a biblioteca de fotos. Então precisamos passar um controller, que é o próprio View Controller, e o imagePicker, que é o controladorDeImagem.

[07:12] Então fizemos uma configuração inicial. Ele está reclamando porque nós estamos dentro de uma closure, então precisamos referenciar as variáveis com self.

[07:24] E eu vou rodar então no simulador para fazermos o nosso primeiro teste. Ele está reclamando porque implementamos o protocolo de delegate, mas nós ainda não implementamos no View Controller, então vamos fazer isso: extension ReciboViewController: CameraDelegate. E dentro passamos o método didSelectFoto:

[07:56] Vou rodar o projeto para fazermos então nosso teste e verificar se precisamos fazer mais alguma configuração ou se só essa configuração inicial já basta para acessarmos a biblioteca de fotos. Então vamos dar uma olhada.

[08:15] Já buildamos o app, vou entrar em recibos e clicar no ícone da câmera. RepareNote que nós não temos uma ação porque não exibimos o menu que nós criamos. Então temos que chamar o present(menu, animated: true, completion: nil).

[08:46] Vou rodar e subir o simulador mais uma vez para fazermos o teste. Vou entrar na aba de recibos, clicar no ícone da câmera, clicar em “Biblioteca de fotos” e por enquanto nós não temos ainda acesso à biblioteca de fotos.

[09:05] Nós precisamos pedir a permissão do usuário mais uma vez. Para ter acesso à biblioteca nós precisamos pedir a permissão do usuário. Nós já fizemos isso e vamos configurar novamente a seguir.

@@03
Escolhendo foto da biblioteca

[00:00] Continuando, vamos novamente configurar a permissão no “info.plist”. Lembrando que vários recursos do iOS precisam de permissão do usuário para que consigamos acessar, como localização, câmera, push, enfim. Todos os recursos que precisemos acessar do usuário nós precisamos de permissão.
[00:27] Então vou clicar no botão de mais, onde vou adicionar mais uma permissão. E quando eu começo a digitar “Privacy”, note que surge uma lista com vários tipos de permissão.

[00:42] A que eu vou utilizar vai ser a permissão de acesso a foto, então “Privacy – Photo Library Additions Usage Description”, que é a permissão que nós precisamos. Eu vou basicamente utilizar uma mensagem parecida: “Alura Ponto necessita de acesso à biblioteca de imagens”.

[01:22] Com isso, voltamos no View Controller e vamos aproveitar também para criar mais uma opção para o nosso menu. Até agora nós temos a opção de acesso à biblioteca de fotos. Vamos criar o botão “Cancelar” também.

[01:38] Então vou adicionar uma ação, cujo tipo será destrutivo, e na closure não vou passar nada, porque não queremos fazer nada quando o usuário clicar no botão “Cancelar”: menu.addAction(UIAlertAction(title: “Cancelar”, style: .destructive, handler: nil)).

[02:06] Vou rodar o aplicativo mais uma vez. Eu vou, inclusive apagar ele do simulador. Clico e seguro no ícone, depois clico em “Deletar”. E vou fazer mais um build. Vamos testar essa implementação. Vou clicar no View Controller de recibo e no ícone da foto.

[02:32] Já temos o nosso menu de seleção de fotos. Eu vou clicar na "biblioteca de fotos" e então nós já temos permissão para uso das fotos. O que nós precisamos fazer agora é, ao escolher uma foto, setar essa imagem nessa View de fundo.

[02:54] Quando escolhermos uma foto ele vai trazer para esse método didSelectFoto, que é o método de delegate que é disparado quando nós escolhemos a foto.

[03:07] Nós precisamos pegar a foto selecionada e utilizar esse outlet que nós temos, que é fotoPerfilImageView, onde nós vamos setar a foto que o usuário selecionou.

[03:23] Eu vou fazer fotoPerfilImageView.image = image. Vou rodar mais uma vez e entrar no simulador para testarmos. Vou clicar em “Recibo > Biblioteca de Fotos”. Vou escolher uma foto, clico em “Escolher”.

[03:48] Temos um ajuste para fazer, primeiro para a imagem ocupar todo o espaço disponível. Repara que ficou um corte em cima e embaixo da foto de perfil. Então vou entrar no recibo e vou selecionar o “Image View”. E vamos então utilizar a propriedade de “Content Mode”.

[04:14] No menu lateral direito temos selecionada a opção “Aspect Fit”. Vamos mudar para “Aspect Fill”, que é a propriedade que preenche a imagem com o espaço disponível. Então temos um zoom na imagem para que ela ocupe todo o espaço.

[04:35] O segundo ajuste a fazer é pegar o Outlet do botão, que é escolhaFotoButton e agora vamos ter que tirar a imagem de fundo, porque temos uma câmera.

[04:55] Então vou pegar o método setImage e passar um UIImage sem nenhum nome, ou seja, uma imagem vazia, no caso. Vamos fazer esse teste. Vou rodar o simulador, e deveria sumir aquele ícone de câmera quando selecionamos uma imagem da biblioteca.

[05:19] Vou clicar no ícone da câmera, entrar na biblioteca de fotos, selecionar uma foto e clicar em “Escolher”. E agora temos a nossa imagem ocupando todo o espaço.

[05:33] O que podemos fazer, ao invés de tirar o ícone, que ainda continua aparecendo, é bloquear o acesso ao botão. Então podemos ocultá-lo depois que o usuário selecionar a foto. Então vou fazer escolhaFotoButton.isHidden = true.

[05:55] Vamos fazer esse último teste. Vou subir o simulador de novo, entrar na biblioteca de foto, selecionar uma imagem, e agora sim nós temos então a nossa imagem setada no Image View.

[06:20] Essa é uma forma super simples de utilizarmos a biblioteca de fotos, e é muito usual em vários aplicativos de cadastro de usuário, em que o usuário precisa colocar uma foto de documento ou algo do tipo. E precisamos manejar essas imagens dentro do app. Então aprendemos a tirar foto e a acessar a biblioteca.

[06:43] Agora precisamos continuar com as implementações, colocando os recibos e persistindo-os localmente no nosso device.

@@04
Biblioteca de fotos do iOS

Em formulários de cadastro, em que precisamos inserir uma foto, é comum ter a funcionalidade da câmera. Porém não são todos os usuários que utilizam esse recurso. É recomendado disponibilizar, além da câmera, a biblioteca de imagens do iOS, assim, o usuário consegue escolher uma foto que ele já tirou anteriormente.
O que precisamos implementar para acessar a biblioteca de fotos?

Precisamos ter acesso aos métodos do protocolo UIImagePickerControllerDelegate, pois, a partir dele, conseguimos alterar o sourceType.
 
O protocolo UIImagePickerControllerDelegate possui vários métodos, entre eles, o que utilizamos para recuperar a foto tirada com a câmera.
Alternativa correta
É através da classe UIImagePickerControllerDelegate que setamos a opção 'photoLibrary'.
 
UIImagePickerControllerDelegate é um protocolo utilizado para acessar os métodos de delegate da classe UIImagePickerController.
Alternativa correta
Precisamos ter acesso à classe UIImagePickerController para mudar o sourceType para 'photoLibrary'.
 
Alternativa correta! Através da classe UIImagePickerController, conseguimos mudar o conteúdo de exibição para biblioteca.
Alternativa correta
Precisamos criar outra variável do tipo UIImagePickerController. Uma serve para câmera e, a outra, para biblioteca de fotos.
 
Não é necessário ter duas variáveis do mesmo tipo para alterar a funcionalidade.

@@05
Faça como eu fiz: Implementando a seleção de fotos

Neste capítulo, utilizamos a classe UIImagePickerController para selecionar fotos da biblioteca de imagens do iOS. Para fazer isso, alteramos o sourceType para .photoLibrary.
Além disso, como criamos uma classe para centralizar toda lógica de manipulação de fotos/biblioteca, precisamos de alguma forma devolver o conteúdo selecionado pelo usuário para o ViewController. Como podemos fazer isso?

Um dos padrões de projeto (design patterns) mais utilizado em iOS é o delegate. Através dele, definimos um protocolo que deve ser implementado no controller que receberá a foto e, também, uma variável com o tipo do protocolo para que o ViewController assine:
Classe CameraCOPIAR CÓDIGO
protocol CameraDelegate: AnyObject {
    func didSelectPhoto(_ foto: UIImage)
}COPIAR CÓDIGO
Em seguida, precisamos da variável delegate:

class Camera: NSObject {

    weak var delegate: CameraDelegate?
   ...
   ...
   ...COPIAR CÓDIGO
E, por último, devemos implementá-lo no ViewController:

func tentaAbrirCamera() {
        if UIImagePickerController.isSourceTypeAvailable(.camera) {
            camera.delegate = self
            camera.tirarFoto(self, controladorDeFoto)
        }

}COPIAR CÓDIGO
extension HomeViewController: CameraDelegate {
    func didSelectPhoto(_ foto: UIImage) {
        // Aqui podemos manipular a foto selecionada
    }
}

@@06
O que aprendemos?

Nesta aula, aprendemos sobre:
Implementação da classe UIImagePickerController:
O tipo SourceType.photoLibrary fornece, aos dispositivos, o uso da biblioteca de imagens.
Para exibir a tela de seleção de foto ou câmera, você pode utilizar o método present do ViewController.