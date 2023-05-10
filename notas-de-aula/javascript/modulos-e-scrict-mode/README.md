# 📒 Módulos e o strict mode no JavaScript

## 📑 Módulos

Quando trabalhamos com Node.js, é comum usarmos arquivos diferentes 
para separar e organizar o código. Cada arquivo `.js` é um módulo 
independente e suas funções, variáveis e classes não são compartilhados 
com o restante do código, a não ser quando são explicitamente exportados 
e importados em outros módulos.

O JavaScript, em seus diversos interpretadores, faz a 
importação/exportação de módulos de duas formas, usando a sintaxe 
**CommonJS (CJS)** ou a sintaxe **EcmaScript Modules (ESM)**.

### CommonJS (CJS)

Até a versão 13, a função que o Node utiliza por padrão para importar 
módulos em um arquivo é `require()`. Os módulos podem importar e 
exportar todas as funções declaradas no arquivo ou apenas algumas, de 
acordo com o necessário. Este é o formato de exportação e importação 
de módulos conhecido como CommonJS ou CJS.

### EcmaScript Modules (ESM)

Quando utilizamos o ESM, o mesmo processo de exportação de módulos é 
feito com a sintaxe *export* *ou export default* e a importação com a 
sintaxe `import <nomeModulo> from ‘./caminho/arquivo.js’`.

Esta outra forma de lidar com a importação e exportação de módulos veio 
com o famoso **ES6** ou JS2015 e foi aos poucos sendo implementada para 
funcionar nativamente nos navegadores com a ajuda de bundlers como o 
WebPack, que fazem a “tradução” de métodos do JavaScript mais moderno 
para garantir retrocompatibilidade.

Hoje o ESM já funciona nativamente em todos os navegadores e passou a 
ter suporte para Node a partir da versão 13. Mesmo assim, grande parte 
das aplicações desenvolvidas com Node ainda utiliza o formato CJS de 
importação e exportação de módulos e as bibliotecas, pacotes e 
frameworks estão em processo de substituição do CJS para o ESM.

**Importante:** para utilizar a sintaxe ESM com Node é preciso incluir, 
no arquivo `package.json`, a propriedade `"type": "module"` e sempre 
incluir a extensão do arquivo `.js` nos caminhos de importação - por 
exemplo:

```js
import soma from ‘./caminho/arquivo.js’;
``` 

Existe uma convenção no uso de ESM em projetos Node, que é utilizar 
a extensão `.mjs` para distinguir quais arquivos são módulos, continuando 
com a extensão `.js` para os arquivos que não exportam módulos.


## 🔒 Strict mode

O modo estrito do JavaScript serve para impedir que alguns comportamentos 
do JavaScript causem "falhas silenciosas" (transformando em erros que 
são lançados pelo interpretador) e corrigir alguns outros que podem 
induzir a bugs potenciais e comportamentos inesperados. O JS é uma 
linguagem que não tem *breaking changes*, ou seja, não é possível 
corrigir certos comportamentos não desejados retirando o código das 
novas versões, pois há o risco de quebrar código que já está rodando 
em sites e aplicações na internet. O modo estrito é uma forma de ajudar 
a contornar alguns destes comportamentos sem que o código "não estrito" 
deixe de funcionar.