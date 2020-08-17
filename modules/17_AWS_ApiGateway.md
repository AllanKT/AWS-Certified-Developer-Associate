# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Application Services**</span>
## <span style="color:#FFC300 ">API Gateway</span>

---
### <span style="color: #ff5733 ">API Gateway Essentials</span>

* **Api Gateway Essentials**:
    * serviço que permite criar e gerenciar apis
    * age como um "front door" para a aplicação, permitindo acesso ao backend

* *Main Features*:
    * RestApi com resources, metodos e settings
    * deploy de apis com stages (throttling, caching, meteringe logging) em diferentes ambientes (dev, stage, prod, etc)
    * versiona api, clonando existentes
    * rollback para versões anteriores
    * nomes de dominio customizaveis
    * API keys para acesso e analisa o uso da key pelo CloudWatch
    * metricas de estrangulamento, baseado em numeros de requisições por segundo
    * segurança com Signature v.4 de autorização as apis

* *Benefits*:
    * cache de respostas
    * Proteção contra DDoD com CloudFront
    * SDK
    * suporta swagger
    * request/reponse transformação de dados

* **Resources**:
    * entidade logica usada para acessar via path
    * *URLs*:
        * usada para expor o resource
        * o stage aparece por padrão no endpoint
        * dominios simplificam a url
        * resources podem possuir resources filhos associados a metodos http
        * Example: https://*domain*.execute-api.*region*.amazonaws.com/*stage*/*resource*/*child-resource*

* **Methods**:
    * metodos http para cada recurso (get, put, post, delete, any)
    * podem responder utilizando, lambda, http existente, serviço aws, entre outros

### <span style="color: #ff5733 ">API Gateway Deployments and Stages</span>

* **Deployments**:
    * snapshots dos resources e methods das apis
    * criados e associados com um stage

* **Stages**:
    * referenciados pelo lifecycle status da api (dev, prod, beta)
    * mapeia o deploy em ordem
        * habilita cache
        * customiza requisição de estrangulamento
        * configura log
        * define stage dos ambientes

### <span style="color: #ff5733 ">API Gateway Caching and Monitoring</span>

* **Caching**:
    * pode cachear respostas, onde requisições não precisam chegar na api
        * reduz chamadas ao backend
        * chamadas rapidas
    * pode configurar o cache key e o TTL

* **Cloudwatch**:
    * deve ser usado para monitorar o api gateway
    * regras de estrangulamento são monitoradas pelo Cloudwatch
    * metricas de monitoramento (caching, latency, detected erros)
    * niveis de metodos podem ser monitoradas
    * alarmes baseados em metricas

<span style="color: #2980b9 ">**QUIZ**</span>

**1**: An API Gateway Stage refers to:

* A snapshot of your API including methods, integrations, models, mapping templates, and Lambda authorizers. (A stage is represented by a Stage resource and represents a snapshot of the API, including methods, integrations, models, mapping templates, and Lambda authorizers. )

* <span style="color:  #c0392b ">A specific snapshot of your resources and methods (This is actually called a "deployment")</span>

**2**: When you update an API in an API Gateway deploy, you must redeploy the API to what? (Choose 2)

* An existing stage

* A new stage

**3**: With AWS Step Functions, all the work in your state machine is done by tasks. These tasks performs work by using what types of things? (Choose the best 3 answers)

* Passing parameters to API actions of other services (Passing parameters allows further integration with other services. Video for reference: Step Function Essentials)

* Activities (Activities (which can be things such as EC2, ECS, or even mobile applications), can be configured to work with task states!)

* An AWS Lambda Function Integration (A Lambda function is a type of task state! Lambda functions can be directly integrated with Step Functions inside of a state machine task state.)

* <span style="color:  #c0392b ">An EC2 Integration (While EC2 can be an "activity" (which is a type of task state), EC2 itself isn't considered a type of task state. Video for reference: Step Function Essentials)</span>
