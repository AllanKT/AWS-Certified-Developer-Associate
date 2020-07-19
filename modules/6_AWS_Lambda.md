# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>

## <span style="color:#884ea0 ">**AWS Serverless Based Compute Services**</span> 
## <span style="color:#FFC300 ">AWS Lambda</span> 
---
### <span style="color: #ff5733 ">Lambda Essentials</span>

* **AWS Lambda** roda códigos sem necessidade de gerenciamento de quaisquer servidores e infraestrutura;

* Upload da *Lambda Function* (código e dependencias) e a AWS lida com os requisitos de execução e escalonamento que as funções precisarem;

* Lambda é uma plataforma serverless
    * **Serverless**: executar o código sem o provisionamento ou gerenciamento de servidores;
    * Paga pelo tempo de execução (em milisegundos), espaço de memoria por instancia executada;
    * Por padrão, lambda já possui alta disponibilidade, tolerancia a falha, escalabilidade, elasticidade e custo beneficio;
* *Lambda Functions* | *Lambda Funcitons Packages*: conceitos fundamentais do Lambda, consistindo de:
    * código;
    * dependencias (bibliotecas, configurações, etc);
* Facilmente integrado com demais serviços da AWS

* **Blueprints**: Variedade de lambdas functions já disponibilizados pela AWS

* **Serverless Application Repository (SAR)**: Similar ao Blueprint, porém este é um repositorio de lambda fucntions publicados por desenvolvedores, empresas e parceiros da AWS;

### <span style="color: #ff5733 ">Lambda Functions and Events</span>

* **Lambda Events** são lambda functions ativadas sob um determinado evento, sendo variado entre diferentes coisas:
    * HTTP API request pelo API Gateway
    * Eventos agendados pelo Cloudwatch
    * upload de arquivos no S3
    * mudanças pelo Dynamo Stream
    * Invocações diretas pelo CLI ou CDKs
    * entre outros...

* **Lambda Functions**:
    * Consiste de:
        * Código da aplicação
        * dependencias (bibliotecas, configurações, etc)

    * **Modelo de programação**:
        * Todas as linguagens executam com conceitos similares:
            * Handler files/functions: ponto de entrada para execução do Lambda;
            * Eventos: dados passados peara a lambda functios quando ativadas;
            * Context: informações em tempo de execução, como o tempo restante, requestID, etc;
            * Logging e Exceptions: sempre comunicados através do Cloudwatch, comunicando sucesso ou falha para a AWS
            * Runtime-specific concepts: Há algumas diferenças e conceitos unicos de tempo de execução, como o callback do NodeJs que é usado para retornar informações de volta ao solicitante;

    * **Tipos de chamada**:
        * quando uma função é chamada diretamente pelo Lambda Invoke API, é selecionado um tipo de invocação:
            * *Synchronous*: Esperar o valor de retorno e devolve ele
            * *Asynchronous*: Não esperar o valor de retorno e descarta ele
    
        * Quando chamado por um evento, o tipo de invocação é determinado peli serviço que está chamando a funcção;

### <span style="color: #ff5733 ">Lambda Function Configuration</span>

* Configurações de um Lambda Fucntions:
    * Linguagem: Nodejs, Java, Python, .NET Core, Go e Ruby
    * Handler:
        * Cada função possui um arquivo e função principal;
        * formato: *filename.functionname*
    * Memory: 
        * 128 MB à 3008 MB (incrementado em 64 MB cada)
        * escalonamento de alocação de CPU em memoria
    * Maximum execution duration:
        * 900 seg (15 mins) (incrementado em 1 segundo cada)
    * Permissions:
        * IAM Roles permitem que funções lambda tomem ações sob outros recursos da AWS
        * Recursos baseados em acesso controlado por policies permitem que outros serviços e contas externas possam invocar ou tomar ações sob Lambda Functions;
    * Environment Variables:
        * Par de chave-valor
        * pode ser criptografado usando KMS
    * AWS Virtual Private Cloud (VPC): Concede acesso a VPCs configuradas, juntamente com suas respectivas Subnets e Secutiry Groups;
    * Dead Letter Queues: Configuração de SQS ou SNS para aceitar dados de funções que falharam anteriormente
    * Concurrency: número máximo de invocações concorrentes da função
    * Tags: par de chave-valor, que ajuda a organizar as funções na conta AWS

### <span style="color: #ff5733 ">Lambda Function Packages</span>

* **Function Packages** | *deployment packages*: são códigos e dependencias da Lambda Function empacotados em zip packages, incluindo:
    * Arquivo handler
    * bibliotecas ou pacotes
    * qualquer outro codigo integrao com o handler
    * pacotes de terceiros, providos por um gerenciados de pacotes, como npm ou pip;

### <span style="color: #ff5733 ">Lambda Versions and Aliases</span>

* Lambda disponibiliza duas ferramentas para gerenciar seu codigo em produção:
    * **Versions**:
        * Lambda Versions são versões distintas das funções, armazenadas na AWS onde cada uma delas possui seu próprio ARN
        * Cada versão é chamada por **$LATEST** - literalmente chamadas $LATEST, sendo apenas a versão mutavel;
        * Cada versão possui um número de versão (1, 2, ...)
            * As versões numeradas recebem um número começando com um e cada versão subsequente é incrementada em um;
            * Números das versões são imutaveis;
        * Por cada versão ter ARNs unicos, permite que as Lambda Functions possam ser gerenciadas facilmente entre os diferentes ambientes (Prod, Stage, Dev, etc);

    * **Aliases**:
        * Lambda Aliases são um tipo de ponteiro que referencia uma Lambda Version especifica;
        * Usando aliases, é possivel invocar uma função sem o conhecimento de qual versão etá sendo referenciada;
        * Alias tem um ARN estático, mas pode apontar para qualquer versão da mesma função
        * Alias também podem ser utilizados para separar o trafego entre Lambda Versions
    
* Beneficios de Versions e Aliases:
    * Facilidade do fluxo de desenvolvimento e gerenciamento de estagios
    * Evitar ter que reconfigurar eventos, pois podem apenas apontar para o alias da função
    * Voltar para uma versão anterir facilmente, ajustando a função que o alias aponta
    * Usar o alias para dividir o trafego entre versões que pode ajudar a testar novas versões em produção
