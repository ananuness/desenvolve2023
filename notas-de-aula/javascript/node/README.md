# ⚙️ Node.js

## :notepad_spiral: Conteúdos

- [O que é o Node.js?](#📚-o-que-é-o-nodejs)
- [Para que é usado?](#💻-para-que-é-usado)
- [Node.js vs JavaScript](#🤝-nodejs-vs-javascript)
- [O package.json](#📦-o-packagejson)
- [O npm/yarn](#📤-o-npmyarn)

## 📚 O que é o Node.js?

O JavaScript é uma linguagem interpretada, ou seja, ela precisa de um
interpretador, para conseguir entender e rodar código js. E antes, o
navegador era o único que tinha um interprador para a linguagem, ou
seja, ele é o **ambiente original de execução do JavaScript**.

Já o Node.js é uma *engine*, ou seja, um "motor" de interpretação do
JavaScript fora do ambiente do navegador. Além disso, ele contém uma
série de recursos como bibliotecas, APIs e ferramentas que são
diferentes do navegador. De acordo com o próprio site do Node:

> "Node.js é um software de código aberto, multiplataforma, baseado no
> interpretador V8 do Google e que permite a execução de códigos 
> JavaScript fora de um navegador web. A principal característica do 
> Node.js é sua arquitetura assíncrona e orientada por eventos."

## 💻 Para que é usado?

O Node, então, existe para que o JS seja usado para outras funcionalidades
que vão além de dar comportamento as páginas do navegador. Claro, 
principalmente focado no desenvolvimento de aplicações web como APIs,
servidores web etc. Mas tem outras funções, como desenvolver *chatbots*,
*streaming* de dados, Internet das Coisas (IoT), *web scraping* dentre 
vários outros usos.

## 🤝 Node.js vs JavaScript

No JS, basicamente tudo da linguagem, todas suas funcionalidades,
bibliotecas nativas etc, é interpretado no "motor de interpretação", o
navegador. E cada um desenvolve e mantém sua *engine* de uma maneira
diferente. A **V8** roda na Google; a SpiderMonkey na Firefox e o Chromium
na Microsoft Edge.

Então, por exemplo, o método `.sort()` pode ser usado em qualquer uma
das engines, porém, a forma que o algoritmo é implementado, pode variar
bastante entre esses "motores".

E, apesar do Node ser baseado na V8 da Google, ele não tem as mesmas
bibliotecas ou APIs nativas que os navegadores têm, como é o caso da
*DOM*, mas o Node traz várias outras funcionalidades principalmente
pelo foco ser o desenvolvimento backend.

> **Curiosidade:** podemos usar o Node para desenvolver aplicações 
> inteiras, como o editor de código Atom, o "whatsapp empresarial" 
> Slack e o Postman, que é uma ferramenta que dá suporte à  documentação, 
> execução de testes de APIs e requisições em geral. 

Em resumo, a linguagem ainda é a mesma, ✨ JavaScript ✨ (pode ser
Typescript 😶‍🌫️). O que o Node faz é permitir que escrevamos em JS,
programas que rodem fora do ambiente do navegador. Então, aprender a 
programar com Node, baseia-se em aprender as funcionalidades desse
ambiente que é diferente de programar para o navegador, embora tenha
suas semelhanças.

## 📦 O package.json

O arquivo `package.json` é o coração, o *arquivo manifesto* de qualquer
projeto que utilize o Node. É nele que você encontra todas as informações
principais sobre o projeto:

- nome do projeto;
- descrição do projeto;
- versão do projeto;
- dependências;
- o arquivo que é o ponto de entrada do seu projeto;
- scripts (comandos que podemos configurar) e dentre outras informações;

## 📤 O npm/yarn

Ambos são gerenciadores de pacote, os *package managers*. Ou seja, eles
são repositórios de código, voltados para pacotes do Node e esses pacotes
vão desde bibliotecas bem restritas que fazem uma tarefa bem específica,
até os frameworks mais completos que podem ser usados com Node. E através
deles, conseguimos instalar pacotes localmente para usarmos no nosso 
projeto e todos eles ficam localizados na pasta `node_modules` e essas
dependências instaladas são listadas de maneira mais detalhada em outro 
arquivo, o `package_lock.json`, que é gerado automaticamente.

O npm já vem instalado junto com o Node.js, porém, a partir dele,
conseguimos instalar o yarn, que é outro gerenciador, com comandos um
pouco diferentes, mas na maior parte desempenham a mesma função.