# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span> 

## <span style="color:#884ea0 ">**Identity & Access Management for your AWS Account**</span> 
## <span style="color:#FFC300 ">AWS Identity and Access Management</span> 
---
### <span style="color: #ff5733 ">IAM Essentials</span> 

* **IAM (Identity & Access Management)**: gerencia usuaários, grupos, e regras de acesso;
    * Configuração em nivel global de regiões;
    * Novas contas são criadas sem nenhum acesso aos serviços da AWS (este é um conjunto de regras de negação não explícita em todos os novos usuários do iam);
    * Polices concedem permissão de acesso aos serviços;
* Best Practice para novas contas root:
    * Deletar access keys da root;
    * ativar MFA
    * Criar IAM users admin
    * Gerenciar usuários por grupos de permissão
    * Aplicar policy de password nas IAMs
* Priciple of Least Privilege (Principio do menor privilegio): conceder acesso apenas ao que é necessário para o trabalho;

### <span style="color: #ff5733 ">IAM Policies</span> 

* **Policy**: documento que declara formalmente uma ou mais permissões;
    * por padrão, usuário não tem permissão de nada;
    * modelos de política pré-criados:
        * Admin access: acesso a todos os recursos
        * Power user access: acesso de admin, exceto para gerenciar user/group
        * Read only access: Apenas visualização de recursos;
    * policies podem ser customizadas (policy generator);
    * uma policy pode pertencer a mais de um user/group;
    * policies não gerenciam recursos da aws (ec2, s3, etc);

### <span style="color: #ff5733 ">IAM Users</span>

* **ARN (Amazon Resource Name)**: Utilizado como identificador de diferentes recursos dentro da conta AWS;

```cmd
and:aws:<service>:<region || null>:<account number>:<resource from service>
```

* IAM Users possuem permissão negada para todos os serviços;
* Credenciais não devem ser armazenadas em uma EC2
* usuários que tem grupo e politicas associadas a ele, significa que este possui multiplas IAM policies aplicadas de diferentes fontes;
* politicas de **explicit deny** sobreescrevem politicas de **explicit allow**;

### <span style="color: #ff5733 ">IAM Groups</span>

* Permite atribuir uma mesma *police* para mais de um usuário;
* Facil de gerenciar os acessos dos usuários;

### <span style="color: #ff5733 ">IAM Roles</span>

* Pode ser assumido por qualquer entidade (recursos AWS OU uma conta non-AWS com acesso temporario), adquirindo permissões especificas;
* Utilizado para se conectar diretamente com serviços AWS (polices não podem);
    * *Example*: Instância EC2 acessar um bucket no S3;
        * a instância deve receber uma role do IAM com permissão de read-only do S3, realizando ações baseadas em seu nivel de permissão;
        * Por boas praticas, não se deve armazenar credenciais AWS em instancias EC2 (A role deverá usar);
        * Gerenciamento de roles em EC2 e outros serviços AWS, so podem ser realizados apos a conclusão de sua criação;
        * EC2 so podem ter uma *role* relacionada por vez;
    * *Example*: Uso temporario de roles dos recursos e contas AWS, através de Active Director, serviços sing-on (facebook, google, etc) por uma role "Identity Provider Access";
        * criar *Cross Account* acesso de uma conta utiliza recursos através de outra conta;

### <span style="color: #ff5733 ">Security Token Service</span>

* STS (Security Token Service): Permite criar credenciais temporarias com concessão confiavel aos recursos AWS;
* São credenciais de curto prazo, ativas por alguns minutos ou várias horas;
* Uma vez expiradas, elas não podem mais ser usadas para acessar os recursos AWS;
* Quando um recurso é requisitado utilizando STS, credenciais retornam com 3 componentes:
    * Security Token
    * Access Key ID
    * Secret Key ID

* Beneficios:
    * nenhuma distribuição ou incorporação nas aplicações;
    * concede acesso a aws sem uma conta aws;
    * credenciais temporarias, sem rotação ou revogação;

