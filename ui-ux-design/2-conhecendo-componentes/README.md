# Figma: conhecendo componentes da interface

## Diretrizes do design de interface: Boas Práticas

- **Simplicidade:** temos que utlizar a simplicidade ao nosso favor para conduzir o usuário a se encontrar, a saber onde ela está, quais são as ações que ela pode tomar. Para isso, precisamos nos atentar a 3 detalhes:

	- **tipografia:** evitar utilizar mais de 3 famílias; 
	- **cor:** ideal seria uma para o fundo, outra pra textos e outra para itens de destaque mais uma secundária e cores semânticas, como verde para sucesso e vermelho para erro, por exemplo;
	- **espaçamento:** importante para respiro e leveza visual;
		
- **Hierarquia:** importante para a pessoa entender quais ações existem e o que pode fazer, além de entender o que é de maior e menor importância;
	
- **Navegação facilitada:** auxilia a pessoa a não somente entender as ações, mas também a se localizar e quais as possibilidades de caminhos a seguir;
	
- **Padrão visual:** muito ligada a simplicidade e aos design systems, já que mantendo simples, conseguimos manter uma boa padronização, então os usuários conseguirão reconhecer os padrões que usamos, além de conseguirmos criar sistemas de design na qual definimos nossos padrões e regras para utilização, a exemplo, temos o [Material Design da Google](material.io);
	
- **Responsividade:** é sobre se adequar a vários dispositivos e telas em diferentes tamanhos, através dessas informações, conseguimos definir quebras no layout para executar essa adequação, os famosos Breakpoints;
	
## Design Atômico e Componentes da Interface
	
É uma metodologia de sistemas de design modulares, criado pelo designer Brad Frost, e nela há uma relação muito grande com a biologia e o design de interface, pois sua divisão se assemelha com os níveis de organização em biologia: átomo, molécula, organela, célula, tecido, órgão e assim sucessivamente. Mas nessa metodologia, a estrutura se dá por:

- **Átomos:** são os menores elementos possíveis, que não podemos dividir, como cor, tipografia, sombra, botões, textos, inputs etc;

- **Moléculas:** são pequenos elementos formados por átomos, ou seja, por elementos indivisiveis. A exemplo disso, temos um campo de email com sua label e um botão de enviar;

- **Organismos:** elemento mais complexo formado por moléculas, como um formulário, formado por vários campos de preenchimento de informações;

- **Templates:** aqui, perdemos esse paralelo com a Biologia e entramos de fato em design de interface. Eles são um conjunto de todos os elementos anteriores, trazendo a estrutura do produto, como os wireframes;

- **Telas:** estas são o produto final de fato, trazendo além do aspecto, os textos e ações que essa aplicação irá ter!

Com esses conceitos em mente, ficará mais fácil conseguir produzir elementos escaláveis e reutilizá-los ao longo da nossa aplicação mantendo a padronização ideal.

## Componentes no Figma

A ideia de poder definir um elemento como componente, vem para ajudar na padronização, escalabilidade e, consequentemente, na facilidade de reutilizar e mudar elementos, sem precisar de grandes esforços. Isso pode ser notado se você modificar um elemento que é componente, pois ele modifica todos aqueles que são iguais a ele, garantindo todas as vantagens citadas acima. E para visualizar todos criados, basta ir na aba de Assets à esquerda da prancheta.

### Componente para Variante

Assim que selecionamos um componente, temos a opção ao lado direito, em criar uma *Variant*, que transforma nosso componente em uma caixa com dois elementos iguais. Ou seja, podemos ter nosso elemento padrão e criar uma ou várias variações dele, garantindo maior controle aos nossos elementos.

*Caso tenha algum componente com apenas duas variações, se fizer sentido, podemos utilizar como valor de propriedade ```True``` ou ```False```, que adiciona uma nova forma de selecionar nossas variações, através de um botão "liga/desliga", tornando mais prático do que selecionar por uma lista.*

Uma tática que também pode ser usada na criação de componentes é a criação de um componente base e a partir dele criar um set de variações, o que traz como vantagem a manutenção simplificada dos componentes. Além disso, é importante citar a estratégia de utilizar instâncias de componentes master, dentro de outros componentes. Como por exemplo, poderíamos transformar ícones em componentes master e utilizá-los dentro de outros componentes, a vantagem é a possibilidade de mudar o ícone em apenas um clique, pois podemos adicionar outro componente naquele lugar, trazendo uma customização avançada e facilitada.

## Fluxos e Handoff

O fluxo de navegação é uma forma completa para entregas de projetos. Diferente do protótipo, esse fluxo permite uma análise mais estática de cada passo da aplicação, com distinção de cenários de sucesso e de erro. Vale ressaltar que isso é muito valioso, pois apresenta todos os caminhos que uma jornada pode levar, tornando possível identificar os mais variados cenários que as pessoas que utilizam o produto podem se encontrar.
Já o Handoff é o momento em que um profissional finaliza seu serviço numa parte do projeto e passa para outro poder continuar a produção.

## Extra

### Comandos:

- ```Ctrl + SHift + V:``` garante que o estilo do elemento será preservado e não do que foi copiado;
- ```Ctrl + D:``` duplica um elemento;
- ```Ctrl + A:``` seleciona todos o elementos de um frame;
- ```Ctrl + Alt + B:``` deixa de ser uma instância de um componente e passa a ser um elemento comum;
- ```Ícone do Figma > View > Show/hide UI (ctrl + \):``` mostra ou esconde os menus ao redor da prancheta;
- ```Ctrl + Alt + K ou clicando no elemento, clicando com botão direito e em seguida em Create Component:``` cria componente;

#### Para quando o ícone for redimensionado e se alterar/perder peso

Caso o ícone tenha sido construído utilizando a propriedade do traçado é necessário alterar para que ele se torne um elemento com apenas a propriedade de preenchimento. Isso é necessário pois, ao escalonar um objeto construído com traçado, o valor que corresponde a essa propriedade não se altera e o peso do ícone se perde.
Para corrigir esse problema basta selecionar os elementos vetoriais que estão com a propriedade de traçado, clicar com o botão direito do mouse nesses elementos e selecionar a opção **Outline stroke**. 