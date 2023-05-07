# Consultas SQL: avançando no SQL com MySQL

O principal objetivo da linguagem SQL é padronizar a maneira como os registros são consultados nos bancos de dados relacionais. Atualmente, os bancos relacionais aderem ao padrão SQL, que vai além das consultas: é usado também, na criação, alteração, estruturação e manipulação do banco de dados, além da maneira como banco de dados interage com a segurança, entre outros usos.

## Conteúdos

- [Vantagens](#chat_with_upwards_trend-vantagens)
- [Desvantagens](#chat_with_downwards_trend-desvantagens)
- [Comandos](#clipboard-comandos)
  - [LIKE](#like)
  - [DISTINCT](#distinct)
  - [LIMIT](#limit)
  - [ORDER BY](#order-by)
  - [GROUP BY](#group-by)
  - [CASE](#case)
  - [JOIN](#join)
  - [UNION E UNION ALL](#union-e-union-all)
  - [NOT](#not)
  - [IN](#in)
- [Views](#page_facing_up-views)
- [Observações](#memo-observações)
- [Cheat sheet](#toolbox-cheat-sheet)

## :chat_with_upwards_trend: Vantagens

Entre as vantagens do banco de dados relacional, a primeira é que essa padronização utilizando a linguagem SQL tem um custo reduzido do **aprendizado**. Por exemplo, o profissional com conhecimento sobre o SQL da Oracle conseguirá manipular facilmente o MySQL ou SQL Server da Microsoft. Por mais que existam diferenças, principalmente na parte de funções, a adaptação do profissional não é uma questão complicada.

Outra vantagem, é a **portabilidade**. Por exemplo, é mais simples migrar sistemas que usam Oracle para SQL Server ou para MySQL, ou vice-versa. Lembrando que quanto mais for utilizado o SQL Standard definido pelo ANSI (*American National Standard Institute*, estabeleceu alguns padrões para as consultas dos bancos de dados relacionais), mais fácil será essa portabilidade no futuro. Então, é útil evitar as funções específicas do banco de dados e permitir que o programa realize essa tarefa.

Já a **longevidade** é a garantia de que os seus relatórios ou processos utilizando o SQL irão funcionar por um longo período, já que estarão sempre adaptados ao padrão ANSI. Ou seja, ao efetuar um upgrade de banco de dados o seu sistema não ficará fora de serviço.

Outro benefício é a comunicação. O fato da maioria utilizar SQL permite a facilidade de comunicação entre os sistemas. Como, por exemplo, processos de ETL (*extract, transform and load*), ou de integração entre sistemas que ficam mais simples de serem desenvolvidos, já que ambos utilizam o SQL padrão.

Por último temos a **liberdade de escolha**. Por existir um padrão de linguagem, se a empresa for optar pelo uso de um banco de dados relacional não ficará presa à linguagem de comunicação, por exemplo, já que são bem semelhantes. Ao tomar essa decisão, a corporação irá utilizar outros critérios de escolha, como performance, *hardware*, custo, entre outros.

## :chat_with_downwards_trend: Desvantagens

A primeira é a privação da **criatividade**. O SQL possui limitações que podem não atender às novas demandas no mercado na linguagem SQL, principalmente com o surgimento das redes sociais e dos enormes volumes de dados, o chamado *big data*. Ou seja, há uma carência nas coletas de dados que estão trafegando na internet. Para tal, estão surgindo outros bancos que usam padrões diferentes dos bancos de dados relacionais, o chamado **NoSQL**. Estes atendem de forma mais eficiente as demandas de tabelas de *big data*, como no caso das redes sociais. Lembrando que estamos nos referindo a estruturas que escapam do padrão ANSI e que, por isso, exigem um aprendizado mais específico.

Outro ponto é a escassez de **estruturação** da linguagem SQL, já que ela não possui *if*, *for* e *when*, isto é, comandos condicionais como as demais linguagens de programação. Para conseguir suprir essa carência da estruturação, os bancos de dados relacionais da Oracle, SQL e MySQL criaram suas linguagens próprias internas que realizam esse conjunto de estruturação usando a linguagem SQL, mas que acaba se afastando um pouco do padrão ANSI.

## :clipboard: Comandos

Falando um pouco sobre o padrão ANSI, este possui três grupos de comandos. O primeiro, é o **DDL** ou *Data Definition Language* (linguagem de definição de dados). Os DDLs são a parte da linguagem SQL que permite a **manipulação das estruturas do banco de dados**, como criar um banco, tabelas, índices, apagar as tabelas e alterar a política de crescimento de índice. Ou seja, os comandos que envolvem a estrutura do banco de dados relacionais são os comandos do tipo DDL.

O segundo grupo de comandos são os chamados **DML**, ou *Data Manipulation Language* (linguagem de manipulação de dados). Esse grupo visa **gerenciar os dados: incluindo, alterando e excluindo informações nas estruturas do banco**, como as tabelas. Além disso, realizam as consultas, buscam as informações das estruturas e exibiremos para o usuário.

E por fim, os comandos **DCL**, ou *Data Control Language* (linguagem de controle de dados). Este grupo nos permite **administrar o banco de dados**, como o controle de acesso, o gerenciamento do usuário, gerenciar o que cada usuário pode ou não visualizar, gerenciar o banco ao nível de estrutura (como a política de crescimento, como e onde será armazenado no disco), administrar os processos, saber quantos processos estão sendo executados, controle de log e assim por diante.

A seguir comentarei um pouco sobre alguns comandos importantes suportados pelo MySQL.

### LIKE

O *LIKE* é usado para fazer buscas em uma coluna. Geralmente usado juntamente com o símbolo de porcentagem (%) para representar qualquer registro genérico, exemplo:

```sql
-- seleciona todos os nomes que *contenham* Soares
SELECT * FROM clientes WHERE nome LIKE '%Soares%';

-- seleciona todos os nomes que *terminam* com Soares e antes pode ser qualquer coisa
SELECT * FROM clientes WHERE nome LIKE '%Soares';

-- seleciona todos os nomes que *começam* com Ana e depois pode ser qualquer coisa
SELECT * FROM clientes WHERE nome LIKE 'Ana%';
```

### DISTINCT

O *DISTINCT* é usado para trazer apenas os resultados diferentes entre si, sem repetição das mesmas propriedades.

```sql
SELECT DISTINCT sabor FROM sucos;
```

### LIMIT

O *LIMIT* é usado sempre no fim da query, ele delimita a quantidade de resultados trazidos por uma consulta.

```sql
-- retorna 10 resultados
SELECT * FROM sucos WHERE capacidade > '700ml' LIMIT 10;

-- retorna 3 resultados, começando pela segunda linha (incluso)
SELECT * FROM sucos WHERE capacidade > '700ml' LIMIT 2,3;
```

### ORDER BY

O *ORDER BY* ordena os resultados dado determinado campo, se não especificado, a ordenação acontece de maneira ascendente (ASC, do menor para o maior). Também é possível a ordenação por mais de um campo, neste caso, a ordenação será do primeiro ao último campo.

```sql
-- resultado na ordem alfabética
SELECT * FROM clientes ORDER BY nome;

-- resultado na ordem inversa a alfabética
SELECT * FROM clientes ORDER BY nome DESC;

-- resultado na ordem alfabética e dentre os iguais do campo nome, a 
-- ordenação acontece pela ordem crescente da idade
SELECT * FROM clientes ORDER BY nome, idade;

-- resultado na ordem alfabética inversa e dentre os iguais do campo 
-- nome, a ordenação acontece pela ordem crescente da idade
SELECT * FROM clientes ORDER BY nome DESC, idade ASC;
```

### GROUP BY

O *GROUP BY* é usado para juntar campos repetidos e no caso dos campos numéricos, quando fazemos essa junção, podemos aplicar uma fórmula matemática como soma (*SUM*), média (*AVG*), mínimo (*MIN*), máximo (*MAX*), quantidade de linhas (*COUNT*) etc. Falando nas fórmulas, quando omitimos a agregação, ela é aplicada para toda a tabela.

```sql
-- agrupando os resultados pela categoria e quando forem iguais, 
-- somamos os campos de preço
SELECT categoria, SUM(preco) FROM produtos GROUP BY categoria;

-- somamos todos os campos de preço da tabela
SELECT SUM(preco) FROM produtos;

-- podemos agrupar por mais de um campo, nesse caso o clientes são 
-- agrupados por bairro e estado, para informar a quantidade de clientes 
-- e apresentar essas informações em ordem crescente de bairro
SELECT bairro, estado, COUNT(*) AS quantidade_clientes 
FROM clientes GROUP BY bairro, estado
ORDER BY bairro;
```

### HAVING

*HAVING* é uma condição que se aplica depois do resultado de uma agregação, ou seja, um *SELECT* que é agrupado.

```sql
-- agrupando os resultados pela categoria, quando forem iguais, somamos 
-- os campos de preço e, por fim, obtemos apenas as somas superiores a 20
SELECT categoria, SUM(preco) AS preco_total FROM produtos 
GROUP BY categoria HAVING preco_total > 20;
```

### CASE

*CASE* é um comando para fazer testes em um ou mais campos e, dependendo do resultado, teremos um ou outro valor. Lembrando que no *THEN* podemos ter um valor, um texto, uma conta etc. Assim como, podemos usar um case no *GROUP BY*.

```sql
-- estamos definindo o que cada intervalo de nota significará de maneira mais clara
SELECT cliente,
CASE
  WHEN nota >= 8 AND nota <= 10 THEN 'ÓTIMO'
  WHEN nota >= 7 AND nota < 8 THEN 'BOM'
  WHEN nota >= 5 AND nota < 7 THEN 'MÉDIO'
  ELSE 'RUIM'
END AS feedback
FROM avaliacoes;

-- agrupados por feedback a quantidade de cada categoria de nota definida
SELECT CASE
  WHEN nota >= 8 AND nota <= 10 THEN 'ÓTIMO'
  WHEN nota >= 7 AND nota < 8 THEN 'BOM'
  WHEN nota >= 5 AND nota < 7 THEN 'MÉDIO'
  ELSE 'RUIM'
END AS feedback, COUNT(*) AS quantidade
FROM avaliacoes
GROUP BY feedback;
```

### JOIN

Comandos de *JOIN* trazem a possibilidade de unir uma ou mais tabelas através de campos em comum. Existem vários tipos de *JOINs*:

- *INNER JOIN*: retorna somente itens correspondentes.

```sql
-- ligando-as através do id
SELECT pessoas.nome, hobbies.hobby FROM pessoas
INNER JOIN hobbies ON pessoas.id_hobby = hobbies.id;
```

- *LEFT JOIN*: retorna todos os campos da tabela da esquerda e somente os correspondentes da direita.

```sql
-- ligando-as através do id, porém retornando todos os campos de pessoas, apenas os correspondentes de hobbies e os não-correspondentes retornam null
SELECT pessoas.nome, hobbies.hobby FROM pessoas
LEFT JOIN hobbies ON pessoas.id_hobby = hobbies.id;
```

- *RIGHT JOIN*: retorna todos os campos da tabela da direita e somente os correspondentes da esquerda.

```sql
-- ligando-as através do id, porém retornando todos os campos de hobbies, apenas os correspondentes de pessoas e os não-correspondentes retornam null
SELECT pessoas.nome, hobbies.hobby FROM pessoas
RIGHT JOIN hobbies ON pessoas.id_hobby = hobbies.id;
```

- *FULL JOIN*: retorna todos os campos de ambas as tabelas.
Não suportado pelo MySQL ⚠️

```sql
-- ligando-as através do id e retornando todos os campos
-- e os não-correspondentes como null
SELECT pessoas.nome, hobbies.hobby FROM pessoas
FULL JOIN hobbies ON pessoas.id_hobby = hobbies.id;
```

- *CROSS JOIN*: retorna o produto cartesiano das duas tabelas, ou seja, todas as combinações possíveis dos campos selecionados.

```sql
SELECT pessoas.nome, hobbies.hobby FROM pessoas, hobbies;
```

### UNION e UNION ALL

O *UNION* faz a união de duas ou mais tabelas e é importante que as tabelas que serão unidas tenham o **mesmo número e tipo de campos**. Temos também o *UNION ALL*, a diferença é que neste não aplica o *DISTINCT* sobre o resultado final da consulta, visualmente, é como ambas as tabelas fossem unidas.

```sql
-- traz os bairros de ambas as tabelas sem repetição
SELECT bairro FROM clientes UNION SELECT bairro FROM vendedores;

-- traz os bairros de ambas as tabelas com repetição
SELECT bairro FROM clientes UNION ALL SELECT bairro FROM vendedores;
```

↪ Simulando *FULL JOIN* no MySQL com *UNION*
```sql
SELECT pessoas.nome, hobbies.hobby FROM pessoas
LEFT JOIN hobbies ON pessoas.id_hobby = hobbies.id
UNION 
SELECT pessoas.nome, hobbies.hobby FROM pessoas
RIGHT JOIN hobbies ON pessoas.id_hobby = hobbies.id;
```

### NOT

O *NOT* é usado para inverter o resultado de uma expressão lógica, exemplo:

```sql
-- traz apenas clientes fora do intervalo [18, 25]
SELECT * FROM clientes WHERE idade NOT BETWEEN 18 AND 25;
```

### IN

O *IN* é usado para especificar mais de um valor na condição de *WHERE*, como:

```sql
SELECT * FROM produtos WHERE categoria IN ('bebidas', 'frios');

-- equivalente a:
SELECT * FROM produtos WHERE categoria = 'bebidas' OR categoria = 'frios';
```

↪ Mas também, pode ser usado para fazer subconsultas, por exemplo:

```sql
SELECT * FROM livros 
WHERE categoria 
IN (SELECT categorias.name FROM categorias); 
-- equivale a escrever todas as categorias existentes
```

## :page_facing_up: Views

As views são tabelas lógicas, resultado de uma consulta que pode ser usada depois em qualquer outra query.

```sql
CREATE OR REPLACE VIEW 'vw_pessoas_hobbies' AS
SELECT pessoas.nome, hobbies.hobby FROM pessoas
INNER JOIN hobbies ON pessoas.id_hobby = hobbies.id;
```

## :memo: Observações

Condições de filtro (*WHERE*) que possuem a chave primária ou estrangeira, significa que ela tem índice (que pode ser criado para uma coluna), como consequência, a busca será muito mais rápida do que pesquisando por outros campos. Porém, é algo perceptível quando um banco é muito grande.

Quando o filtro for um valor, principalmente com casas decimais, pode ser interessante utilizar o comando *BETWEEN* ao invés do operador igual (=), já que no banco de dados, esses valores não são exatamente o que é mostrado em tabela, e sim, aproximações. Exemplo, queremos buscar por um preço de 19,51 no banco de produtos, mas sabendo que esse valor é uma aproximação, podemos escrever a seguinte query:

```sql
SELECT * FROM produtos WHERE preco BETWEEN 19.50 AND 19.52;
```

## :toolbox: Cheat Sheet

Note que nem todos os comandos apresentados são suportados pelo MySQL, então vale a pena consultar a [documentação](https://dev.mysql.com/doc/) para conferir o que é válido.

<img src="../../../assets/sql-cheat-sheet.jpg" alt="Cheat sheet do SQL">

<h4 align="center">🚧 Readme em construção 👷🏻‍♀️</h4>
