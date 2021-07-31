### On13 MONGO - DB  | Introdução ao Banco de Dados

Aluna : [Ana Paula Lima ](https://www.linkedin.com/in/ana-paula-lima-3269214b/#) 

Prof.: Vanessa Jansen

<br>Essa semana vamos iniciar no uso do banco de dados, primeiramente aprendemos sobre a historia, criação e como acessar as informações <br />

# Demandas:

- Você deve criar um banco de dados novo (database) e uma coleção com um nome pertinente, de acordo com os dados e tema que você escolher. Os seguintes comandos devem ser feitos e entregues:
  - Inserção de documentos
  - Atualização de documentos
  - Exclusão de documentos
  - Consulta com projeção
  - Consulta utilizando combinação entre os seletores
  - Consulta paginada e ordenada (utilizar *skip*, *limit* e *sort*)

<h4> Resolução: </h4>



- Criado um banco de dados Travel e uma collections Agendamentos:

![image-20210730210311594](C:\Users\Paula\AppData\Roaming\Typora\typora-user-images\image-20210730210311594.png)

- Efetuada a inserção dos dados:

```
db.Agendamentos.insertMany([
    {
        "id": "jIan-LdcKJa2hj2zJ1m_",
        "durationPrediction": "08:27min",
        "stops": "1",
        "derpature": {
            "local": "São Paulo",
            "time": "Nov 02 2021 22:00:00"
        },
        "destination": {
            "local": "Rio de Janeiro",
            "time": "Nov 03 2021 06:27:00"
        },
        "busInfos": {
            "registerNumber": "979620",
            "capacity": "40"
        },
        "driverInfos": {
            "id": "iIt_aijKGGf-wibaF7i12m-hs",
            "name": "Gustavo Henrique Melo",
            "license": "41713-4219"
        },
        "passengersInfos": [
            {
                "id": "EfL80lA1y3gstpclKL9w-g-3u",
                "name": "Maria Cecília da Conceição",
                "email": "mariaconceicao@email.com",
                "documentNumber": "899439400"
            },
            {
                "id": "3bq-Kkvf8Cd3Ks08p_zhwj_gl",
                "name": "Catarina Mendes",
                "email": "catarinamendes@email.com",
                "documentNumber": "933097178"
            },
            {
                "id": "cedinAHGhyjjwGKulty_q1GqD",
                "name": "Pietro Pires",
                "email": "pietropires@email.com",
                "documentNumber": "974685470"
            },
            {
                "id": "p05z6iL-_hooI-9qxAe4wHFpJ",
                "name": "André da Luz",
                "email": "andreluz@email.com",
                "documentNumber": "547679013"
            },
            {
                "id": "L9oxoChtuLGhFzlhxwl6C190x",
                "name": "Camila Fernandes",
                "email": "camilafernandes@email.com",
                "documentNumber": "561205047"
            },
            {
                "id": "153p9rtjpa",
                "name": "Josélia Catarina",
                "email": "joseliacatarina@email.com",
                "documentNumber": "984763498",
                "travelId": "jIan-LdcKJa2hj2zJ1m_"
            },
            {
                "id": "n4pe14qtph",
                "name": "Roberta Viana",
                "email": "robertaviana@email.com",
                "documentNumber": "84392739502"
            },
            {
                "id": "3d1kqt8bf68",
                "name": "Aline Rodrigues da Silva",
                "email": "alinerodrigues@email.com",
                "documentNumber": "829842019"
            }
        ]
    },
```



- Buscar viagens com destino local Rio de Janeiro:

```
db.getCollection('Agendamentos').find({'destination.local':'Rio de Janeiro'})
```

- Buscar um passageiro em um array usando elemMatch:

```
db.getCollection('Agendamentos').find({'passengersInfos' : {$elemMatch:{name: "Arthur Moura"}}})
```

- Buscando dois motoristas em viagens diferentes usando o $in:

```
db.getCollection('Agendamentos').find({ 'driverInfos.name': { $in: ["Emanuel Alves", "Gustavo Henrique Melo"] } } )
```

- Buscando dois passageiros diferentes usando o $or:

```
db.getCollection('Agendamentos').find({ 'passengersInfos': {$elemMatch:{ $or: [{name:"Maria Cecília da Conceição"}, {name:"Davi Luiz da Mota"}] } } })
```

Atualização do numero da licença do motorista:

```
db.getCollection('Agendamentos').update(
    {
        "driverInfos.name" : "Gustavo Henrique Melo"
    }, 
    {
        $set: {
            "driverInfos.license": "1234567890"
        }
    },
  {
        "multi" : true,
    }
);
```

Excluir todas as viagens que não possuem o id jIan-LdcKJa2hj2zJ1m_

```
db.getCollection('Agendamentos').remove({
    "id": { $ne: "jIan-LdcKJa2hj2zJ1m_" }
})

```

