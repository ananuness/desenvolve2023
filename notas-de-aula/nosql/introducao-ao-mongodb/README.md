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

Com a coleção criada, podemos seguir para inserir registros nela com a 
seguinte notação:

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

Para atualizar alguma informação, usamos o `.updateOne()`.

⚠️ **Cuidado**, o update do Mongo não é igual ao update do SQL, na qual
você especifica um campo e muda para outro valor. Caso não informe ao
update que **operação** deseja fazer, ele irá **substituir** o documento
inteiro que está na contido no filtro, para o documento informado no
segundo elemento. Para evitar esse comportamento, faz-se:

```js
// parâmetros: filtro, update, options
// é necessário informar a operação $set
db.alunos.updateMany(
  { "curso.nome": "Sistema de informação" },
  { $set: {
     "curso.nome": "Sistemas de informação"
    }
  }
)
```

Mais operadores interessantes além do `$set` seriam os da categoria
_**Array Update Operators**_, um deles é o `$push`, que adiciona um
novo valor a um array:

```js
// informando que no campo notas queremos adicionar esse novo valor
db.alunos.updateOne(
  { _id: ObjectId("64593e6ca3a2f50208f7606a") },
  { $push: {
     "notas": 8.5
    }
  }
)

// para adicionar vários valores
db.alunos.updateOne(
  { _id: ObjectId("64593e6ca3a2f50208f7606a") },
  { $push: {
     "notas": {
        $each: { [8.5, 3] }
     }
    }
  }
)
```

