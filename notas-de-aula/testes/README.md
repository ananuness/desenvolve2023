# 👩‍🔬 Testes

## Testes Unitários

A responsabilidade dos testes unitários é analisar pequenas interações 
no código, como uma função ou método isolado, independendo da estrutura
completa da aplicação. Tendo como importância verificar se aquela
funcionalidade está se comportando como deveria. 

Então, os testes unitários têm uma maior granularidade, eles são 
componentes pequenos em relação ao projeto inteiro e podem ser testados
isoladamente. Em contrapartida, ter essas unidades funcionando sozinhas, 
não garante que a integração delas irá funcionar.

## Testes de Integração ou de Serviço

Falando em integração, esses testes também levam em consideração as
interfaces entre cada pedaço da aplicação, como a comunicação entre
módulos, testar rotas, requisições, chamadas externas como o banco de 
dados ou uma API. Ainda assim, esses testes não analisam todo o fluxo
de uma aplicação, não garantindo seu funcionamento por completo.

## Testes End-to-End (E2E)

Analisar o fluxo de uma aplicação, fica a cargo dos testes end-to-end,
que são os testes de ponta a ponta, alto nível. Eles são longos e 
completos que analisam todos os módulos e stacks, como frontend, banco 
de dados, microsserviços etc, mas não diretamente.

A forma como o teste e2e irá funcionar, tomando como exemplo um sistema
web, será utilizando alguma forma ou algum programa que clique na 
interface, faça cadastros, navegue entre as páginas existentes e 
consiga observar as respostas dessas ações e informar se está se
comportando como esperamos. 

Observe que não será levado em consideração a implementação do código,
e sim, se a aplicação como um todo está funcionando corretamente.

## Cultura de Testes

Ter uma cultura de testes, significa criar um ambiente em que a equipe
de desenvolvimento tenha a capacidade de implementar e gerir os testes,
entendendo como eles afetam a qualidade do código e permitindo que 
problemas que eventualmente passem desse ambiente de testes sejam 
resolvidos. No geral, podemos conceituar como utilizar boas práticas 
de testes dentro da nossa companhia, organização ou projeto.

Para isso, consideraremos três fatores fundamentais: o primeiro fator 
será a **qualidade**. Ela é ter uma métrica para saber se algo é bom 
ou ruim. As métricas serão regras que vamos determinar, criaremos 
objetivos para nossa base de códigos e observaremos se estamos chegando 
perto desses objetivos ou se estamos nos afastando deles.

O segundo fator que vamos considerar é a **confiança**, que é algo 
mais subjetivo. Se todo mundo está programando e considerando a 
qualidade do que está sendo desenvolvido e buscando atingir aquelas 
métricas que foram ajustadas, teremos uma maior confiança na qualidade 
e no entendimento da nossa base de código, e continuaremos em operação. 
Vamos reduzir os custos e seguir de forma eficiente.

E em terceiro lugar, o **tempo**, um fator muito importante. Quanto 
mais economizarmos no tempo, podemos adotar e já pensar em outras 
funcionalidades para atingir os objetivos de negócio, que são a razão 
pela qual estamos desenvolvendo o produto.

Algumas etapas que podemos seguir para atingir esses fatores 
fundamentais mencionados:

- **Análise de requisitos:** visa identificar quais funcionalidades 
estarão presentes no projeto e selecionar quais testes e quais tipos 
de teste vamos implementar para poder atingir esses objetivos.

- **Plano de teste:** comumente, o time conhecido como QA, que é o 
*Quality Assurance*, ou os analistas de qualidade, elaboram o plano de 
teste, contendo as ferramentas que serão utilizadas, dividindo as 
responsabilidades de quem vai criar os testes e estimando no geral qual 
será o tempo, a complexidade e os gastos de recursos que terá naquele 
projeto.

- **Caso de teste:** aqui, são detalhados os testes em si. Quais são as 
condições, os dados de entrada, os comportamentos esperados, dados de 
saída, quantidade de testes etc. Todo esse mapeamento é feito nessa
etapa.

