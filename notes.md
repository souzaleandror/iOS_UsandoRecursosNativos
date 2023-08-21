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
PRÓXIMA ATIVIDADE

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
PRÓXIMA ATIVIDADE

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
PRÓXIMA ATIVIDADE

O uso da classe UIImagePickerController nos oferece a possibilidade de utilização tanto da câmera, quanto da biblioteca de imagem do iOS.
Como podemos ter acesso aos eventos de uso da câmera para tirar uma foto ou a escolha de uma imagem da biblioteca?

Opinião do instrutor

Para ter acesso aos eventos de escolha de foto, é necessário implementarmos o protocolo de delegate UIImagePickerControllerDelegate. Através dele, podemos implementar o método didFinishPickingMediaWithInfo que nos devolve informações da imagem selecionada.

@@07
O que aprendemos?
PRÓXIMA ATIVIDADE

Nesta aula, aprendemos sobre:
Implementação da classe UIImagePickerController:
A classe '''UIImagePickerController''' nos oferece o uso da câmera para tirar fotos, gravar filmes e escolher itens da biblioteca de mídia do usuário.
O tipo SourceType.Camera fornece, aos dispositivos que suportam captura de mídia, o uso da câmera ou gravação de vídeos.