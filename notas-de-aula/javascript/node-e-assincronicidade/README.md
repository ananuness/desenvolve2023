# ⏳ Node.js e Assincronicidade

## 🛠️ Como o Node executa o código e como funciona sua arquitetura?

Para falar sobre esse assunto, começamos falando sobre a **Call Stack**, 
que é a pilha de processamento do nosso código, ou seja, todas as 
funções que executamos vão para essa pilha. Por exemplo, dado o seguinte 
código:

```js
function multiply (a, b) {
  return a * b;
}

function double(number) {
  return multiply(number, 2);
}

function printDouble(number) {
  const result = double(number);

  console.log(result);
}

printDouble(2);
``` 

O JavaScript vai ler esse código de cima para baixo, vai declarar todas 
as 3 funções que estão sendo criadas e no final irá invocar a função 
`printDouble()` passando `2` como parâmetro.

Quando essa função for invocada, é onde entra a *Call Stack* em ação. 
Então, a `printDouble(2)` já está presente nessa pilha de processamento, 
mas observe que dentro da printDouble, chamamos a `double(number)`, logo 
ela também entra dentro da nossa *Call Stack*. E dentro da função double, 
chamamos a `multiply(number, 2)`, então ela entra na Stack também.

Dentro da função `multiply`, observamos que ela apenas retorna um valor, 
então assim que termina sua execução, quer dizer que seu papel já foi 
concluído, logo, ela sai da Call Stack. A próxima, é a `double`, que já 
com o valor do retorno da multiply em mãos, também conclui sua execução 
e sai da Stack. O mesmo acontece com o printDouble, e nisso, podemos 
observar que, as primeiras execuções a serem empilhadas na Stack, serão 
as últimas a saírem.

### 🧵 O Node é Single Thread

Isso quer dizer que o Node tem apenas uma Call Stack, ou seja, ele 
consegue executar uma coisa por vez.

*Mas como assim? Se o Node é Non-blocking I/O, ou seja, executa código assíncrono.*

De fato, o Node consegue executar mais de uma coisa ao mesmo tempo, 
mesmo sendo *Single thread*, porque debaixo dos panos, ele roda com uma 
biblioteca escrita em C, chamada **Libuv**.

A Libuv implementa dois caras que são responsáveis por essa possibilidade 
de rodar códigos assíncronos em "background" e eles são chamados de 
**Thread Pool** e **Event Loop**. Mas a Libuv não serve só para isso, 
ela implementa toda a parte de *FileSystem* do Node, de DNS, entre 
outros. Ela uma biblioteca bem completa e dá muitos poderes para o Node.

#### 🔁 Exemplo de Thread Pool e Event Loop

```js
console.log('Antes');

db.query(query, function callback(err, data) {
  console.log(data);
});

console.log('Depois');
```

Observando o código, já entendendo sobre Call Stack, sabemos que a 
primeira linha entrará na Stack, logo é executada e sai.

Já na linha do `db.query`, é onde encontramos a chamada **função bloqueante**, 
ou seja, ela leva certo tempo para ser executada, nesse caso, por ser 
uma função que precisa se conectar com o banco de dados, executar a 
query, esperar a resposta, trazer as informações etc. 

Nesse tempo, se o Node não tomasse nenhuma ação, essa função ficaria 
travada na Call Stack, bloqueando a execução do restante do código, 
enquanto ela não fosse resolvida. Mas o Node entende que essa função é 
bloqueante e passa a execução dela para dentro da Thread Pool da Libuv 
sendo tirada da Call Stack e liberando para o resto do nosso código 
ser executado.

Após a query ser executada na Thread Pool, a função de callback passada 
como parâmetro é lançada para uma **Callback Queue**, já com todos os 
dados recebidos pelo banco de dados. 

E entre a nossa Call Stack e a Callback Queue, temos o chamado 
**Event Loop**, que é como se fosse um `while (true)`, que fica toda 
hora indo na Queue para ver se tem alguma função pronta para ser 
executada. Quando for encontrada, é feita uma verificação para saber 
se a Call Stack está liberada e se estiver a função callback é puxada 
de volta para a Stack para continuar o processamento normal.

E é assim que o Node consegue executar código assíncrono!

<hr>

**Non-blocking I/O:** É a capacidade de realizar operações de entrada e 
saída (Input e Output) sem bloquear a thread principal do sistema 
(execução assíncrona).