# React

## O que é o React

o React trabalha com arquivos conhecidos pela extensão `.jsx` ou `.tsx`
se estiver usando TypeScript. Basicamente, esses arquivos suportam a
utilização de JavaScript + XML, ou seja, HTML dentro do JavaScript.

## Estrutura de um projeto React ([Vite](https://vitejs.dev/))

O Vite é uma das novas maneiras de criar nosso setup para projetos 
react, agora iremos falar um pouco sobre a estrutura do projeto inicial.

- `./public/`: nesta pasta ficam os arquivos públicos, geralmente 
aqueles que precisam ficar publicamente visíveis na nossa aplicação,
como imagens, fontes, favicons, assets em geral;

- `./src/`: pasta que contém de fato o código da aplicação;

- `./index.html`: é o arquivo principal do projeto, em que todo o 
código desenvolvido na pasta *src* é injetado pelo React.

- `./src/main.[jsx, tsx]`: esse arquivo é responsável por inserir no
`./index.html` o código do projeto. Através das importações do React e
do ReactDOM (basicamente o *port* do React para funcionar na web),
utilizamos um método chamado `.createRoot()`, que é utilizado apenas
uma vez em toda aplicação, aceitando um parâmetro informando qual
elemento HTML irá receber o código gerado pelo projeto React, em
seguida, chama-se o método `.render()`, para informar o que queremos
renderizar, ou seja, mostrar em tela, e é passado como parâmetro o que
queremos injetar dentro o elemento informado antes desse render. E por
fim, a tag *React.StrictMode* é uma recomendação do React para avisar
para o desenvolvedor, possíveis erros dentro do código gerado.

```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'

// mostrando em tela, dentro do elemento 
// com id 'root' o conteúdo informado
ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <React.StrictMode>
    <h1>Hello World!</h1>
  </React.StrictMode>,
)
```

> Exceto as pastas citadas, ficam arquivos de configuração.

## Bundlers e Compilers

O JavaScript é uma linguagem que depois de 2015 evoluiu muito, e por
avançar muito rápido, assim como o HTML e CSS, tem vários conceitos,
recursos etc, que os navegadores muitas vezes não conseguem acompanhar 
rápido o bastante para conseguir entender. 

Por conta disso, precisamos de ferramentas que vão conseguir converter 
nosso código escrito, em uma versão que a maioria dos navegadores 
consiga entender e é para isso que se usa os **Compilers**, um exemplo
famoso de compiler é o *Babel*.

Já mudando de assunto, dentro de aplicações frontend, muito 
provavelmente não teremos apenas um arquivo javascript, CSS ou HTML, e 
sim, vários, que no fim nas contas queremos empacotar todos os arquivos 
dentro do mesmo projeto e enviá-lo para a produção e os **Bundlers** são ferramentas que fazem isso. Eles entendem todos os relacionamentos entre 
os arquivos da nossa aplicação (ex. imports, dependências etc) e um
exemplo famoso de um bundler é o *Webpack*.