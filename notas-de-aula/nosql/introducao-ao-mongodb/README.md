# MongoDB: uma alternativa aos bancos relacionais tradicionais

O [MongoDB](https://www.mongodb.com/what-is-mongodb) é um sistema de 
gerenciamento de banco de dados (DBMS) não relacional, baseado em 
software livre, que utiliza documentos flexíveis em vez de tabelas e 
linhas para processar e armazenar várias formas de dados. Como uma 
solução de banco de dados NoSQL, ele não requer um sistema de 
gerenciamento de banco de dados relacional (RDBMS), portanto, ele 
oferece um modelo de armazenamento de dados **elástico**, que permite 
aos usuários armazenar e consultar tipos de dados variados com 
facilidade. Isso não apenas simplifica o gerenciamento do banco de 
dados para os desenvolvedores, como também cria um ambiente altamente 
escalável para aplicativos e serviços multiplataforma.

## Casos de uso

### Aplicativos para dispositivos móveis

O modelo de documento JSON do MongoDB permite armazenar dados de 
aplicativos backend onde quer que seja necessário, incluindo em 
dispositivos Apple iOS e Android, além de soluções de armazenamento 
baseadas em cloud. Esta flexibilidade permite agregar dados em diversos 
ambientes, com índice secundário e geoespacial, proporcionando aos 
desenvolvedores a capacidade de escalar seus aplicativos mobile de 
maneira intuitiva.

### Análises em tempo real

À medida que as empresas expandem suas operações, obter acesso às 
métricas chave e *insights* de negócios a partir de grandes conjuntos 
de dados torna-se algo crítico. O Mongo faz facilmente a conversão de 
documentos JSON e similares, como BSON em objetos Java, tornando a 
leitura e gravação de dados no MongoDB rápida e incrivelmente eficiente 
durante a análise de informações em tempo real em vários ambientes de desenvolvimento. Isso tem mostrado benefícios para vários setores de 
negócios, incluindo governo, serviços financeiros e de varejo.

### Sistemas de gerenciamento de conteúdo

Os sistemas de gerenciamento de conteúdo (CMS) são ferramentas 
poderosas que possuem um papel importante em assegurar experiências de 
usuário positivas ao acessar sites de e-commerce, publicações on-line, 
plataformas de gerenciamento de documentos e outros serviços e 
aplicativos. Ao usar o MongoDB, você pode facilmente incluir novos 
recursos e atributos em seus aplicativos e sites on-line por meio de 
um único banco de dados e com alta disponibilidade. 

Essas são apenas algumas de suas várias utilidades!

### Comparativo com SQL

| MongoDB | SQL |
| ------- | ---- |
| documentos | linhas |
| campos, chaves/valores | colunas |
| coleções | tabelas |

## Criando coleções e registros

No MongoDB não trabalhamos com estruturas fixas como as tabelas, e sim 
com as chamadas coleções, estas são as unidades básicas de dados. 
Formatados como **Binary JSON** (*Java Script Object Notation*), esses
documentos podem armazenar vários tipos de dados e serem distribuídos 
para diversos sistemas. 

Como o Mongo emprega um design de esquema dinâmico, os usuários têm 
uma flexibilidade incomparável ao criar registros de dados, consultar 
coleções de documento por meio da agregação do MongoDB e analisar 
grandes quantidades de informações.

⚠️ *Mas o que pode acontecer com os nossos dados?*

- A consistência pode ser eventual;
- Pode haver duplicação e inconsistência entre campos usados como 
links de documentos;

Mas compensação, ganhamos desempenho e escalabilidade. A aplicação 
torna-se responsável pela integridade dos dados duplicados.

➜ Para criar uma coleção, "chame" o banco de dados (db, de *database*)
e informe o que quer, nesse caso, criar uma coleção e por fim, informe
o nome dessa nova *collection*:

```js
db.createCollection("alunos");
```

Com a coleção criada, podemos seguir para inserir registros nela com a seguinte notação:

```js
db.alunos.insertOne({
  "nome": "Ana",
  "data_nascimento": new Date(2000, 02, 23),
  "curso": {
    "nome": "Sistemas de informação"
  },
  "notas": [10.0, 9.0, 4.5],
  "habilidades": [
    {
      "nome": "inglês",
      "nivel": "básico"
    }
  ]
});
```

➜ Repare que chamamos o db, informamos qual coleção queremos adicionar
um novo registro e o método correspondente a inserção de um documento.
E, levando em conta que o `.insert()` está descontinuado, podemos 
utilizar:

- `.insertOne()` para inserir um documento;
- `.insertMany()` para inserir vários documentos;
- `.bulkWrite()` para executar várias operações de gravação com 
controles para ordem de execução;

➜ Agora para vermos nossa collection, colocamos:

```js
db.alunos.find();

// ou, para trazer os dados organizados:
db.alunos.find().pretty();

// retorno:
[
  {
    "_id": ObjectId("64591cf0a3a2f50208f76069"),
    "nome": "Ana",
    "data_nascimento": ISODate("2000-03-23T03:00:00.000Z"),
    "curso": {
      "nome": "Sistemas de informação"
    },
    "notas": [10.0, 9.0, 4.5],
    "habilidades": [
      {
        "nome": "inglês",
        "nivel": "básico"
      }
    ]
  }
]
```

➜ Já para removermos determinado documento, usamos:

```js
db.alunos.deleteOne({
  "_id": ObjectId("64591cf0a3a2f50208f76069")
});
```

E levando em consideração que `.remove()` foi descontinuado, podemos
usar:

- `.deleteOne()` para deletar um documento;
- `.deleteMany()` para deletar vários documentos através de um filtro;
- `.findOneAndDelete()` para deletar baseado em um filtro e sort;
- `.bulkWrite()` para executar várias operações de gravação com 
controles para ordem de execução;

## Consultando e filtrando dados

Como já vimos, o `.find()` traz tudo o que está em determinada coleção,
mas podemos precisar de algo mais específico, para isso, informamos
como parâmetro, que dado queremos encontrar nos documentos:

```js
// traz todos os documentos com nome correspondente
db.alunos.find({
  "nome": "Ana"
});

// para campos mais internos, basta usar a notação de ponto do JS
// e para campos extras, é só adicionar o campo desejado
db.alunos.find({
  "habilidades.nome": "inglês",
  "habilidades.nivel": "básico"
});
```

## Consultas com OR, AND e IN

Fazer consultas no Mongo utilizando o `.find()` é super rico em
possibilidades, por isso a [documentação](https://www.mongodb.com/docs/v3.0/reference/method/db.collection.find/)
é uma aliada importante para aproveitar essa variedade, uma delas, na 
qual podemos querer mais de um resultado utilizando o **OR**, a sintaxe é:

```js
db.alunos.find({
  $or: [
    { "curso.nome": "Moda" },
    { "curso.nome": "Ciência da computação" }
  ]
});
```

Já para as consultas com **AND**, basta inserir, fora do escopo do 
`$or`, por exemplo:

```js
// retorna alunas com nome Juliana E que está em um OU ambos os cursos
db.alunos.find({
  $or: [
    { "curso.nome": "Moda" },
    { "curso.nome": "Ciência da computação" }
  ],
  "nome": "Juliana"
});
```

Por fim, temos o **IN** (`$in`), que no SQL é usado quando temos vários 
OR na query. Utilizando a mesma query anterior, a sintaxe fica um pouco 
diferente:

```js
db.alunos.find({
  "curso.nome": {
      $in: ["Moda", "Ciência da computação"]
  },
  "nome": "Juliana"
});
```

## Atualização completa e parcial de documentos










## Comandos

```bash
help # exibe principais comandos do Mongo Shell
show dbs # lista todos os BDs do servidor mongod
show collections # lista todas a coleções de um BD
use <db_name> # conecta ao BD especificado
rs.help() # exibe os comandos relacionado ao ReplicaSet
sh.help() # exibe os comandos relacionado ao Sharding
```


#### Observações

- **Sharding** (Particionamento de dados): é um dos métodos utilizados 
para a obtenção de escalabilidade horizontal. O conjunto de dados é 
dividido em diferentes partes (*shards*) e essas partes são 
distribuídas em servidores distintos;

- **ReplicaSet** (Conjunto de Réplicas): é um grupo de servidores
(mongod) que hospedam/armazenam o mesmo conjunto de dados;

<h4 align="center">🚧 Readme em construção 👷🏻‍♀️</h4>