* Quando usar?
    * identiry Federation:
        * Empresas federadas (acesso atraves da rede da empresa);
            * STS suporta SAML, que é usado pelo Active Director da Microsoft;
        * federação de entidades da web (google, facebook, etc)
    * Roles para acesso cross-account:
        * usuário de uma organização terá mais de uma conta AWS;
    * Roles para amazon EC2 ou outros serviços:
        * concede acesso de uma aplicação rodando em uma EC2, acessar outro serviço sem ter credenciais relacinadas;

### <span style="color: #ff5733 ">IAM API Keys</span>

* Utilizadas para realizar chamadas programaticas aos recursos AWS:
    * CLI, ferramentas Windows Powershell, AWS SDKs, chamadas HTTP

* **!IMPORTANT**:
    * Disponibilizadas apenas uma vez, quando um novo user é criado ou quando é reeditado com novas credenciais;
    * AWS nunca gera o mesmo conjunto de chaves;
    * API keys devem ser associadas a um usuário, para desenvolvimento;
    * no console da AWS, so pode ser visto o access key, nunca o secret key;
    * Um usuário não pode ter duas credenciais ativas simultaneamente (desativar a atual, e gerar uma nova);
    * NUNCA armazena credenciais AWS em uma EC2;

### <span style="color: #ff5733 ">AWS Key Management Service (KMS)</span>

* **NOTE**: KMS está separado do IAM no console da AWS;
* principais recursos da AWS;
* **CMKs (Customer Master Keys)**: usado para encriptar/decriptar até 4KB de dados;
* Gera, encripta e decripta chaves de dados usados fora da AWS;
* dois tipos:
    * *Customer-managed*: cria. habilita/desabilita, rotaciona as politicas de acesso do CMK;
    * *AWS-managed*: criados, gerenciados e usados por serviços AWS integrados com KMS (*aws/service-name*);
* Data Keys:
    * chaves de criptografia para criptografar grandes quantidades de dados ou chaves criptografadas;
    * não gerencia ou armazena as chaves de dados
* Envelope Encyption:
    * Plaintext criptografado com uma *data key*;
    * *data key* criptografado com uma *key encryption key (KEK)*;
    * *KEK* criptografado por outro *KEK*, mas eventualmente este será o *master key*;

### <span style="color: #ff5733 ">AWS Inspector</span>

* **Amazon Inspector**: um serviço automatizado de avaliação de segurança que ajuda a testar o acesso de rede de uma EC2  e estados de segurança de aplicações rodando nesta;
* permite automatizar vulnerabilidades de segurança avaliado todo o desenvolvimento e deploy do sistema;
* permite realizar testes de segurança;

### <span style="color: #ff5733 ">Cognito Essentials</span>

* idP (Identity Providers - Google, Facebook, etc);
* Não está relacionado ao serviços de IAM;
* Utilizado como um conjunto de identificação web (facebook, google) de acesso as aplicações;
* User Poll: 
    * Diretorio de usuários do Cognito;
    * O diretorio de perfis pode ser acessado atráves de um SDK;
* Identity Pool:
    * usuários obtem credenciais AWS temporarias;
    * suporta usuários anonimos e também usuários identificados por alguma serviço;

### <span style="color: #ff5733 ">Identity Federation and Amazon Cognito</span>

* A token gerada pelo cognito, e utilizada como token temporaria para acessar outros recursos da AWS;

<span style="color: #2980b9 ">**QUIZ: AWS Identity and Access Management Concepts for Developers**</span>
 
**1**: You are the lead developer for a healthcare company and are managing an application running on multiple EC2 instances. Those EC2 instances must have the ability to access other AWS resources. What is the best way to manage this access?

 * Use an IAM role to manage temporary credentials for applications that run on an EC2 instance. The role will supply temporary permissions that applications can use when they make calls to other AWS resources.  (Availability Zones have low latency connections between Availability zones in THE SAME region, not other regions.)

