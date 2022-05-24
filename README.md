<h1 align="center">Chat Web</h1>

<p align="center">Chat desenvolvido com apenas para envio de mensagens.</p>

<img src="https://img.shields.io/static/v1?label=licnese&message=MIT&color=blue&style=<STYLE>&logo=<LOGO>">
<img src="https://img.shields.io/static/v1?label=npm&message=8.10.0&color=blue&style=<STYLE>&logo=<LOGO>">
<img src="https://img.shields.io/static/v1?label=socket.io&message=4.5.1&color=<COLOR>&style=<STYLE>&logo=<LOGO>">
<img src="https://img.shields.io/static/v1?label=jquery.js&message=3.6.0&color=<COLOR>&style=<STYLE>&logo=<LOGO>">

<p align="center">
 <a href="#comousar">Como usar</a> •
 <a href="#comousar">Sobre</a> •
 <a href="#tecnologias">Tecnologias</a> •
 <a href="#contribuicoes">Contribuiçoõs</a> •
 <a href="#license">Licença</a> •
 <a href="#autor">Autor</a>
</p>

<h2 id="comousar">Como usar</h2>

<p>Antes de poder botar a mão no código, precisamos ter instalado o <a href="https://nodejs.org/en/download/">nodejs</a>, porque é com ele que iremos rodar nossa aplicação no back-end. O editor de código não precisar ser o vscode, mas recomendo ele por ser bem completinho.</p>

<p>Depois de ter baixado você da um: <strong>node -v</strong>, isso irá mostra qual a versão do node e também para ter certeza de que foi tudo bem com a instalação.</p>

<p>Com o editor de codigo aberto você vai abrir o terminal e digitar o código abaixo. 👇</p>

```node
npm i ejs express socket.io 
```

<p>Esse cócdigo é para as instalações das bibliotecas que iremos ultilizar na nossa aplicação.</p>

<h4>Bibliotecas</h4>

O *ejs* é o template engine padrão do node.

O *express* é o nosso framework do node.

O *socket.io* é o nosso meio de comunicação que iremos utilizar entre o Front e Back da aplicação.

<h2 id="sobre">Sobre</h2>

<p>Depois dessa conf basica vamos iniciar o projeto criando um arquivo <strong>server.js</strong> na raiz do projeto.</p>

<p>Dentro do arquivo .js vamos começar a importar as bibliotecas. 👇</p>

```js
// Aqui importamos as bibliotecas baixadas com npm
const express = require('express')
const path = require('path')
```

<p>E agora vamos começar a criar o nosso app do express.</p>

```js
const app = express() // Criando o app do express
```

<p>Agora nesse app eu preciso conectar informar para ele que, ele tera uma porta que vai ser acessada pelo o web socket que, ele é um novo protocolo, igual ao nosso que temos um metodo http, a gente tem o protocolo wss que vai ser acessada pelo o web socket.</p>

<p>Vamos precisar definir imformar o web socket, e para poder imformar vamos precisar definir o protocolo http.</p>

```js
const server = require('http').createServer(app) // Definindo o protocolo http
```

<p>E agora vamos definir o protocolo wss para o web socket.</p>

```js
const io = require('socket.io')(server) // Definindo o protocolo WSS
```

<p>Agora já temos os protocolos http e web socket configurados.</p>

<p>Depois de ter configurado, vamos definir a nossa pasta aonde irá ficar nossos arquivos publicos acessados pela aplicação.</p>

```js
app.use(express.static(path.join(__dirname, 'public')))
```

<p>Depois de ter criado a pasta, vamos fazer mais algumas configuraçÕes para ele entender que vamos utulizar as views como html.</p>

<p>Por padrão no node ele utiliza o ejs.</p>

```js
app.set('views', path.join(__dirname, 'public')) // Aqui definimos aonde vai ficar as nossas views
app.engine('html', require('ejs').renderFile) // Agora definimos a engine como html
app.set('view engine', 'html') // Aqui já podemos utilizar html para nossas views aqui do chat
```

