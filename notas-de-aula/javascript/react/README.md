# ⚛️ React

## Conteúdos

- [Library vs Framework](#library-vs-framework)
- [O que é o React?](#o-que-react)
  - [Single Page Application (SPA)](#single-page-application-spa)
  - [Características do React](#caracteristicas-do-react)
    - [Componentes](#componentes)
  - [Por que usar React?](#por-que-usar-react)
- [Compilers e Bundlers](#compilers-e-bundlers)

## Library vs Framework

Uma *library* (biblioteca) é um conjunto de funcionalidades focada em
resolver um tipo de problema, como o **date-fns** para manipulação de 
datas e o **axios** um client HTTP.

Já os frameworks, também são um conjunto de funcionalidades, porém,
que resolve vários tipos de problemas, como o **Angular**, que traz
funcionalidades para a criação de interface, requisições HTTP, rotas 
etc, e o **Vue.js**.

## O que é o React?

O React é uma biblioteca para a criação de interfaces (UIs), então ele
cuida única e exclusivamente as interfaces das aplicações. E todas as
funcionalidades adicionais, são encontradas nesse ecossistema de 
pacotes por volta do React, fazendo dele uma solução ainda mais robusta,
como React Router para rotas, Framer Motion para animações, Styled
components para estilo, Redux para gerenciamento de estados, dentre
várias outras soluções para essa lib tão famosa.

Outra coisa bacana do React é que ele é multiplataforma, então suas
UIs podem ser para desktop, web, mobile etc. Isso acontece, pois a
biblioteca não cuida de onde a interface será renderizada, e sim, um
"parceiro" que irá cuidar disso, por exemplo:

- **ReactDOM**: pacote para aplicações web;
- **React Native**: framework para mobile;
- **Electron**: framework para *cross-plataform* desktop apps;
- **React Native Windows**: framework para apps desktop Windows;

### Single Page Application (SPA)

Se pegarmos o React, ReactDOM para renderização nos navegadores e o
React Router para criar as rotas, teremos a famosa Aplicação de página
única ou simplesmente SPA.

Elas são essas aplicações mais modernas para web, que você navega nela 
e a página não atualiza, e sim, muda alguns pontos do seu conteúdo,
tornando-a mais rápida, dinâmica e assim por diante.

### Características do React

O React é basicamente JavaScript puro, tornando a curva de aprendizado
um pouco menor para quem tem uma boa base na linguagem, mas também,
implementa conceitos novos caracteríscos da lib, como:

#### Componentes

Os componentes no React são simplesmente pequenas partes reutilizáveis
da interface, logo, se você consegue visualizar elementos em tela que 
se repetem, que possui diferenças mínimas ou nulas, então geralmente 
isso se tornará um componente.

Então, um componente basicamente são caixas isoladas umas das outras e
caso você precise mexer em uma delas, isso não impactará nas caixas
restantes. E, que se juntarmos essas caixas, como se fosse um Lego, 
elas formarão algo maior, no caso, nossa interface completa.

> Como são criados?

O React implementa algo novo chamado de JSX, ele é basicamente um
arquivo onde podemos escrever código HTML dentro do JavaScript.

```js
import React from 'react';

export function App() {
  return <h1>Componente Funcional</h1>;
}
```

Temos então, o import, já utilizando o ES6 e uma função, ambos apenas
JavaScript, além do retorno ser um HTML. Esses componentes por função
são chamados de **Componentes Funcionais**. Mas também temos uma 
segunda forma, que é através de classe, que apesar de estar caindo em
desuso, ainda existe muitas aplicações legado que utilizam essa
estrutura:

```js
import React from 'react';

class App extends React.Component {
  // método obrigatório para renderizar HTML
  render() {
    return <h1>Componente Funcional</h1>;
  }
}
```

> Observe que, por padrão, o nome da função/classe do componente deve 
> ser em letra maiúscula, o famoso *Pascal Case*.

Vamos agora para um exemplo mais complexo. Observe que a maneira que 
adicionamos uma classe em um elemento está um pouco diferente da forma 
padrão do HTML, isso porque devemos lembrar que estamos usando 
JavaScript e a palavra "class" entra em conflito com a palavra reservada 
`class` do JS. Assim como, quando quisermos adicionar JS no HTML, temos
que envolver por chaves `{}`, como fizemos com a `logo`.

```js
import React from 'react';
import logo from './logo.png';
import './styles.css';

export function App() {
  return (
    <div className="app">
      <header>
        <img src={logo} />
      </header>
      <aside>Sidebar</aside>
      <section>Timeline</section>
      <aside>Explore</aside>
    </div>
  );
}
```

Relembrando o que foi dito anteriormente, os componentes são caixas
isoladas, estruturas feitas de maneira a não impactar em outros
componentes. Porém, do jeito que está esse código, isso não está
acontencendo, pois temos o header, a sidebar etc, tudo dentro do mesmo
componente.

O ideal seria pegarmos todas essas partes, como o header, sidebar, 
timeline e o explore e separá-los em pequenas caixinhas, ou seja, em
componentes. E o motivo disso é que criamos independência entre os
elementos da nossa página, por exemplo, se mexermos no Explore, a
Timeline não irá saber, não terá nenhum efeito colateral.

### Por que usar React?

- Reutilização de Componentes (+ velocidade, + produtividade);
- Facilidade de manutenção e escalabilidade;
- LOWA (*Learn Once, Write Anywhere*), ou seja, Aprenda uma vez, Escreva
em qualquer lugar. Fazendo referência à possibilidade de desenvolver
aplicações web, mobile e desktop.

E para saber mais, visite a documentação do [React](https://react.dev/learn)!

## Compilers e Bundlers

O JavaScript é uma linguagem que depois de 2015 evoluiu muito, e por
avançar muito rápido, assim como o HTML e CSS, tem vários conceitos,
recursos etc, que os navegadores muitas vezes não conseguem acompanhar 
rápido o bastante para conseguir entender. 

Por conta disso, precisamos de ferramentas que vão conseguir converter 
nosso código escrito, em uma versão que a maioria dos navegadores 
consiga entender e é para isso que se usa os **Compilers**, um exemplo
famoso de compiler é o *Babel*, que é usado para fazer esse tipo de 
conversão, algo que o navegador entenda:

Além disso, dentro de aplicações frontend, muito provavelmente não 
teremos apenas um arquivo javascript, CSS ou HTML, e sim, vários, que 
no fim nas contas queremos empacotar todos os arquivos dentro do mesmo 
projeto e enviá-lo para a produção e os **Bundlers** são ferramentas 
que fazem isso. Um exemplo famoso de bundler é o *Webpack*, que além
da funcionalidade citada, também é responsável por tornar possível
a importação de arquivos de imagem e CSS dentro de um arquivo 
javascript, como visto em aplicações react.

E essas ferramentas também são importantes quando construímos o 
frontend através de frameworks ou bibliotecas como o React. Apesar de
hoje em dia existir compilers e bundlers mais otimizados e de fácil
uso e configuração do que os famosos Babel e Webpack, eles são muito 
utilizados, mas para saber mais sobre os mais novos e ter um 
comparativo bacana, recomendo a leitura desse 
[artigo no CSS Tricks](https://css-tricks.com/comparing-the-new-generation-of-build-tools/).
E sobre o que o Next.js usa, confira a documentação sobre o 
[SWC](https://nextjs.org/docs/architecture/nextjs-compiler) e o
[Turbopack](https://nextjs.org/docs/architecture/turbopack).