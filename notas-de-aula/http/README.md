# HTTP: Entendendo a web por debaixo dos panos

## Conteúdos

- [O que é HTTP?](#o-que-é-http)
- [A versão segura do HTTP](#a-versão-segura-do-http)
- [Funcionamento do HTTPS](#funcionamento-do-https)
- [Chaves Assimétricas e Simétricas](#chaves-assimétricas-e-simétricas)
- [Endereços sob o seu domínio](#endereços-sob-o-seu-domínio)
  - [Conceitos vistos](#➜-conceitos-vistos)
- [Modelo Requisição e Resposta](#modelo-requisição-e-resposta)
- [Conceitos vistos](#➜-conceitos-vistos)
- [Web Service](#web-service)
- [MIME types (tipo/subtipo)](#mime-types-tiposubtipo)
- [Serviços REST (Representational State Transfer)](#serviços-rest-representational-state-transfer)
- [HTTP2 - Dados binários, GZIP ativo e TLS](#http2---dados-binários-gzip-ativo-e-tls)
- [Headers Stateful](#headers-stateful)
- [Server Push](#server-push)
- [Multiplexação](#multiplexação)
- [Keep-Alive no HTTP2](#keep-alive-no-http2)

## O que é HTTP?

A primeira coisa que nos vem a mente quando falamos sobre HTTP é a 
utilização da internet, então, precisamos entender primeiro o que é 
aquela URL passada e que dados podemos passar também.

Exemplo, quando nos conectamos com o site da alura, precisamos de uma 
internet ativa e um navegador para podermos interagir com tal plataforma 
e qualquer outro site da web. Acontece, que nessa comunicação temos o 
modelo cliente-serviço (**Client-Server**), nesse modelo de comunicação 
existem várias regras que tem que ser bem definidas, porque precisamos 
que ambos os lados entendam as mesmas informações, então nosso navegador 
(cliente) vai enviar dados, que o servidor (site da Alura, por exemplo) 
deverá está pronto pra entender, o mesmo vale ao contrário, quando nosso 
servidor ou aplicação web devolver uma resposta, o navegador tem que 
saber interpretar, por isso precisamos que esses dois mundos utilizem 
o mesmo canal de comunicação com as mesmas regras. 

E quando falamos de regras de comunicação no mundo web, estamos falando 
do **protocolo HTTP**, ou seja, um conjunto de regras para determinar 
como irá ser nossa comunicação (**requisição e resposta**).

## A versão segura do HTTP

Quando trabalhamos com requisição, nosso navegador pode enviar dados 
para serem recebidos pelo servidor, mas até chegar de fato na aplicação, 
podemos ter N intermediários, quando trabalhamos com o mundo web, temos 
uma camada de roteador, então ela chega no roteador da sua casa, depois 
pode ir para o modem, do modem foi para o provedor, para o firewall e 
por aí vai. 

Inclusive, isso pode se tornar perigoso, pois o HTTP trafega texto puro, 
então nada garante que ninguém verá essas informações. Portanto, existe 
uma versão do HTTP que é o **HTTPS**, que nada mais é que todos os 
protocolos do HTTP, mas com uma camada de segurança que é o SSL 
(**Secure Sockets Layer**) ou TSL (**Transport Layer Security**), que 
é a versão mais nova dessa camada.

## Funcionamento do HTTPS

Para que uma página se torne segura e que o browser confie nesse 
protocolo HTTPS que estamos usando, é preciso que tenhamos uma identidade 
confirmada. No mundo web, isso é chamado de **Certificado digital** e 
este, possui uma chave que vai criptografar os dados que o navegador 
enviar para o servidor. Então, com essa chave pública, iremos conseguir 
criptografar os dados, e no lado do servidor, a aplicação terá uma chave 
privada, que apenas ela conhece e irá conseguir descriptografar esses dados.

Então, resumindo, o navegador tem um certificado digital, que possui a 
chave pública que servirá para encriptografar os dados que saem de nossas 
máquinas. Eles são enviados e apenas são descriptografados na aplicação 
em questão que terá a *chave privada*! Estabelecendo assim, um tráfego 
de dados seguro.

### Chaves Assimétricas e Simétricas

Aprendemos que o HTTPS usa uma chave pública e uma chave privada. As 
chaves estão ligadas matematicamente, o que foi cifrado pela chave 
pública só pode ser decifrado pela chave privada. Isso garante que os 
dados cifrados pelo navegador (chave pública) só podem ser lidos pelo 
servidor (chave privada). Como temos duas chaves diferentes envolvidas, 
esse método de criptografia é chamado de **criptografia assimétrica**. 
No entanto, a criptografia assimétrica tem um problema: ela é lenta.

Por outro lado, temos a **criptografia simétrica**, que usa a mesma 
chave para cifrar e decifrar os dados, como na vida real, onde usamos 
a mesma chave para abrir e fechar a porta. A criptografia simétrica é 
muito mais rápida.

Agora, o interessante é que o HTTPS usa ambos os métodos de criptografia, 
assimétrica e simétrica, ou seja, no certificado, vem a chave pública 
para o cliente utilizar e o servidor continua na posse da chave privada. 
Isso é seguro, mas lento e por isso o cliente gera uma chave simétrica 
ao vivo, para ele e para o servidor com o qual está se comunicando 
naquele momento! 

Essa chave exclusiva (e simétrica) é enviada para o servidor utilizando 
a criptografia assimétrica (chave privada e pública) e por fim, é 
utilizada para o restante da comunicação.

Portanto, HTTPS começa com criptografia assimétrica para depois mudar 
para criptografia simétrica. Essa chave simétrica será gerada no início 
da comunicação e será reaproveitada nas requisições seguintes afim de 
um tráfego otimizado.

## Endereços sob o seu domínio

Domínios são nomes dados a sites na web, para que o usuário não precise 
lembrar do seu IP. Esses nomes são registrados no DNS (**Domain Name System**), 
que dá ao navegador o endereço de IP relacionado a determinado nome ou 
domínio que vemos em URLs de sites.

### ➜ Conceitos vistos

- URL são endereços na web;
- Uma URL começa com o protocolo (http://) seguido pelo domínio 
(www.alura.com.br);
- Após o domínio, é especificado o caminho para um recurso 
(/course/introducao-html-css);
- Um recurso é algo concreto que queremos acessar;

## Modelo Requisição e Resposta

O HTTP não guarda estado (**stateless**), quando fazemos uma requisição, 
a seguinte não sabe o que foi feito em momentos anteriores. Cada requisição 
é única na web.

Então, por exemplo, como nós podemos deslogar da plataforma e a Alura 
consegue manter as informações dos usuários:

Quando fazemos o login, enviamos o formulário preenchido com os dados 
necessários, a Alura verifica se essas credenciais estão corretas e 
então gera uma identificação para nós e devolve para o navegador, para 
este, quando fizer novas requisições, mandar de volta essa identificação 
a cada requisição para o servidor da Alura estar adiantando essas 
informações e saber que você está ativo/logado no site.

Esse é um conceito bastante utilizado na web que é a **sessão**, é a 
maneira que conseguimos lidar com os usuários logados e não só para 
autenticação, mas para guardar informações também. E a sessão só é 
implementada através da ideia de guardar no nosso navegador uma espécie 
de **Cookie**, que é um par de chave-valor.

Quando falamos de Cookies, na verdade queremos dizer **Cookies HTTP** 
ou **Cookie web**. Um cookie é um pequeno arquivo de texto, normalmente 
criado pela aplicação web, para guardar algumas informações sobre usuário 
no navegador. Quais são essas informações depende um pouco da aplicação. 
Pode ser que fique gravado alguma preferência do usuário. Ou algumas 
informações sobre as compras na loja virtual ou, como vimos no vídeo, 
a identificação do usuário. Isso depende da utilidade para a aplicação web.

### ➜ Conceitos vistos

- O protocolo HTTP segue o modelo Requisição-resposta;
- Uma requisição precisa ter todas as informações para o servidor;
- HTTP é Stateless (não mantém informações entre requisições)
- As plataformas de desenvolviment6o usam sessões para guardar 
informações entre requisições;
- Parâmetros de requisição são usados para definir detalhes da pesquisa 
ou enviar dados de um formulário;

## Web Service

Quando falamos de um Web Service, sempre usamos o protocolo da web, ou 
seja o HTTP. Um Web Service disponibiliza uma funcionalidade na web, 
através desse protocolo. As funcionalidades variam muito e dependem muito 
da empresa e do negócio dela, mas por exemplo, na Alura temos um Web 
Service que traz todas as informações de um curso (nome, capítulos, 
exercícios, etc). O Google ou Facebook possuem muitos Web Services para 
acessar um usuário, ver os posts dele, interesses, etc. Muitas vezes 
esses serviços são pagos. O importante é que sempre usamos o protocolo 
HTTP. A grande diferença de um Web Service é que os dados não vem no 
formato HTML, e sim em algum formato independente da visualização, como 
**XML** ou **JSON**.

## MIME types (tipo/subtipo)

- **alguns tipos:** text, image, application, audio, video;
- **alguns subtipos:**
  - text/plain, text/html, text/css, text/javascript;
  - image/gif, image/png, image/jpeg;
  - audio/midi, audio/mpeg, audio/webm, audio/ogg, audio/wav;
  - video/mp4;
  - application/json, application/xml,  application/pdf;

Para saber mais sobre os tipos, clique [aqui](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

## Serviços REST (Representational State Transfer)

é um padrão arquitetural para comunicações entre aplicações.

## HTTP2 - Dados binários, GZIP ativo e TLS

O protocolo que estamos trabalhando até agora foi especificado na década 
de 90 e de lá até hoje muitas alterações foram feitas até na forma como 
usamos a internet.

Com a chegada do mundo mobile novas preocupações apareceram e otimizações 
são cada vez mais necessárias para uma boa performance. Por isso uma 
mudança foi necessária e em 2015 depois de alguns anos de especificações 
e reuniões surgiu a versão 2 desse protocolo. A nova versão é batizada de 
**HTTP/2** e tem essa [documentação](https://http2.github.io/) como referência.

A nova versão do protocolo HTTP traz mudanças fundamentais para a Web. 
Recursos fantásticos que vão melhorar muito a performance da Web além de 
simplificar a vida dos desenvolvedores.

No HTTP 1.1, para melhorar a performance, habilitamos o GZIP no servidor 
para comprimir os dados das respostas. É uma excelente prática, mas que 
precisa ser habilitada explicitamente. 

No HTTP/2, o GZIP é padrão e obrigatório. Mas, se você já olhou como 
funciona uma requisição HTTP, vai notar que só GZIPar as respostas 
resolve só metade do problema. Tanto o *request* quanto o response levam 
vários cabeçalhos (*headers*) que não são comprimidos no HTTP 1.1 e 
ainda viajam em texto puro. 

Já na nova versão, os *headers* passam a ser binários. Por sua vez, os 
binários são comprimidos usando um algoritmo chamado **HPACK**. Isso 
diminui bastante o volume de dados trafegados nos headers. Além de todas 
essas otimizações para melhorar a performance ainda houve uma preocupação 
com segurança exigindo TLS por padrão também.

Apesar do protocolo HTTP/1.1 ter sido de extrema importância para a Web 
ao longo de vários anos, como toda boa tecnologia, é necessário um update. 
A nova versão do HTTP veio para adequar este protocolo tão famoso a um 
mundo onde temos muito mais dados sendo trafegados na rede, e a 
velocidade de acesso e segurança do usuário se tornam bastante 
importantes.

### Headers Stateful

A partir do HTTP/2 não precisamos mais repetir os *Headers*, os cabeçalhos 
que já enviamos em uma requisição anterior. Logo, quando fazemos uma 
requisição para o `principal.js`, onde teríamos os cabeçalhos exatamente 
iguais aos da requisição passada, nós não precisamos enviar novamente 
esses dados, apenas enviar dados novos quando forem diferentes.

### Server Push

Podemos imaginar que estamos fazendo uma requisição para uma página 
principal, a index.html. Essa requisição bate no servidor e o ele nos 
traz o conteúdo HTML. 

O HTML retornado pode ter o título Caelum, e então vai aparecer no nosso 
navegador essa informação. Além disso, temos um arquivo CSS, de estilização 
da página, que é o estilo.css, e dois arquivos JavaScript necessários para
a página ser executada, o `jquery.js` e o `principal.js`. Além disso, 
no meio do corpo do HTML, tem um recurso que é de imagem, temos a imagem 
`logo.png`. Mas além desses, podemos ter vários outros recursos na nossa 
página.

Então, ao receber esse conteúdo, o browser tem que sair fazendo requisições 
de tudo o que é necessário para que ele renderize a página. O navegador 
interpreta esse conteúdo HTML de cima pra baixo, verifica que o primeiro 
recurso necessário é o `estilo.css`, então ele vai buscar. O segundo 
recurso necessário, `jquery.js`, que é uma biblioteca JavaScript. E além 
disso, precisamos do `principal.js` e do `logo.png`.

A partir do HTTP2, isso ficou um pouco diferente. Agora temos uma 
conversa mais paralela. O servidor pode empurrar para o clientes certos 
recursos antes mesmo de serem solicitados, pois ele consegue analisar o 
HTML e ver o que mais é preciso para carregar a página fazendo com que 
não seja necessário gastar tempo pedindo todos os outros recursos.

## Multiplexação

Outra coisa importante de requisição é que temos o conceito de request 
e response. Cada requisição e cada resposta no HTTP1.1 são únicos.

"Por baixo dos panos", antes dessa requisição de fato ser feita, há 
uma conexão, comunicação entre cliente e servidor, que chamamos de TCP. 
Para que consigamos realizar uma requisição via HTTP, antes existe um 
modelo de TCP, que é um protocolo de transporte. Isso é mais a nível de 
infraestrutura, pois quando trabalhamos com desenvolvimento, acabamos 
deixando isso pra lá, já que ficamos na camada acima dessa conexão.

Queremos mostrar é que quando fazemos uma requisição, ela é única. No 
HTTP, cada requisição deveria abrir uma conexão TCP, executar e fechar.
Mas isso seria muito ruim porque conexão TCP é recurso caro, é um recurso 
que demora a ser alocado. Claro que é muito rápido a nível computacional, 
mas é mais um passo antes da requisição HTTP prosseguir e recebermos 
uma resposta. Então o que acontece, no HTTP1 existe um mecanismo chamado 
de *Keep-Alive*. 

O Keep-Alive determina quanto tempo, por exemplo, a nossa conexão pode 
ficar ativa. Ou seja, não encerra essa conexão TCP. Portanto, conseguimos 
realizar várias requisições com a mesma conexão TCP.

Hoje, na maioria dos browsers, temos um número entre 4 e 8 de conexões 
simultâneas por domínio. Significa que se fizermos uma requisição para 
a página da Caelum e a página da Caelum tiver mil recursos, o browser 
tem 4 a 8 conexões TCP ativas para conseguir realizar essas requisições 
em paralelo, e não serial. Mas isso na versão 1.1.

### Keep-Alive no HTTP2

O Keep-Alive continua existindo no HTTP2, só que ele trouxe uma novidade. 
Por exemplo, se temos uma conexão TCP aberta e realizamos uma requisição, 
poderíamos já dar prosseguimento às próximas requisições, isso em paralelo, 
sem de fato ficar esperando o resultado dela, de maneira assíncrona, e 
vamos recebendo essas respostas à medida em que o servidor for conseguindo 
processar.

Então, essas requisições e respostas vão chegando a todo tempo. É totalmente 
paralelo. A mesma coisa acontece com o servidor, não precisamos esperar uma 
resposta para enviar outra. Se já está pronta para ser enviada, ele já 
envia diretamente.

Esse conceito que surgiu no HTTP2 é chamado de **Multiplexing** e traz 
uma performance bastante relevante para o nosso HTTP.