<p>Agora vamos fazer uma função para quando ele acessar o endereço do servidor padrão, a gente vai poder renderizar a view chamada <strong>index.html</strong>.</p>

```js
app.use('/', (req, res) => {
    res.render('index.html')
})
```
<p>Assim que você criar o arquivo .html dentro ta pasta public, já podemos chamar o endereço da aplicação. Ele vai ficar ouvindo na porta em que colocamos.</p>

```js
server.listen(3050)
```
<p>Agora que terminamos de configurar o JavaScrip para renderizar o chat, vamos iniciar com o arquivo .html que é nossa view.</p>

```html
<!DOCTYPE html>
<html lang="PT-br">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat - Ciência da Computação</title>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="styles/css/style.css">
</head>
<body>
</body>
</html>
```
<p>Essa é a estrutra básica do html, na parte do head já está com o link do css e da google fonts onde peguei um estilo de fonte mais bonito para a aplicação.</p>

```html
<!DOCTYPE html>
<html lang="PT-br">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat - Ciência da Computação</title>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="styles/css/style.css">
</head>
<body>

    <form autocomplete="off" id="chat">
        <h2>Chat Web - Ciência da Computação</h2>        
        <div class="input">
            <input type="text" required name="username">
            <label>Usuário</label>
        </div>
        <div class="messages"></div>
        <div class="flex">
            <input class="di-message" type="text" name="message" placeholder="Digite sua mensagem">
            <button type="submit"><i class="icon fa fa-send"></i></button>
        </div>
    </form>
</body>
</html>
```

<p>Aqui vamos colocar tudo dentro de um form que irá servir de base para o nosso chat. Botamos alguns inputs para o usuário poder digitar o nome e iniciar a conversar e um botão para envio da mensagem.</p>

```html
<!DOCTYPE html>
<html lang="PT-br">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat - Ciência da Computação</title>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="styles/css/style.css">
</head>
<body>
    <form autocomplete="off" id="chat">
        <h2>Chat Web - Ciência da Computação</h2>        
        <div class="input">
            <input type="text" required name="username">
            <label>Usuário</label>
        </div>
        <div class="messages"></div>
        <div class="flex">
            <input class="di-message" type="text" name="message" placeholder="Digite sua mensagem">
            <button type="submit"><i class="icon fa fa-send"></i></button>
        </div>
    </form>

    <script src="https://kit.fontawesome.com/23cfd476d0.js" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script> <!-- Link do jquery -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.5.1/socket.io.js"></script>
</body>
</html>
```

<p>Depois de termos feito a parte visual, agora a gente bota os links das bibliotecas que iremos usar.</p>

```node
node server.js
```

<p>Assim que você estiver feito essa parte vamos querer ver como que está ficando nossa aplicação. Então vamos ter que roda esse codigo no nosso terminal e deixar ele rodando para podermos ter o acesso na porta.</p>

<p>Para ver como ele está ficando, é só por o endereço que definimos lá em cima.</p>

```web
localhost:3000
```

<p>Mas ele ainda não está enviando a mensagem.</p>

<p>Para ele poder enviar as mensagens com os nomes dos usuários, vamos ter que configurar para quando um novo usuário acessar a nossa aplicação.</p>

```js
io.on('connection', socket => {
    console.log(`Socket conectado: ${socket.id}`)
})
```

<p>Aqui temos uma mensagem que será disparada toda vez que um usuário entrar ou atulizar a página. Mas para enviar as mensagens, teremos que fazer mais algumas configurações.</p>

<p>No arquivo .html antes de fechar o body, vamos conectar o nosso back ao front e como estamos utilizando a mesma linguagem podemos usar a mesma url.</p>

```js
<script>
      var socket = io('http://localhost:3000') //O io é usado através do link da biblioteca do socket.io
</script>
```

<p>Agora a gente precisa reiniciar e conectar com o back novament, e ver se ele está conectando com o socket, quando a gente redenriza a página.</p>

<p>Rode o código no seu terminal.</p>

```node
node server.js
```
<p>Depois de ter feito toda essa parte e aparecer que foi conectado vamos para a parte de envio de mensagens.</p>

