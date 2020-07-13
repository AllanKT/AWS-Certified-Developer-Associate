# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span> 

## <span style="color:#884ea0 ">**AWS Fundamentals**</span> 
## <span style="color:#FFC300 ">The Basics of AWS</span> 
---
### <span style="color: #ff5733 ">AWS Global Infrastructure</span> 

#### AWS

* root tem acesso FULL ADMIN na conta;
* não usar a conta root diariamente com admin;
* criar contas com IAM com permissão de admin;
* proteger a root com MFA;
* *aws users*: usuários que podem ser criados, que terão diferentes graus de acesso à conta de produção;
* diferentes formas de acesso:
    * aws console: todas as ações realizadas no console são chamadas de API;
    * aws cli: todas as ações realizadas no cli são chamadas de API, gerenciadas por um API Key configurado;
    * aws sdk: 
* Alguns serviços da AWS trabalham de forma global, sem uma região especifica (IAM, S3, etc);

#### Organização

* **Edge Location**: datacenter que não contem serviços da aws, e sim providencia a entrega de conteudo pelo globo;
    * CloudFront: é um CDN;
* **Region**: Agrupamentos independentes separando datacentes pelo globo;
* **Availability Zones (AZs)**: Providênciam "High Availability" e "Fault Tolerance"; Desenham a arquitetura conforme leis e regulamentações especificas das partes do mundo;
    * trabalham juntos em uma região para prover os recursos da AWS;
    * aplicações multi-AZ provem "Fault Tolerance" e "Failover";
    * AZs, de uma msm região, possuem baixa latência entre si, mas são isoladas para garantir a "Fault Tolerance";
* **Datacenters**: 2 ou mais datacenters compõem uma AZ;

### <span style="color: #ff5733 ">AWS Shared Responsibility Security Model</span>

* Lambda é um serviço totalmente gerenciado que permite que a aws lide com a responsabilidade pelo sistema operacional;

* **Trusted Advisor**: _
* **Security Groups**: _

### <span style="color: #ff5733 ">AWS Compute Overview</span>

* **EC2**: virtualização de servers provisionados;
    * Montar um OS ocm suas partes;
    * instalar diferentes partes do OS;
* **ECS**: serviços de gerenciamento de containers;
    * gerenciar imagens de containers;
    * rodar essas imagens em algum local (EC2);
    * similar ao kubernetes;
* **Lambda**: serverless;
    * menos gerenciamento e controle;
    * upload do codigo, e a AWS faz o gerenciamento do OS que executa;
* **Elastic Beanstalk**: Solução PaaS;
    * auxilia no deploy de aplicações (similar ao Heroku);

### <span style="color: #ff5733 ">AWS Storage Overview</span>

* **S3**: Serviço de armazenamento de Objetos;
* **RDS**: Serviço para bancos de dadso relacionais;
* **DynamoDB**: Banco de dados não relacional;
* **RedShift**: Data Warehousing escalavel;
* **ElasticCache**: Engine de banco in-memory para cache de dados;

<span style="color: #2980b9 ">**QUIZ: AWS Fundamentals Quiz for Developers**</span>
 
**1**: Which of the following statements about Availability Zones, Regions or Edge Locations is FALSE:

 * Availability Zones have low latency connections between Availability Zones in different regions (Availability Zones have low latency connections between Availability zones in THE SAME region, not other regions.)

**2**: When interacting with AWS, most services will allow you to create resources within an AWS region. Which of the following services is an exception that only allows you to interact with it at the "Global" level?

 * AWS IAM (When working with IAM you are creating Users, Groups, and Roles at the "Global" level. While users can be restricted to specific regions, you will still be creating those resources at the account level - not within a specific region.)

**3**: What statements are true about Availability Zones (AZs) and Regions?

* AZs are geographically separated inside a region to help protect against natural disasters affecting more than one at a time. (AZs are separated inside an AWS Region (sometimes by hundreds of miles))

* There are (almost always) two or more AZs in each AWS Region (For high availability and fault tolerance, there are almost always more than one AZ in each region.)

**4**: The AWS shared security responsibility model means that:

* AWS has a list of things for which it will assume responsibility and a list for which you will have to be responsible. (AWS will take care of things like the hardware layer and below (data center security, environmental control, etc.))

**5**: Where can you deploy EC2 instances into?

* Specific AWS Availability Zones (This is one of the correct answers! You can specify a particular Availability Zone when creating EC2 instances.)

* Specific AWS Region (This is one of the correct answers! You can specify a particular AWS region to create an EC2 instance within.)

* <span style="color:  #c0392b  ">Specific AWS Edge Locations (Sorry! Edge locations are used as part of CloudFront to cache data more closely to requestors. They do not actually contain any AWS services themselves.)</span>