> Para ver mais sobre esses operadores, vá até a 
> [documentação](https://www.mongodb.com/docs/manual/reference/operator/update-array/).

E levando em consideração que `.update()` foi descontinuado, podemos
usar:

- `.updateOne()` para atualizar um documento dado um filtro;
- `.updateMany()` para atualizar vários documentos através de um filtro;
- `.findOneAndUpdate()` para atualizar baseado em um filtro e sort;
- `.bulkWrite()` para executar várias operações de gravação com 
controles para ordem de execução;

## Buscando e limitando registros

Outras operações que podemos fazer são as de comparação, uma delas é
o 'maior que', *mas como fazer isso no Mongo?*

Lembrando que, 'maior que' em inglês é *Greater Than*, podemos fazer
o seguinte:

```js
// informo que quero apenas os aluno que possuem notas maiores que 5
db.alunos.find({ 
  "notas": { $gt: 5 }
});

// retorna o primeiro documento que satisfazer a condição
db.alunos.findOne({ 
  "notas": { $gt: 5 }
});

// retorna apenas 3 documentos que satisfazem a condição
db.alunos.find({ 
  "notas": { $gt: 5 }
}).limit(3);
```

>Note que podemos usar o `.limit()` para limitar o retorno, substituindo
> até mesmo o `.findOne()`

Outro método interessante do MongoDB é o `.sort()`, que podemos usar
para ordenar nossa busca. Ele recebe como parâmetro um objeto JSON-like:

```js
// irá retornar os documentos em ordem alfabética
db.alunos.find().sort({ "nome": 1 });

// irá retornar os documentos na ordem inversa à alfabética
db.alunos.find().sort({ "nome": -1 });
```

## Endereços, posicionamentos e busca por proximidade

Vamos imaginar que temos em nossa faculdade cerca de 2000 alunos e que 
todos os dias eles se deslocam até o local de estudo. Muitos acabam indo 
sozinhos de carro, metrô, mas vivem relativamente perto. Gostaríamos de incentivar alunos que vivem ou trabalham em regiões próximas a se 
encontrem para irem juntos a faculdade, economizando assim gasolina e 
preservando o meio ambiente. Vamos trabalhar com a ideia de proximidade.

Quando escolhemos um determinado ponto no GoogleMaps e elegemos a opção 
dele nos mostrar estabelecimentos próximos, através do "proximidades" 
temos, portanto, uma busca por proximidade no mapa.

O que queremos fazer com um dos pontos do mapa é mostrar quais são os 
três alunos/pontos mais próximos. Montaremos, dessa maneira, por 
proximidade o esquema de caronas dos alunos. Poderíamos pegar cada 
ponto do mapa por seu endereço, mas esse tipo de referência de 
localização é difícil, pois pode ser alterada, portanto, é pouco confiável. 

Então, usaremos as coordenadas de **latitude** e **longitude** que 
permanecem no mesmo local. Na sequência pegaremos os três alunos mais 
próximos de um outro aluno de referência.

O MongoDB, entretanto, não consegue transformar o endereço que passamos 
em latitude e longitude, quem faz isso é uma API de terceiros. É 
obrigatório acrescentar as coordenadas, mas podemos adicionar outras 
informações adicionais, como, a cidade. 

⚠️ **Atenção**! Se quisermos buscar algum aluno utilizando as suas 
coordenadas temos que seguir um padrão, ele é em inglês. Então, ao em 
vez de "coordanadas" usaremos `coordinates`. Além disso, temos que 
falar qual o tipo de coordenada, nesse caso, é um mero ponto 
(`type: point`):

```js
db.alunos.update(
{ "_id" : ObjectId("56cb0139b6d75ec12f75d3b6") },
{
  $set : {
    localizacao : {
      endereco : "Rua Vergueiro, 3185",
      cidade : "São Paulo",
      coordinates : [-23.588213, -46.632356],
      type : "Point"
    }
  }
});
 ```

Vamos pedir ao Mongo para fazer uma pesquisa de proximidade geográfica, 
ou seja, agregar os dados mais próximos e nos devolver o resultado. 
Vamos utilizar o `aggregate`, para agregar um conjunto de dados. 
Passaremos um dicionário que deve ter alguns parâmetros, o primeiro é 
o tipo de busca que queremos fazer, como é uma **procura por proximidade** usaremos o `$geoNear`. O segundo parâmetro é o `near` que indica que 
queremos aquilo que esteja próximo a uma coordenada específica. Por fim, passaremos também as `coordinates` (longitude e latitude) e o type que 
no caso é `Point`. 

Temos que dizer que ele deve realizar essa busca procurando o campo 
**localização**. Então, temos que criar um índice de busca, o 
`db.alunos.createIndex()` e nele passaremos que a chave localização 
deve ser indexada para uma busca em uma **esfera 2d**, pois contam 
apenas duas dimensões. Teremos o seguinte:

```js
db.alunos.aggregate([
{
  $geoNear : {
    near : {
      coordinates: [-23.5640265, -46.6527128],
      type : "Point"
    }

  }
}
]);

db.alunos.createIndex({
  localizacao : "2dsphere"
});
```

Agora, precisamos mostrar como calcular a distância entre esses dois 
pontos. Teremos que falar ao $geoNear que a forma é `spherical: true`, 
ou seja, que a comparação não deve ser entre as distâncias de uma linha, 
e sim, de uma esfera. Além disso, temos que falar o que deve ser feito 
com a distância, então, temos que criar o campo 
`distanceField: "distance.calculada"`. Teremos o seguinte:

```js
db.alunos.aggregate([
{
  $geoNear : {
    near : {
      coordinates: [-23.5640265, -46.6527128],
      type : "Point"
    },
    distanceField : "distancia.calculada",
    spherical : true
  }
}
]);

db.alunos.createIndex({
  localizacao : "2dsphere"
});
```

Além disso, podemos pedir para que apenas 4 pontos sejam trazidos através 
do `num: 3`. Agora que sabemos como buscar pontos vamos aprender a 
ignorar o primeiro ponto que é o próprio aluno. Vamos adicionar ao 
db.alunos.aggregate o `num: 4` e para pular um, `skip: 1`.

```js
// no final ele não mostra 4 elementos, mas sim 4 - 1
db.alunos.aggregate([
{
  $geoNear : {
    near : {
      coordinates: [-23.5640265, -46.6527128],
      type : "Point"
    },
    distanceField : "distancia.calculada",
    spherical : true,
    num: 4
  }
},
{ $skip: 1 }
]);
```

Vimos um exemplo de utilidade diferente do Mongo como a busca por 
proximidade que pode ser utilizada para resolver problemas em um mapa.

O MongoDB, entretanto, não se limita a busca de dados em uma esfera, 
ele armazena diversos tipos de informação, validar dados, alterar 
completamente um documento e etc.

## Comandos

```bash
# exibe principais comandos do Mongo Shell
help

# lista todos os BDs do servidor mongod
show dbs

# lista todas a coleções de um BD
show collections

# conecta ao BD especificado
use <db_name>

# exibe os comandos relacionado ao ReplicaSet
rs.help()

# exibe os comandos relacionado ao Sharding
sh.help() 

# pede ao mongo para inserir um documento em Array em uma coleção
mongoimport -c <collection_name> --jsonArray < <array_file>.json
```


#### Observações

- **Sharding** (Particionamento de dados): é um dos métodos utilizados 
para a obtenção de escalabilidade horizontal. O conjunto de dados é 
dividido em diferentes partes (*shards*) e essas partes são 
distribuídas em servidores distintos;

- **ReplicaSet** (Conjunto de Réplicas): é um grupo de servidores
(mongod) que hospedam/armazenam o mesmo conjunto de dados;