```js
<script>
var socket = io('http://localhost:3000')

$('#chat').submit(function(event) {
	event.preventDefault()

	var author = $('input[name=username]').val()
	var message = $('input[name=message]').val()

	if(author.length && message.length) {
		var messageObject = {
			author: author,
			message: message
		}
		socket.emit('sendMessage', messageObject)
	}
})
</script>
```

<p>Aqui iremos fazer uma verificação de quando o chat for enviado(subimit), vamos receber uma função com um parâmetro(event).</p>

<p>Logo a baixo vamos dar um evento para não enviar esse formulário.</p>

<p>Agora vamos pegar o username e colocar dentro de uma variavel, vamos fazer a mesma coisa para o message.</p>

<p>E vamos fazer uma verificação simples para ver se o usuário digitou tanto o nome como a mensagem. Dentro do if vamos criar um objeto para não ficarmos presos em somente em enviar: strings ou inteiros, a gente pode enviar arrays inteiros ou objetos entre servidor front-end via web socket.</p>

<p>E logo depois vamos criar um evento que sera chamado lá no back-end.</p>

```js
io.on('connection', socket => {
    console.log(`Socket conectado: ${socket.id}`)
	socket.on('sendMessage', data => {
		console.log(data)
	})
})
```

<p>Aqui iremos fazer a chamada do evento criado la no front-end, reinicie seu servidor e envie uma mensagem. Se apareceu no seu terminal o nome do usuário e a mensagem está tudo ok.</p>

```js
let messages = []
```

<p>Aqui vamos criar um array que ira armazenar as mensagens, como não estamos utilizando um banco de dados em mongo, não temos uma rede e uma estrutura de armazenamento, vamos utilizar um array mesmo.</p>

```js
io.on('connection', socket => {
    console.log(`Socket conectado: ${socket.id}`)
	socket.on('sendMessage', data => {
		messages.push(data)
	})
})
```
<p>Agora aqui dentro quando recebemos uma mensagem vamos fazer o seguinte colocamos .push e esse array ira guardas todas as mensagens aqui dentro.</p>

<p>Mas mesmo com isso ele ainda não renderiza a mensagem dentro da tela, do usuário que enviou.</p>

```js
<script>
var socket = io('http://localhost:3000')

function renderMessage(message) {
	$('.messages').append('<div class="message"><strong>'+ message.author +'</strong>: <span>'+ message.message +'<span></div>')
}

$('#chat').submit(function(event) {
	event.preventDefault()

	var author = $('input[name=username]').val()
	var message = $('input[name=message]').val()

	if(author.length && message.length) {
		var messageObject = {
			author: author,
			message: message
		}

		renderMessage(messageObject)

		socket.emit('sendMessage', messageObject)
	}
})
</script>
```

<p>Vamos criar uma função que vai receber uma mensagem, que vai renderizar ela em tela. Agora utilizando o jquery pegando a message colocando um evento nela para poder falar quem que é o autor e a mensagem digitada.</p>

<p>Então vamos chamar a, nossa função e ver se está redenrizando os envios. Porém se abrirmos em outra aba, ela não aparece as mensagens enviadas e se atulizar a pagina ela perde todos os envios.</p>

```js
io.on('connection', socket => {
    console.log(`Socket conectado: ${socket.id}`)
	socket.on('sendMessage', data => {
		messages.push(data)
	})
})
```

<p>É aqui no nosso server quando a gente faz messages.push com a nova mensagem(data), em nenhum momento a gente está retornando alguma coisa para o front-end uma informação para o front-end, de que essa mensagem foi recebida no servidor e tem uma nova mensagem para o front-end mostrar em tela.</p>

```js
io.on('connection', socket => {
    console.log(`Socket conectado: ${socket.id}`)

    socket.on('sendMessage', data => {
        messages.push(data)
        socket.broadcast.emit('receiveMessage', data)
    })
})
```

<p>E o que a gente faz é, o socket tem 3 eventos são: emit -> para enviar uma mensagem somente para esse socket, on -> que usamos para ouvir uma mensagem e o broadcast.emit -> o broadcast enviara para todos os sockets conectados na aplicação.</p>

