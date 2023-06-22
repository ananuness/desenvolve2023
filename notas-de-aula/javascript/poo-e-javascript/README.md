# 🗂️ Programação orientada à objetos e JavaScript

## Conteúdos

- [O que são paradigmas de programação?](#o-que-sao-paradigmas-de-programacao)
- [Orientação à objetos](#orientacao-a-objetos)
- [Orientação à objetos em JS](#orientacao-a-objetos-em-js)
  - [Entendendo o this](#entendendo-o-this)
  - [Fuction vs Arrow Function](#function-vs-arrow-function)
  - [Herança de protótipo](#heranca-de-prototipo)
  - [`__proto__` vs prototype](#__proto__-vs-prototype)
  - [Cópia vs referência](#copia-vs-referencia)
  - [Object.create() vs new](#object.create()-vs-new)
  - [Estrutura de classe](#estrutura-de-classe)
  - [Herança de classe](#herança-de-classe)
  - [Encapsulamento](#encapsulamento)
  - [Polimorfismo](#polimorfismo)
  - [Interfaces](#interfaces)
- [SOLID](#solid)


## O que são paradigmas de programação?

Um paradigma de programação se baseia normalmente em alguma teoria matemática e/
ou computacional, desenvolvida para resolver determinados problemas de 
programação de determinada forma.

Cada paradigma de programação tem o seu conjunto de regras e elas cobrem a forma 
como os dados são tratados, a organização do sistema, como o código é escrito, a 
arquitetura, entre vários outros aspectos.

A programação orientada à objetos e também a programação estruturada derivam do 
paradigma imperativo. Já a programação funcional deriva do declarativo. E o 
paradigma relacional está associado à bancos de dados relacionais.

Os paradigmas imperativos são aqueles que usam afirmações para alterar o estado 
de um programa, da mesma forma como o modo verbal imperativo no português 
expressa um comando ou ordem para ser executada. Essa categoria se preocupa com 
o “como” uma tarefa vai ser executada, o seu passo-a-passo e a sequência dessas 
etapas. Alguns dos paradigmas que se encaixam aqui são os seguintes:

- Estrutural
- Procedural
- Orientado à objetos

Um exemplo que mostra o paradigma **imperativo** é a implementação da seguinte 
função que recebe um array e retorna outro array com cada um dos valores dobrado:

```js
function dobra(arr){
	let resultados = [];

  for (let i = 0; i < arr.length ; i++){
		resultados.push(arr[i] * 2);
	}

	return resultados;
}
```

Podemos notar que passamos as instruções de como percorrer o array, qual operação 
fazer e o que devemos adicionar ao resultado.

Outra categoria de paradigma é o **declarativo**. Podemos dizer que uma 
característica dele é expressar a lógica de um processo sem descrever o seu 
controle de fluxo. Ou seja, é associado ao *o que uma tarefa vai resultar ou retornar*. 
**Um paradigma que pode se encaixar nessa categoria é o paradigma funcional**. 
Uma implementação declarativa do mesmo problema de dobrar os valores de um vetor 
pode ser feita da seguinte forma:

```js
function dobra(vetor){
	return vetor.map((item) => item * 2);
}
```

Podemos observar que não foi necessário explicitar como iterar sobre o laço de 
repetição ou atribuir os novos valores. No cotidiano temos diversos outros 
exemplos de afirmações que podem ser consideradas declarativas, como arquivos HTML:

```html
<h1> Programação Declarativa</h1>
<p> 
  Estou declarando como quero que o texto apareça, e não dizendo 
  para o computador como renderizar um texto.
</p>
```

Ou até mesmo as queries SQL, nas quais apenas dizemos qual resultado esperamos, 
sem especificar como a busca deve ser feita:

```sql
SELECT * FROM alunos WHERE escola='Alura';
```

O JavaScript e algumas outras linguagens podem utilizar mais de um paradigma. É 
comum ouvir o termo "*multiparadigma*" quando nos referimos a esse tipo de 
linguagem, e isso traz alguns benefícios, pois permite perfis diferentes de 
desenvolvedores e sistemas utilizarem uma linguagem em comum. Claro que um 
paradigma não é necessariamente melhor que o outro, mas dependendo das 
circunstâncias podemos utilizar um que seja mais otimizado para determinada 
aplicação. Assim como os códigos declarativos que utilizamos podem ter uma 
implementação imperativa por baixo dos panos.

## Orientação à objetos

> "Princípio de espelhar o mundo real através de uma estrutura de objetos com 
> características e ações que interagem uns com os outros."

Então a principal ideia da orientação a objeto é 
*trazer para o código conceitos e ideias que vemos no dia a dia*, no mundo real, 
por exemplo, pegar informações de uma pessoa, pegamos as informações necessárias 
e transformamos em código. 

Outro conceito importante em orientação à objeto é o de **classe**. No JavaScript, 
os objetos criados a partir de objetos literais ou usando construtores através de 
função era a forma utilizada de trabalhar com esse paradigma, pois a sintaxe de 
classe não existia no JavaScript até o famoso ES6. 

Antes disso, para trabalharmos em com orientação à objetos, usávamos apenas 
funções e um conceito que é particular do JavaScript e a forma que ele foi pensado 
originalmente, que é o que chamamos de **herança de protótipo**.

A herança de protótipo, ao contrário da herança de classe, foi a forma como o 
JavaScript originalmente pensou em fazer modelos de objetos e passar propriedades 
de um objeto para outro.

Então na classe, define-se as propriedades que identificamos do mundo real e 
precisamos trazer para o mundo computacional para modelarmos na codificação depois. 
Por isso uma classe vai definir para nós as características que precisamos, os 
chamados **atributos**, e os comportamentos de um determinado objeto, que são os 
**métodos** que chamamos.

Herança é um mecanismo que permite a classe herdar características e comportamentos 
de uma outra classe. Logo, é um mecanismo importante que nos permite trabalhar com 
o conceito de reaproveitamento de código.

## Orientação à objetos em JS

*"Mas por que eu preciso entender a herança de protótipo, que é uma coisa do JavaScript, se foi falado que de 2015 para cá foi implementado classe e podemos fazer tudo como classe?"*

Porque no JavaScript, a classe é implementada em cima desse modelo original de 
herança de protótipo e porque a palavra-chave `this` é essencial para entendermos 
como a herança de protótipo funciona.

Além disso, tudo que é relacionado ao protótipo, por exemplo, o this, aparece para 
nós em vários momentos. Quando estudamos programação em JavaScript, mesmo que não 
estejamos fazendo nada relacionado a orientação à objetos, o this e a questão do 
protótipo ainda vão aparecer, então esse é o momento de pararmos e entendermos um 
pouco como a herança de protótipo, o this e outras palavras-chave funcionam.

### Entendendo o this

Podemos dizer que é literalmente "isso". É uma palavra que só faz sentido com 
**contexto**. Então se você falar para uma pessoa: “Eu quero isso”, a pessoa vai 
te perguntar: “Você quer o quê?”, a pessoa não vai saber. This é um termo que só 
funciona se tiver contexto atrelado a ele.

Vamos pedir para o `console.log` retornar somente *this*. Ele traz um objeto global, 
que é um objeto interno do Node, contendo todas as propriedades que são comuns a 
todos os módulos do Node.js, um objeto interno, ou seja, se não passamos para o 
this nada ligado à ele, ele traz o contexto global de onde está. Por exemplo:

```js
const user = {
  nome: 'Ana',
  idade: '23'
}

function exibirNome() {
  console.log(this.nome);
}
```

A função não sabe o nome de quem eu quero que ela traga, porque ela não tem 
nenhuma propriedade que se chame nome para ser chamado, então não tem contexto 
nenhum. Vamos dar um contexto para ela:

```js
const exibirNomeComContexto = exibirNome.bind(user);
```

O método `bind` é um método que usamos para prender a execução de uma função a 
um contexto específico, passando como parâmetro um objeto que vamos usar de 
contexto. Então, podemos executar `exibirNomeComContexto()` e o `exibirNome()`, 
para conferirmos os dois retornos. 

E agora, temos como resposta `Ana` e no segundo, `undefined`. Isso porque quando 
pedimos para executar `exibirNome`, ele está executando só essa função sem 
contexto, nos devolvendo `undefined` porque ele não encontrou a quem esse nome 
se refere.

O que estamos chamando de contexto é o objeto, no caso, o `user`, que tem uma 
propriedade nome que o JavaScript pode trazer de volta. E é por isso que 
`exibirNomeComContexto` consegue retornar um nome. 

Uma coisa interessante nesse caso é que quando passamos essa função como valor 
para dentro de uma variável, não criamos uma referência dela, e sim uma cópia e 
é por isso que `exibirNomeComContexto` e `exibirNome` são funções diferentes 
nesse momento, não interferindo uma com a outra. Porque exibirNome, no momento 
que foi passado para dentro de exibirNomeComContexto é uma nova função.

Existem outros dois métodos para manipular o contexto do this:

**call()**: executa a função passando valores e parâmetros específicos para serem 
usados como contexto do this. Ou seja, é possível atribuir um this diferente do 
contexto atual ao executar a função. Também é possível passar parâmetros para 
`call(),` como no exemplo a seguir.

Temos uma função que monta uma determinada mensagem a partir dos parâmetros nome 
e email. Se quiséssemos vincular os dados da mensagem a um objeto com dados de 
usuários, podemos usar `call()` passando como primeiro parâmetro o contexto a ser 
considerado como this (no caso, objeto user) e a partir do segundo parâmetro 
definimos quais os argumentos.

```js
function exibeMensagem(nome, email) {
 console.log(`usuário: ${nome}, email ${email}`);
}

const user = {
 nome: 'Mariana',
 email: 'm@m.com',
 executaFuncao: function(fn) {
   fn.call(user, this.nome, this.email);
 }
}

user.executaFuncao(exibeMensagem) //usuário: Mariana, email m@m.com
```

Nesse caso, a função que será executada também está sendo passada como parâmetro 
de `executaFuncao` e usamos `call()` para chamar a função com um contexto (this) 
específico e também argumentos específicos.

**apply()**: funciona de forma semelhante ao call(), porém, recebe a lista de 
argumentos em um array. Usando arrays, é possível passar os argumentos via variável 
ou até mesmo usando a propriedade *arguments* que existe internamente em todo objeto.

### Function vs Arrow Function

Em um primeiro momento, todas as três formas de criação de função parecem funcionar 
de forma bem similar. Porém, a *arrow function* difere da *function* usual em 
alguns pontos, sendo o mais importante para nós nesse momento a questão do this.

A primeira diferença entre a **declaração de função** e as **expressões de função** 
é o *hoisting*, que é uma característica do Javascript que permite com que você 
utilize variáveis e funções antes mesmo de declará-las, ou seja, é como se elas 
fossem “içadas” para o topo do código, mesmo que na prática isso não aconteça, 
já que isso ocorre porque elas são alocadas na memória durante a compilação do código.

Mas, além do *hoisting*, existe outra diferença principal entre declaração de 
função e *arrow function*: ao contrário das funções normais, *arrow functions* 
herdam automaticamente o contexto de onde foram criadas e não têm seu próprio 
“contexto de invocação”. Ou seja, não podem ser ligadas a contextos específicos 
com this e nem fazer uso dos métodos `bind()`, `call()` e `apply()`. 

*Arrow functions* também não possuem a propriedade *prototype* e por isso não 
podem ser usadas como funções construtoras.

### Herança de protótipo

Vamos ver como funciona a herança de protótipo, que é a forma "original" do 
JavaScript, de fazer orientação à objetos, antes de existirem as classes.

O processo do interpretador do JavaScript de ir pulando objeto, percorrendo e 
procurando determinado método ou determinada propriedade para acessar, chamamos 
isso de cadeia de protótipo. E ela pode se estender, fazendo os objetos herdarem 
recursos uns dos outros, até que cheguem no final da cadeia, no final do processo, 
onde o JavaScript vai encontrar o próprio protótipo do objeto **Object**, que é 
a base que define todos os objetos criados com JavaScript, e é onde estão 
definidos todos os métodos que são comuns a todos os objetos, inclusive 
`setProtypeOf`, que leva dois parâmetros, o objeto que vai herdar propriedades e 
o objeto que vai ceder essas propriedades à serem herdadas.

> Cadeia de protótipo: é como a relação de herança, que tem um objeto pai com 
> vários outros objetos filhos.

### `__proto__` vs prototype

Durante os estudos de JavaScript é normal vermos os protótipos de duas formas 
diferentes, através da propriedade `__proto__` ou do objeto *prototype* que vemos 
em todos os objetos. Para entender melhor essa diferença, vamos testar alguns 
códigos:

```js
let user = {
 perfil: 'estudante'
}

let estudante = {
 nome: 'ana'
}

Object.setPrototypeOf(estudante, user);
```

No trecho acima, definimos dois objetos, com propriedades diferentes, e 
estabelecemos que o objeto `user` será usado como protótipo para o objeto 
estudante. Podemos testar esse código direto no terminal:

```js
console.log(estudante.nome)   // 'ana'
console.log(estudante.perfil) // 'estudante'
```

Ou seja, o objeto estudante, além da propriedade nome, também tem a propriedade 
perfil, trazida do protótipo user. É possível acessar `__proto__` de estudante, 
porém, para isso, devemos copiar o código acima e executá-lo no console do navegador, 
pois o módulo console do Node.js funciona de uma forma um pouco diferente e não 
vai acessar essa propriedade. Se adicionarmos mais uma propriedade ao objeto user, 
esta entrará também como protótipo do objeto estudante. 

Quando usamos objetos e funções para trabalhar com POO em JavaScript, os objetos 
criados não são instâncias diferentes (ou seja, cópias do objeto-base), e sim, 
referências a um mesmo objeto que está sendo delegado aos objetos que o usam como 
protótipo. Agora vamos ver outro exemplo, dessa vez utilizando **new** para criar 
um novo objeto:

```js
function User() {}

User.prototype.perfil = 'estudante';

let estudante = new User();

console.log(estudante.perfil); //'estudante'
```

No caso acima, a palavra-chave **new** vai criar um novo objeto simples e definir, 
na propriedade prototype desse objeto recém criado, as propriedades de protótipo 
que encontrar em User. O *prototype* é criado automaticamente e existe como 
propriedade apenas em funções, para quando queremos usar determinada função como 
construtor usando **new**. 

Em resumo:
- `__proto__` é uma propriedade que todos os objetos têm e que aponta para o 
protótipo que foi definido para aquele objeto;
- *prototype* é uma propriedade da função que é definida como protótipo quando 
usamos **new** para criar novos objetos.

Você pode ter notado que alguns objetos também possuem uma propriedade chamada 
`[[Prototype]]`. Esta é uma propriedade interna que cada instância de um objeto 
possui, e que aponta para a propriedade *prototype* da função que está sendo usada 
como protótipo. Quando criamos um novo objeto usando **new**, a propriedade 
*prototype* do construtor é "linkada" à essa propriedade `[[Prototype]]` da nova 
instância criada.

Existem diversos métodos internos do JavaScript para verificar as propriedades de 
um construtor e também das instâncias criadas através dele. Não é recomendável 
alterar diretamente o *prototype*, pois alterar as regras de herança de qualquer 
objeto afeta a performance do código em qualquer interpretador, seja o Node.js 
ou navegadores. 

Outro detalhe é que todas as propriedades de uma cadeia de protótipos são 
enumeradas e o tempo que o interpretador leva para pesquisar uma propriedade, 
desde o nível mais alto na cadeia, pode ser longo e impactar o desempenho. Além 
disso, se o código tentar acessar uma propriedade não existente, vai percorrer 
toda a cadeia durante a busca. Assim, não é uma boa prática criar longas cadeias 
de protótipos.

### Cópia vs referência

Os métodos e propriedades não são copiados de um objeto para outro na cadeia de 
protótipos, eles são acessados pelo interpretador ao percorrer a cadeia e os 
métodos executados de acordo com o this, ou seja, o contexto em que o método foi 
executado.

### Object.create() vs new

O **new** serve para criar instâncias de objetos através de funções construtoras 
(antes de ter sido introduzida a nomenclatura de classe). Já o `Object.create()` 
tem utilidade semelhante ao **new**, porém ele faz mais sentido no contexto de 
protótipo e o **new** no de classes. Na vida real, se for usar o modelo *prototype*, 
utilizamos Object.create criando objetos literais, passando objetos a partir de 
um modelo para outro.

### Estrutura de classe

O `constructor()` é uma função especial que recebe, via parâmetros, as propriedades 
que um objeto precisa ter ao ser instanciado a partir de uma classe, também é 
através do construtor que uma classe herda métodos e propriedades da superclasse 
através da função `super()`. Porém, dependendo da necessidade do projeto, uma 
classe pode não ter um construtor, apenas métodos. Além disso, por debaixo dos 
panos, todas as classes seguem o modo estrito do js.

Quando criamos uma classe, é possível designar que determinados métodos sejam 
estáticos. Ou seja, estes métodos não são inicializados quando criamos uma nova 
instância de classe (usando **new**), mas sim a partir da própria classe, por 
exemplo:

```js
class User {
 constructor(nome, email, cpf) {
    this.nome = nome
    this.email = email
    this.cpf = cpf
	}

	exibirInfos() {
		return `${this.nome}, ${this.email}, ${this.cpf}`
	}
}
```

No exemplo acima, o método `exibirInfos()` não é um método estático, e só é 
possível executá-lo a partir de uma instância da classe User, agora vamos 
refatorar a classe, declarando `exibirInfos()` como sendo um método estático:

```js
class User {
  constructor(nome, email, cpf) {
    this.nome = nome
    this.email = email
    this.cpf = cpf
  }

	static exibirInfos() {
		return `${this.nome}, ${this.email}, ${this.cpf}`
	}
}
```

Ao executarmos, recebemos o seguinte retorno:

```js
console.log(User.exibirInfos()) //undefined, undefined, undefined
```

Agora, como o método depende de informações recebidas do construtor e isso não 
ocorreu (uma vez que não criamos uma instância e nem passamos os dados necessários), 
recebemos `undefined` para cada propriedade. Os métodos estáticos são normalmente 
utilizados para chamadas de métodos internos de *frameworks* e bibliotecas, ou 
em qualquer caso que a classe não dependa de instâncias específicas.

### Herança de classe

A herança de classe é importante para um melhor reaproveitamento de código, uma 
vez que permite a criação de novas funcionalidades com base em um modelo. Fazendo 
com que os objetos e as regras de negócio criadas pelo sistema façam sentido e 
sejam de fácil abstração.

### Encapsulamento

Um dos princípios da Orientacao à objetos é a limitação do acesso direto aos dados, 
como os atributos e métodos de uma classe, para evitar usos inadequados desses dados.

### Polimorfismo

Em relação ao polimorfismo, o principal conceito é a propriedade de duas ou mais 
classes derivadas de uma mesma superclasse responderem à mesma mensagem, cada uma
de uma forma diferente. Ocorre quando uma subclasse redefine um método existente 
na superclasse, ou seja, quando temos os métodos sobrescritos (*overriding*), mesma 
assinatura, mas com funcionalidades diferentes.

### Interfaces

As interfaces possuem um papel muito importante na programação orientada à objetos, 
uma vez que esse paradigma é baseado na ideia de que os objetos apresentam uma 
interação entre si. Nesse sentido, as interfaces de um objeto funcionam como uma 
coleção de métodos pelos quais é possível realizar essas interações.

Imagine uma fôrma pré-definida para alguma coisa. As interfaces funcionam de forma 
similar, é como um "contrato de código", onde você pode nomear, parametrizar e/ou 
descrever exatamente quais serão os tipos de objetos gerados a partir desse “molde”.

Normalmente você pode usar interfaces em TypeScript durante a criação do contrato 
que classes devem seguir e os membros da interface que essas classes devem 
implementar. Além disso, pode-se representar os tipos na sua aplicação, assim 
como sua declaração normal de tipo de dado. 

Interface então, é uma estrutura que define um contrato na sua aplicação, e as 
classes que derivam de uma interface obrigatoriamente devem seguir a estrutura 
fornecida por ela, ou seja, devem seguir seus tipos e métodos. O compilador do 
TypeScript não converte interfaces para JavaScript, e imaginem a confusão que 
seria se esse conceito fosse aplicado a uma linguagem fracamente tipada...

A interface é construída por meio da checagem de tipos, que são as conhecidas 
*duck typing* (tipagem pato) ou a *structural subtyping* (subtipagem estrutural).
 Traduzindo isso para programação, não nos interessa o tipo do objeto, mas sim o 
 que o objeto consegue fazer, ou seja, se ele tem determinados métodos e 
 propriedades.

## SOLID

É um conjunto de *design patterns* desenvolvido para OO:

**S - Single responsability principle**: cada módulo, classe, método, função só 
tem uma responsabilidade;

**O - Open/closed principle**: a classe tem que está aberta para ser expandida, 
porém, fechada para ser modificada. Então a ideia é que seja possível adicionar 
funcionalidades numa classe, mas não alterar métodos que já existam, estejam em 
funcionamento ou alterar a classe em si. O princípio do aberto/fechado está muito 
ligado a um conceito em OO, que não temos no JavaScript, que são as chamadas 
interfaces. Elas existem no TypeScript, que é um superset do JavaScript.

**L - Liskov substitution principle**: se temos uma subclasse e uma superclasse, 
ou seja, uma classe que herda da outra, deveria ser possível sempre substituir 
uma pela outra, sem que nada deixe de funcionar. Em outras palavras, se uma classe 
tem um atributo, a subclasse dela também tem que ter. Se algo funciona na 
superclasse, tem que funcionar na subclasse também, ou seja, uma subclasse não 
pode fazer o que chamamos de quebrar contratos feitos pela superclasse. Portanto, 
uma coisa que está estabelecida pela superclasse, não pode ser quebrada pela 
subclasse.

**I - interface segregation principle**: esse princípio diz que clientes não 
devem ser forçados a depender de interfaces que eles não usam. Basicamente, esse 
princípio diz que não podemos impor uma implementação de uma coisa que não vai 
ser necessária.

**D - dependency inversion principle**: diz que módulos que estão em um nível 
mais acima da hierarquia de classes, não podem depender de nada que está abaixo 
deles, e também diz que nenhum deles podem depender de implementações, e sim, de 
abstrações. Quando falamos de abstração, estamos falando de esconder detalhes de 
como uma coisa funciona. Por exemplo, usamos um computador, utilizamos as 
interfaces do computador, como o teclado, então todas as entradas USB são 
interfaces por onde nos comunicamos com o computador, mas não vemos por dentro o 
funcionamento dele. Ou seja, a questão é abstrair os detalhes de como determinado 
método funciona, e não fazer com que tudo seja implementado junto.