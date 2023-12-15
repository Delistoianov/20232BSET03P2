# Documentação atividade prova
Inteli - Engenharia de Software | Avaliação 2023-2B P2

No readme, descreva as vulnerabilidades identificadas e as medidas adotadas para corrigir cada uma delas

Vulnerabilidades identificadas: 

1. Funcionamento incorreto da lógica.
2. Operados "${}" em requisições POST são portas de entrada para SQL injection.


Medidas adotas:

1. A lógica do código está condizente com a estrutura antiga, no entanto, agora está em funcionemento. A lógica está descrita abaixo:

    1. Usuário faz um post no body, que espera receber a chave "name" e o valor "cats" ou "dogs" a depender do endpoint em questão.
        * Como resposta se espera:
        `            {
  "id": 1,
  "name": "dogs",
  "votes": 0
} ou {
  "id": 1,
  "name": "cats",
  "votes": 0
}
`
    2. Após isso pode-se fazer um get, para testar a funcionalidade do votar.
        * Como resposta se espera:
    `  {
    "id": 1,
    "name": "cats",
    "votes": 0
  } ou {
    "id": 1,
    "name": "dogs",
    "votes": 0
  } `

    3. Usuário vota em algum dos dois bixos:
        * Como resposta espera-se:
        `""Voto computado"`

    4. Para mostrar que o funcionamento está correto, agora pode-se fazer um get novamente.
        * Como resposta espera-se:
    ` {
    "id": 1,
    "name": "dogs",
    "votes": 1
  } ou     "id": 1,
    "name": "cats",
    "votes": 1`

    Observe que agora os dados foram computados.

2. Melhora na segurança:

* Para evitar ataques de SQL injection foi retirado os operadores "${}" dos endpoints POST que continham body. Para previnir esse tipo de problema a tag "${}" foi substituida por "(?, 0)", que é um metodo mais seguro

* Além disso, utilizei a biblioteca express-validator para validar parâmetros das rotas,   
