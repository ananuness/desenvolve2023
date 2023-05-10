# 🧩 Objetos e o prototype em JavaScript

## 🧬 O que é prototype?

É muito comum ouvirmos que o JS é uma linguagem baseada em protótipos e que tudo em JS é um objeto. Geralmente, trabalhamos com objetos literais, mas além disso, existe um outro tipo de objeto que o JS utiliza para que consigamos criar uma base para tudo que trabalhamos dentro da linguagem, sejam objetos, arrays, números etc.

Então se criarmos no console do navegador uma `const arr = [1, 2, 3]`, podemos fazer operações com ela, como `arr.length` e ele nos passa o tamanho desse array, 3 elementos.

Agora vamos acessar `arr.__proto__`, esta propriedade guarda as definições de todo array que criamos no JS, então o proto de *prototype* é como se fosse uma base que o JS traz para dentro de tudo que criamos, sejam arrays, números, objetos, strings etc, e graças a essa base que ele traz e cria junto com os nossos dados, conseguimos ter métodos associados a ele. Então conseguimos utilizar esses métodos graças a esse objeto oculto, que o JavaScript cria e associa, tudo por baixo dos panos, sem termos que fazer nada.

Esse objeto oculto já traz com ele as próprias funções, então todos os métodos de array que utilizamos em JS como `forEach()`, `map()`, `push()` para adicionar alguma coisa dentro do array, eles estão aqui dentro dessa propriedade que é o proto, o protótipo do objeto array. E conseguimos também ver uma propriedade chamada `constructor()`, o construtor desse objeto. Ele se chama Array, então se quisermos fazer de outra forma essa criação de array podemos simplesmente criar: `const outroArray = new Array([1, 2, 3])`, e se acessarmos outroArray, veremos o array criado, o construtor e dentro dele os dados. Podemos fazer isso com outros tipos de dados também.

Isso é um conceito importante para podermos avançar também nos estudos do JS. Esse protótipo nos permite trabalhar com o conceito de herança, ou seja, herdar atributos, propriedades, funções a partir do protótipo.

## 🔧 Propriedades de prototype

Criando um Cliente genérico:

```js
function Cliente(nome, cpf, email, saldo) {
	this.nome = nome;
	this.cpf = cpf;
	this.email = email;
	this.saldo = saldo;
	
	this.depositar = function(valor) {
		this.saldo += valor;
	}
}
```

*Então, qual a diferença entre o genérico e o literal que já conhecemos?*

Essa função genérica que criamos irá servir como uma função construtora, então essa função vai sempre possuir um objeto cliente:

```js
const pessoa = new Cliente('André', '1254359542', 'andre@email.com', 100);
```

*Mas o que o **new** significa?*

Usamos a palavra reservada **new**, para dizer que estamos criando, a partir da nossa função Cliente, um novo cliente, chamamos isso de **instância**, então a nossa const pessoa é uma nova instância de Cliente criado a partir da nossa função construtora.

Quase todo objeto em Javascript tem associado a ele um segundo objeto, seu protótipo, que lhe confere uma série de atributos e métodos. Através do *prototype* que acessamos para manipulá-lo, podendo adicionar propriedades e funções, novos objetos criados herdarão essas características e comportamentos diretos do protótipo.

Vimos que quando um objeto JavaScript é criado ele tem propriedades particulares (por exemplo, nome, cpf etc). Além do nome e do valor, cada propriedade tem também três atributos:

- *Writable*: define se a propriedade pode ser adicionada ou escrita em um objeto;
- *Enumerable*: define se a propriedade é retornada, por exemplo, em um loop `for...in `ou utilizando `Object.keys()` / `Object.values()` / `Object.entries()`. Ou seja, se a propriedade é enumerável;
- *Configurable*: especifica se a propriedade pode ser modificada ou deletada. Ou seja, se é configurável.

Por definição, todas as propriedades de um objeto criadas durante o desenvolvimento têm estes três atributos como true. Já a maior parte das propriedades herdadas do protótipo têm estes atributos como false e não podem ser enumeradas, adicionadas ou alteradas.

O JavaScript utiliza o termo *own property* (propriedade própria) para se referir às propriedades que pertencem ao objeto (como os exemplos nome, cpf e email) e que não são herdadas do protótipo. Veja que métodos que começam com *getOwnProperty*… funcionam apenas em propriedades "próprias" do objeto. 

- Objetos criados de forma literal (`const obj = {a: 1}`) utilizam `Object.prototype` como protótipo; 
- Objetos criados com **new** a partir de um construtor herdam a propriedade *prototype* de sua função construtora; 
- Objetos criados com `Object.create()` recebem como *prototype* o primeiro parâmetro da função - que pode ser null.