```js
<script>
	var socket = io('http://localhost:3000')

	function renderMessage(message) {
		$('.messages').append('<div class="message"><strong>'+ message.author +'</strong>: <span>'+ message.message +'<span></div>')
	}

	socket.on('receiveMessage', function(message) {
		renderMessage(message)
	})

	$('#chat').submit(function(event) {
		event.preventDefault()

		var author = $('input[name=username]').val()
		var message = $('input[name=message]').val()

		if(author.length && message.length) {
			var messageObject = {
				author: author,
				message: message
			}

			renderMessage(messageObject)

			socket.emit('sendMessage', messageObject)
		}
	})
</script>
```
<p>Agora aqui no front precisamos ouvir a chamada do back, ai fazenmos uma função para receber o nosso objeto com o autor e a mensagem, dai precisamos apenas chamar nossa função de antes(renderMessage), passando nossa mensagem(message).</p>

<p>Reinicie o server do node e é só testar para ver se tudo está dando certo.</p>

<p>Mas ainda temos um problema, quando atualizamos nossa página ele perde as mensagens.</p>

```js
let messages = []

io.on('connection', socket => {
    console.log(`Socket conectado: ${socket.id}`)

    socket.emit('previousMessages', messages)

    socket.on('sendMessage', data => {
        messages.push(data)
        socket.broadcast.emit('receiveMessage', data)
    })
})
```

<p>Como já temos esse array que está armazenando todas as mensagens, assim que um socket for conectado na nossa aplicação, a gente pode enviar uma mensagem só para ele, dai n iremos mais usar o broadcast, então eu vou enviar todas as mensagens assim que ele entrar na aplicação. Agora vamos ouvir esse evento la no nosso front-end.</p>

```js
<script>
	var socket = io('http://localhost:3000')

	function renderMessage(message) {
		$('.messages').append('<div class="message"><strong>'+ message.author +'</strong>: <span>'+ message.message +'<span></div>')
	}

	socket.on('previousMessages', function(messages) {
		for(message of messages) {
			renderMessage(message)
		}
	})

	socket.on('receiveMessage', function(message) {
		renderMessage(message)
	})

	$('#chat').submit(function(event) {
		event.preventDefault()

		var author = $('input[name=username]').val()
		var message = $('input[name=message]').val()

		if(author.length && message.length) {
			var messageObject = {
				author: author,
				message: message
			}

			renderMessage(messageObject)

			socket.emit('sendMessage', messageObject)
		}
	})
```

<p>Então vamos chamar ele aqui no front, passar uma função com um array de messages, podemos pecorrer esse array utilizarando um for, então ele vai pecorrer cada uma dessas mensagens aqui. E chamar a função de antes com as mensagens.</p>

<p>Reinicie seu node e pronto ele vai estar redenrizando para todos os sockets conectados na aplicação.</p>

<p>Uma observação ele não ira ficar salvo porque não temos uma estrutura como uma do mongoDB e mySQL salvando essas mensagens por trás essas menssagens.</p>

<h4 align="center"> 
	<img src="" alt="Imagem da interface do chat">
</h4>

<section id="tecnologias">

<h2>Tecnologias</h2>

<h3>Front-end</h3>
<p>HTML5</p>
<p>CSS3</p>
<p>JavaScript</p>

<h3>Back-end</h4>
<p>Node.js</p>

<h3>Bibliotecas</h3>
<p>socket.io</p>
<p>express</p>
<p>ejs</p>

</section>

<h3 id="contribuicoes">Contribuições</h3>

<img src="" alt="foto de peril"> Robert Barbosa

<img src="" alt="foto de peril"> Mateus Alfaia
<img src="" alt="foto de peril"> Lucas
<img src="" alt="foto de peril"> João


<h2 id="autor">Autor</h2>

<img src="#" alt="foto de perfil" /> Thiago Barreto R.


<h3 id="license">Licença</h3>

Este projeto esta sobe a <a href="./license">licença MIT</a>.

Feito com :heart: por mim e minha equipe de estudo.