**2**: You would like to use STS to allow end users to authenticate from third-party providers such as Facebook, Google, and Amazon. What is this type of authentication called?

* Web Identity Federation

**3**: You have just taken over managing your company's AWS account. As one of your first tasks, you are reviewing IAM groups and their associated permissions. You notice that one of the groups has two conflicting permissions attached: One that allows S3 access and one that denies S3 access. If your goal is to allow members of the group to have S3 access, what needs to be done?

* You must remove the deny policy, as a deny policy will override an allow policy (Correct! If we didn't do this the explicit deny policy (like the one described) would override the allow policy!)

**4**: When requested through an STS API call, credentials are returned with what three components?

* Security Token, Access Key ID, Secret Access Key (Correct! A Security Token, Access Key, and Secret Access Key are required to authenticate API calls with STS provided credentials.)

**5**: Which of the following is required as part of AWS's suggested "best practices" for new accounts?

* Apply an IAM password policy
* Create individual IAM users
* Use user groups to assign permissions

**6**: How should organizations manage permissions across multiple IAM users?

* <span style="color:  #c0392b  ">Users should belong to multiple layers of groups each group granting subsequent additional priviliges and denying others. (Sorry! Because explicit deny policies would prevent users from using resources and taking actions even if they were also given an explicit allow this isn't a very good strategy. Users can be in multiple groups but there isn't nesting as described here.</span>

* Users can be placed into groups and permissions can be applied to the groups themselves. (Correct! IAM Groups provide an easy way to manage permissions at the group level and be applied at the user level.)

**7**: What are the main benefits of IAM groups? (Select two)

* Assigning IAM permission policies to more than one user at a time. 
* Easier user/policy management.

**8**: What best describes the "Principle of Least Privilege"?

* Users should be granted permission to access only the resources they need to do their assigned job.

**9**: Which of these are necessary fields in an IAM Policy?

* Actions
* Resources
* Effects

**10**: What is the access level for newly created regular users in AWS?

* Default deny to all resources and actions (Correct! By default, all new AWS users lack ANY access to AWS resources with a default deny. That default deny doesn't prevent an explicit allow to grant them access. Keep in mind that EXPLICT denys override explicit allows.)

**11**: You work for an application development company that has just hired a senior consultant, named Jessica, who will be working on a large AWS project. You create a new IAM user for her named "Jessica" in your company’s AWS account. On Jessica's first day, you ask her to deploy a Lambda function. Jessica reports back that she does not have access to create a new Lambda function from the AWS Console. But you're unable to review the errors in the AWS console because she is currently working remotely. What is a possible explanation for this?

* You have not added the appropriate IAM permissions and access policies to her user; there is a non-explicit deny to all new users

**12**: API Access Keys are required to make programmatic calls to AWS from which of the following?

* Direct HTTP call using the API
* AWS CLI

**13**: What are some items that are managed in the IAM management section of the AWS Portal?

* Roles
* Multi-Factor Authentication
* Access Keys

**14**: As a best practice, the AWS Root Account should ___.

* take advantage of multi-factor authentication (Correct! The AWS Root Account and other AWS user accounts may do so, but especially the root account should use multi-factor authentication such as a hardware token or a mobile device app like Google Authenticator.)

**15**: What are benefits of using AWS STS?

* Grant access to AWS resources without having to create an IAM identity for them
* Since credentials are temporary, you don't have to rotate or revoke them

**16**: You have hired an engineer, Kathy Johnson, and have created an IAM user for her in the company's AWS account. She will be overseeing the company's DynamoDB tables, so you attached the "AmazonDynamoDBFullAccess" IAM Policy to her IAM user. Six months later, Kathy was promoted to a manager and you added her to the "Managers" IAM group. The "Managers" group has a few explicit allow permissions and no explicit denies attached. But, it does not have the "AmazonDynamoDBFullAccess" policy attached to it. What will happen to Kathy's DynamoDB access?

* Nothing, as an IAM user can have multiple IAM permission policies attached to them at the same time, either directly to the user or through an associated IAM group.
