# Figma: construindo o layout do site mobile

O foco desse curso está na área de UI Designer, que é mais responsável por:

- hierarquia e informação; 
- elementos da interface; 
- fluxos de navegação;
- prototipação;

## Introdução

**Metodologia 5W2H:** consiste em perguntas para entender melhor todo o contexto de nosso produto voltado para UX (experiência do usuário), elas são:

- What (o que)
- Why (por quê)
- Where (onde)
- When (quando)
- Who (quem)
- How (como)
- How much (quanto)

**Metodologia duplo diamante:** uma das metodologias existentes utilizada para pensar em interface, mas essa simplifica bem a maneira de pensar experiências e produtos que irão resolver as dores das pessoas que utilizariam esse produto. O que fica claro nesse momento é que o UX designer, está participando de ponta a ponta nesse desenvolvimento, enquanto o UI designer tem o foco em desenvolver a aparência desse produto.

<img src="../../../assets/duplo-diamante.png" alt="Metodologia do duplo diamante">

Focando no segundo diamante...

- [Primeira parte]
**Idear e desenvolver:** é onde começa a fazer a geração de alternativas, gerando várias ideias do que poderia ser, criando várias telas e opções. É onde fazemos rabiscos, desenhamos no papel, criamos wireframes e fluxos de navegação para saber como isso pode ser desenvolvido.

- [Segunda parte]
**Distribuir e implementar:** as coisas vão convergindo, vamos testando, chegando aos resultados finais, testando com o usuário, fazendo testes moderados/não moderaodos, testes A/B, vendo o que está dando errado e refazer até chegar no produto final.

## Estruturação e Ideação

**Sitemap:** é a criação de um fluxograma ideal para entender e criar todo o fluxo que os usuários podem percorrer. No figma, podemos criar um sitemap através do FigJam.

**Rabiscos:** é um método rápido e prático de projetar e organizar ideias antes mesmo de começar a projetar no figma.

**Wireframes:** é a representação visual da estrutura de um sistema de design, ou seja, ele não é o design final, é apenas demonstrando como seria essa estrutura onde entrariam textos, imagens, botões, de forma muito básica sem dar maior detalhamento de como seria a versão final dessa interface. Com disso, temos dois tipos:

 - **Wireframes de baixa fidelidade:** são mais rápidos para testes e funcionam bem para entendimento de algo rústico. São conhecidos por não conterem as cores finais, apenas escalas de cinza com foco na estrutura do design;

 - **Wireframes de alta fidelidade:** possui uma criação mais lenta e similar ao produto final.

**Grids no Figma:** com o layout grid fica mais fácil definir os espaçamentos e posicionar os elementos. Vale lembrar que os espaçamentos devem ser obrigatoriamente múltiplos de 8 por ser a padronização de todos os projetos.

## Conhecendo o Figma

**Tipografia:** é muito recomendado que se escolha no máximo 3 fontes diferentes, mas deve ter cuidado para que, mesmo diferentes, elas conversem entre si.

**Aplicação de cores:** uma técnica muito usada é o 70 20 10. 70% de uma cor, geralmente a cor de fundo; 20% de outra, geralmente escalas de cinza; e 10% de outra cor, geralmente cores de destaque.

**Imagens:** assim como as cores, as imagens podem ser salvas como estilos para serem reutilizadas, assim como podem ser editadas. Além de ser interessante buscar imagens exemplo em sites como unsplash, pexels e freepik.

**Espaçamentos:** como o material design cita, os espaçamentos são importantes para termos uma padronização nas nossas telas e fluxos que estamos criando. Uma das recomendações é que trabalhemos com espaçamentos múltiplos de 8, criando interfaces mais padronizadas.

**Autolayout:** ajuda a padronizar e automatizar os espaçamentos para evitar maiores conflitos e otimizar o trabalho. Para quem já é frontend, verá a similaridade com display flex e suas propriedades, além de ver o conceito de padding (espaçamento interno do elemento) e alguns conceitos além, como fixed, fill container e hug para largura e altura, que são apenas para definir se essas medidas serão fixas, aumentar de acordo com o container e quebrar linha ou se irão ter a exata medida de si, respectivamente.
Algo interessante a se observar é que é interessante observar que tipo de medida você está utilizando, já que a fill, por exemplo, é mais dinânica que as outras, mas cada uma tem sua aplicabilidade.
Outra boa funcionalidade é a de absolute position, que pode ser selecionada quando colocamos um elemento dentro de outro elemento com autolayout, para podermos sobrepor elementos no nosso design e ter maior flexibilidade na disposição de itens.

*Diferença entre usar frame e retangulo direto é apenas que nosso artboard/frame não vem com uma cor definida e pode ser usado autolayout nele, ao contrário do retângulo.*

## Heurísticas de Nielsen

Primeiro, sobre Jakob Nielsen, ele é um dos pioneiros no estudo de experiências e interações entre humanos e máquinas e juntamente com Norman, criaram o Nielsen Norman Group, que é um dos maiores grupos de estudo dessa área de experiência, interfaces e interações. Com isso, Jakob criou as 10 heurísticas de Nielsen, que é uma lista para entendermos se as interfaces que estamos criando são eficientes, se vão ajudar os usuários e se irão conseguir entender, são elas:

- **Visibilidade do status do sistema:** é importante mostrar para o usuário onde ele se encontra, exemplo, no início das telas, informar do que se trata aquela tela;

- **Compatibiilidade entre o sistema e o mundo real:** é importante traduzir um pouco do contexto do mundo real para as interfaces para que possa ser entendida mais facilmente, por exemplo, a necessidade de construir um botão que passe a ideia visualmente que é algo clicável, destacado e identificável como no mundo real;

- **Liberdade de controle para o usuário:** além de mostrar onde o usuário se encontra, é importante dar ações e possibilidades para ele controlar o que estiver fazendo, por exemplo, os campos de texto, ir e voltar, edições etc;

- **Consistência e padronização:** seja em espaçamentos, cores e fontes, seguir um estilo definido é importante;

- **Prevenção de erros:** ou seja, antes da pessoa cometer um erro na aplicação, podemos previnir que esse erro aconteça, a exemplo disso, temos os avisos de erro em inputs antes que a pessoa envie informações;

- **Reconhecimento ao invés de memorização:** é importante utilizar padrões que as pessoas reconheçam facilmente, por exemplo, ícones de senso comum de busca, a lupa, ícone de notificação, o sino etc;

- **Flexibilidade e eficiência de uso:** é a preocupação em pensar que nossa aplicação será usada pela pessoa mais leiga a mais experiente, podendo oferecer diferentes caminhos para o mesmo local. Isso se aplica mais em ferramentas, como por exemplo, o Figma, que oferece diferentes caminhos para fazer um retângulo, como clicar no botão explícito ou clicar no atalho dessa utilidade. Oferecer esses caminhos para diferentes níveis de experiência realizar uma ação é do que se trata essa heurística;

- **Estética e design minimalista:** é sobre focar em ações, mesmo que a estética seja importante, é essencial trazer o foco em ações;

- **Reconhecimento de erros:** parecido com a prevenção de erros, mas esta trata sobre erros antes deles acontecerem de fato, enquanto o reconhecimento é após! Como o que aparece em tela quando o usuário faz uma busca que não gera resultados ou quando o usuário erra seu login na aplicação;

- **Ajuda e documentação:** é importante trazer para pessoa que estiver utilizando a plataforma, alguma alternativa caso ela precise de ajuda;