# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Application Services**</span>
## <span style="color:#FFC300 ">Amazon CloudFormation</span>

---
### <span style="color: #ff5733 ">CloudFormation Essentials</span>

* permite utilizar infraestrutura como código
* rápido deploy, controle de versionamento de infra, solução para recuperação de disastres
* Infraestrutura as a Code (IaaC)
* **CloudFormation template** descrever a arquitetura da aplicação em um JSON ou YAML
    * usar o template para criar copias da arquitetura para outras regioes, contas, etc
* **CloudFormation Stacks** coleções de recursos aws que podem ser gerenciados atráves de uma unidade
* **CloudFormation Stacks** são definidos pelo **CloudFormation template**

* **Beneficios**:
    * agiliza a duplicação de arquiteturas em regiões
    * versionar a arquitetura
    * permite rollbacks para versões anteriores
    * permite se preparar para recuperações de desastres

* **Resources**:
    * Format Version
    * Description
    * Metadata (informações adicionais sobre o template)
    * Parameters
    * Mappings (keys para nomeção de valores)
    * Contidions (operadores logicos para definir quando os recursos são criados, pode ser usado para configurar diferentes ambientes)
    * Transform (especifica um ou mais macros para processar no template. integra com *AWS Serverless Application Model* que pode ser transformado em um template de CloudFormation)
    * Resources
    * Outputs (mensagens de texto que serão exibidas ao final dos processamentos)

### <span style="color: #ff5733 ">CloudFormation Resources and Stacks</span>

* **Resources**:
    * recursos são identificados com **Resource type identifiers** (AWS::aws-product-name>>data-type-name) (AWS::EC2::Instance, AWS::DynamoDB::Table, etc)
    * cada recurso no CloudFormation tem sua propria *properties* variando entre si (EC2 tem *AvailabilityZone*, etc)
    * *Resource Attributes* controla o relacionamento dos recursos:
        * CreationPolicy: delay na criação da stack quando se quer confirmar que outra parte está completa
        * DeletionPolicy: opcional, para ficar em torno de certos recursos, como buckets, backups, EBS with snapshots, etc
        * DependsOn: especificar certos recursosque dependem da criação de outros recursos
        * Metadata: adicionar matadados no recurso
        * UpdatePolicy: permite especificar como o CloudFormation deve alterar subnets dos recursos AWS

* **Stacks**:
    * grupo de resources que podem ser gerenciados em conjunto
    * definidos no template do CloudFormation
    * pode criar, alterar e deletar um grupo de recursos de uma stack correspondente
    * exemplo: recursos necessarios para rodar uma aplicação web, como web server, database, e regras de network
    * Stack resources são tratados com uma unica unidade:
        * todos os recursos da stack devem ser criados/deletados com sucesso para a stack ser criada/deletada
        * se um stack resource não pode ser criado, CloudFormation faz um rollback dos resources automaticamente

### <span style="color: #ff5733 ">CloudFormation Functions</span>

* **Intrinsic Functions**:
    * CloudFormation possui varias funções integradas, que ajudam a gerenciar as stacks, podendo ser usadas para atribuir diferentes valores as properties que são disponiveis depois de executadas.
    * usado em Resource properties, Outputs, Metadata attributes, Update policy attributes, e conditionals intrinsic functions para criação de recursos

    * Convincionalmente utilizados:
        * Fn::GetAtt - retorna valores de atributos, usado p nomear ARN
        * Fn::Join - adiciona valores separados por um delimitador
        * Ref - referencia valores setados em parametros ou recursos

---

# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**MODULE**</span>
## <span style="color:#FFC300 ">MODULE</span>
### <span style="color: #ff5733 ">CLASS</span>
<span style="color: #2980b9 ">**QUIZ**</span>
* <span style="color:  #c0392b ">ERROR</span>