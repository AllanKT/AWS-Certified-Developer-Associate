# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**Additional Server Based Compute Services**</span> 
## <span style="color:#FFC300 ">AWS Elastic Container Service</span> 
---
### <span style="color: #ff5733 ">ECS Essentials</span>

* **Elastic Container Service (ECS)** é um serviço de containers compativel com o Docker, que permite realizar deploys em instancias EC2 de forma facil e rápida, com alta disponibilidade e tolerancia a falhas;

* ECS é recomendado para distribuição de aplicações em microserviços;

* *Porque usar ECS/Containers?*
    * Criar uma destribuição de aplciações e microserviços:
        * Criar aplicações independentes (microservices);
        * Permite iniciar, parar, gerenciar, monitorar e escalar cada container de forma independente;
    * Batch e Jobs ETL:
        * pacotes batch e jobs etl em containers e realizar deploys em um compartilhamento de clusters EC2;
        * Executar varias versões de um mesmo job ou multiplos jobs no mesmo cluster;
        * Compartilhar a capacidade dos cluster com outros processos e/ou aumentar os jobs dinamicamente sob demanda para melhorar a utilziação dos recursos;
    * CI/CD:
        * Por usar versionamento de imagens Docker, pode usar CI/CD nos containers;
        * Construir processos de bull, build e create de containers das imagens Docker;

* **AWS Fargate**:  
    * Usa containers como bloco de construção principal da aplicação, enquanto AWS gerencia as instancias EC2;

* **Dockerfile**:
    * Arquivo que são especificados todos os componentes que serão incluidos no container;
    * instruções do que serão colocados dentro do container;

* **Container/Docker Image**:
    * Container/Docker Image é o Dockerfile construido
    * Contém todos os downloads de softwares, codigos, bibliotecas, etc;

* **Container Registry**:
    * Repositorio de containers onde as imagens são armazenadas para serem acessadas quando necessário;
        * Localizado na AWS via ECR (Elastic Container Registry);
        * Repositorio de terceiros como Docker Hub;
        * registro proprio;

* **ECS Task Definition**:
    * arquivo JSON que contém o "blueprint" da aplicação, incluindo:
        * Qual container/docker image utilizar;
        * Onde o repositorio de imagens está localizado;
        * Qual porta deve estar aberta na instancia do container;
        * Qual volume de dados deve ser utilizado no container;

    * **ECS Task**:
        * representação do Task Definition na instancia EC2 dentro do cluster de containers;
        * ECS Agent pode iniciar/parar tarefas baseadas em instruções/agendamentos;

    * **ECS Agent**:
        * Executa em cada instancia EC2 do cluster ECS;
        * Informações na comunicação entre instancias ECS, incluem:
            * Task rodando
            * Recursos utilizados
        * Também é responsavel por iniciar/parar tasks (falando para o ECS);

### <span style="color: #ff5733 ">IAM Roles for ECS Tasks</span>

* Usar IAM Roles com ECS Tasks, garante isolamento de credenciais, sem necessitar armazenar as credenciais dentro do container