- **Ambiente de teste:** nessa etapa são escolhidos onde e como esses 
testes serão executados. É feito o *pipeline*, o fluxo de como é 
produzido pela equipe de desenvolvimento e como vai ser testado, 
ferramentas de versionamento e o que será utilizado, na qual as 
alterações e implementações que são feitas pelo time de desenvolvimento 
vão sendo testadas e validadas para poder seguir no projeto.

  Eles podem ser testes que rodam automaticamente, idealmente; podem 
  ser pessoas que serão responsáveis por verificar, criação de tickets
  etc. Isso vai depender de cada instituição e das plataformas e 
  ferramentas que elas conhecem.

- **Implementação:** onde é feita a documentação daqueles resultados que 
foram obtidos com os testes, problemas que aconteceram dentro dos 
processos, estabelecendo como podem ter melhorias para os próximos 
ciclos e toda essa parte que vai lidar diretamente com a implementação, 
tanto do código em si do projeto quanto da implementação dos testes e 
tudo que aconteceu em torno disso.

## Ambiente de Testes

O que exatamente é esse tal ambiente?

>O ambiente de testes é o conjunto formado pelo programa, as configurações 
> (hardware, redes, servidores, dispositivos, etc) e os dados 
> necessários para que os testes sejam executados.

A proposta do ambiente de testes é verificar todos os componentes de um 
sistema nas condições mais próximas possíveis das condições de uso real 
pelos usuários, para que possíveis bugs e erros de implementação possam 
ser corrigidos antes que o programa ou funcionalidade seja disponibilizado 
- o tal “ambiente de produção”.

Vamos ver de forma resumida o que é cada um destes ambientes:

### Desenvolvimento

É o ambiente onde o programa é desenvolvido - como o próprio nome diz. 
Desenvolver aqui pode tanto se referir ao desenvolvimento de algo do 
zero (por exemplo, uma funcionalidade) como a atualizações de partes 
de um programa que já existem. Neste momento, já são efetuados diversos 
testes como os **unitários** e de **integração**.

### Testes

Como o código que está em desenvolvimento está sempre sendo atualizado, 
é normal que testes mais complexos e que levem mais tempo para serem 
implementados, por exemplo os testes **E2E** (end to end ou “ponta a ponta”) 
estejam em um ambiente separado do de desenvolvimento, utilizado muitas 
vezes pelas pessoas que chamamos de QAs (de quality assurance ou 
“garantia de qualidade”) ou testers.

Neste momento são testadas e avaliadas várias partes do programa, como 
a integração com outras partes do sistema, comportamento com o banco, 
performance das tarefas, etc.

### Staging

O último estágio antes da produção, onde o time procura “imitar” o 
ambiente de produção da forma mais fiel possível, para últimos testes 
como os de **desempenho**, **stress** e **carga**.

### Produção

É o ambiente onde o código “final” está rodando e por onde ele é 
acessado e utilizado pelos usuários reais do produto. Mesmo neste 
estágio os times ainda observam e monitoram o comportamento do 
programa em busca de possíveis bugs e/ou comportamentos não esperados; 
ou seja, os testes continuam acontecendo.

## Hooks

Alguns métodos do Jest, estudados em aula, controlavam eventos em 
alguns momentos específicos, como antes de cada teste acontecer ou 
após todos os testes. Chamamos este tipo de função de *hook* (algo como 
“gancho” em português).

As funções hook não são exclusivas do Jest ou mesmo do JavaScript, e 
sim um conceito utilizado em programação no geral. Chamamos de hook 
uma função ou método que é chamado quando queremos dar ao programa um 
comportamento específico em alguma determinada circunstância - por 
exemplo, antes, durante ou depois de determinado código ser executado.

Assim, os exemplos usados, `beforeEach()` e `afterEach()` são 
consideradas funções hooks, pois são executadas em determinados 
momentos/eventos que ocorrem no código e permitem que o comportamento 
do programa “reaja” à estes eventos, alterando o código que será 
executado ou executando algum específico.