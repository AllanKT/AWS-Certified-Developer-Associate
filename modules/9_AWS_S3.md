# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Storage Services**</span>
## <span style="color:#FFC300 ">Amazon S3</span>

### <span style="color: #ff5733 ">Observations</span>: 
---
- Colocando códigos aleatórios como prefixo do diretório do arquivo (força uso de partições diferentes)
- Uso do CloudFront 
---
### <span style="color: #ff5733 ">S3 Essentials</span>

* **S3 Essentials**:
    * Principal serviço de armazenamento da AWS;

    * *Impartant S3 Facts*: 
        * Objetos ficam em regiões AWS e são sincronizados em todas as AZs, provendo alta disponibilidade e durabilidade;
        * sempre deve criar um S3 Bucket em uma região que faça sentido para sua finalidade
            * servir conteudos aos clientes
            * compartilhar dados com EC2

    * *S3 Read Consistency Rules*:
        * Todas as regioes suportam read-after-write com PUTS de novos objetos no S3, ficando imediatamente disponiveis
        * Todas as regioes consistem de PUTS que sobreescrevem objetos existentes e DELETES de objetos

    * Erros são geralemente respostas HTTP;

* **S3 Buckets**:
    * Buckets são os principais constainers de armazenamento do S3, contendo um grupo de informações e tem um subnome similar ao folder;

    * Tags podem ser utilizadas para organizar os buckets

    * Ao criar um bucket, podemos escolher uma região para este, ajudando a diminuir a latencia, minimizar o custo e atender aos requisitos regulamentares;

    * S3 Objects ficam em uma região, a menos que sejam transferidos explicitamente;

    * *Bucket Naming Conventional - All S3 Buckets*:
        * deve ter uma nomeação única em TODA AWS;
        * estar em conformidade com a nomeação DNS convencional
        * no minimo 3 caracteres, e maximo 63
        * apenas letras minusculas, numeros, peiodos e hífens;
        * periodos e hifens não podem ser seguidos um do outro
        * não pode conter formato de IPAddress

    * *Limitaçãos*:
        * Apenas 100 buckets podem ser criados em uma conta AWS
        * Buckets não podem ser transferidos, uma vez criados
        * pode conter um numero ilimitado de objetos

* **S3 Objects**:
    * Arquivos estáticos e metadados de informações;
        * arquivos uploded pelos usuarios
        * AWS Metadata aplicados a objetos como tipod e armazenamento, configurações de criptografia, e permissões
    * Cada objeto deve ter um tipo de armazenamento, que determina a disponibilidade, durabilidade e custo
    * por padrão, todos os objetos são privados
    * Objetos podem:
        * 0 bytes - 5 TB
        * ter multiplas versões (se o versionamento está ativo)
        * pode ser disponivel publicamente pela URL
        * trocar ou deletar automaticamente entre diferentes classes de armazenamento (lifecycle policies)
        * criptografado
        * organizado em sub-nomes chamados *folders*

    * *Object Encryption*:
        * SSE (Server Side Encryption):
            * Objetos S3 podem ser criptografados antes de serem salvos em particões nos data centers, e decriptografadosquando é feito seu download;
            * AES-256

        * Ou utilizar chaves de criptografia proprias, considerando que o cliente pode criptografar os arquivos antes de realizar o upload/download

* **S3 Folders**:
    * S3 suporta o conceito de folders
    * usado para agrupar objetos dentro de buckets
    * usa prfeixos key-name nos objetos

* **S3 é uma estrutura plana, não havendo hierarquia como visto tipicamente em arquivos de sistemas.**

* **S3 Event Notification**:
    * configurar automaticameten comucanições entre S3 e outros serviços AWS quando algum evento acontece no bucket
        * **RRSObjectLost** (automatizar a reciação de objetos RRS)
        * **ObjectCreated** (para todas ou especificas chamadas APIs):
            * Put, Post, Copy, *CompleteMultiPartUpload*
    * Podem ser enviados pelos seguintes serviços:
        * SNS
        * Lambda
        * SQS Queue

### <span style="color: #ff5733 ">Moving Data to S3</span>

* **Single Operation Upload**:
    * Operações de upload podem ser realizadas com CLI, SDK ou pelo próprio console AWS;
    * upload podem ser de até 5GB, porém qualquer arquivo acima de 100MB deverá ser feito com multipart upload;

* **Multipart Upload**:
    * permite o upload de um único objeto em um conjunto de partes;
    * o upload das partes é feito concorrentemente
    * permite parar/retomar upload de arquivos
    * se alguma parte falhar, pode ser reenviado esta parte sem afetar as outras
    * depois de todas as partes serem enviadas, o S3 monta o objetos com estas
    * necessário para objetos de 5GB ou maiores, e altamente recomendado para objetos maiores que 100MB
    * pode ser usado para upload de arquivos de até 5TB

* **Storage Gateway**:
    * conecta dispositivos de software locais de data center para armazenamento em nuvem
    
    * *Gateway-Cached Volumes*:
        * criar volumes de armazenamento dispositivos iSCSI em servidores on-primeses;
        * o gateway armazena os dados escrevendo em volumes no S3 e cria caches acessando frequentemente dados dos dispositivos de armazenamento on-primeses;

    * *Gateway-Stored Volumes*:
        * armazena todos os dados localmente em volumes
        * o gateway periodicamente move snapshots do dado como backups incrementais e armazena no S3;

* **Snowball**:
    * solução para transporte de dados em escala de pentabytes
    * transferencia de dados segura fornecida pela AWS
    * move rapidamente grandes volumes de dados para dentro e fora da AWS

* **AWS Import/Export**:
    * coletar dados locais (on-primeses) e enviar fisicamente para a AWS, com dispositivos do lado do cliente
    * permite enviar quaisquer dados para S3, EBS ou Glacier dentro de um dia útil apos o dispositivo fisico chegar na AWS

    * *Beneficios*:
        * politica de backup externo
        * migra rapidamente grandes escalas de dados para a nuvem (até 16TB por job)
        * recuperação de desastres (eventualmente pega o dado no S3 e envia para você)

### <span style="color: #ff5733 ">S3 Performance</span>

* **S3 Performance**:
    * escalar para taxas de solicitação muito altas, no entanto, existem práticas recomendadas para evitar limites de conta e otimizar suas práticas de armazenamento
        * contatar o suporte AWS para prepararem a conta para evitar os limites temporariamente, quando exceder os numeros de requisições no S3;
        * Seguindo boas praticas para armazenamento, para evitar sobrecarga em requisições


    * Intensive mixed requests:
        * Introdução de aleatoriedade:
            * S3 cria e mantém uma key para cada região
            * keys são armazenadas em partições do index, dependendo do key name
            * adicionar um prefixo aleatorio ajuda a espalhar a carga em multiplas particões
            * prefixos aleatorios são facilmente gerados usando um MD5 hash do key name e concatenando os primeiros caracteres
    * Intensive get request:
        * Introdução de aleatoriedade:
            * mesma solução do *mixed request*
        * Usar **CloudFront**:
            * Cloudfront é um CDN (Content Delivery Network)
            * Distribuição de conteudos com baixa latencia e alta taxa de tranferencia
            * Cache de objetos do S3 (reduz o custo das requisições)
            * Pode cachear objetos em locais proximos dos usuários:
                * reduz latencia
                * melhora a tranferencia de dados
            * ajuda a evitar requisições redundantes ao S3

### <span style="color: #ff5733 ">S3 Permissions</span>

* Todos os buckets e objetos são privados por padrão
* Acesso pode ser garantido atraves de *resource based policies* ou por *IAM policy* (Bucket policies | S3 Access Control List - ACLs)

* S3 IAM Policies:
    * IAM Polocies podem ser conectados a Users, Groups e Roles
    * Não são conectados a buckets ou objetos, mas podem especificar algum pelo seu ARN
    * não garante acesso de usuários anonimos

* S3 Resource Based Policies:
    * Bucket Policies:
        * São policies que são conectadas a S3 Buckets 
        * permissões nas policies são aplciadas a todos os objetos do bucket, a menos que tenha sido criado por um usuário externo
        * usado para conceder acesso a IAM users ou outras contas AWS
    * S3 ACLs:
        * usados com buckets e objetos
        * não concedem ou negam permissoes de acesso
        * usados quando precisa gerenciar objetos de seus buckets
        * usados quando precisa gerenciar niveis de permissão de objetos 
        * usados quando precisa permitir que uma conta externa gerencie as politicas dos objetos
        * escritos em XML

### <span style="color: #ff5733 ">Amazon S3 Encryption</span>

* **S3 Ebcryption**:
    * Duas formas de proteger as informações com S3 e criptografia:
        * In-Transit/Client Side Encryption: Usar SSL ou criptografia do lado do cliente ande de enviar ao bucket
            * *Client Side*:
                * Client-Side Master Key (CSMK)
                * Master Key e dados não criptografados não são enviados para AWS
                * criptografar a data key com uma master key da amazon
                * criptografa o dado e armazena no S3
                * Processo inverso para download
            * *Amazon KMS-Managed*:
                * Customer Master Key (CMK)
                * unica chave para cada objeto
                * requisitando o KMS, ele gera uma key (plaintext) usado para criptografar os dados e um ciphertext blob para upload do arquivo
                * no download, é baixado o objeto criptografado e o metadado, o KMS utiliza o plaintext para decriptografar o objeto
        * At Rest: Requisições onde o S3 criptografa os objetos
            * S3-Managed Keys (SSE-S3)
                * S3 criptografa o dado antes de salvar em disco
                * AES-256 (Advanced Encryption Standard)
                * Cada objeto tem sua chave unica, e uma master key, que muda frequentemente
                * adiciona um **x-amz-server-side-encryption** no header
                * policies podem garantir que todos os objetos do lado do servidor obriguem o header, em suas requisições
                * chaves manipuladas pelo S3 ou SDKs
            * *KMS-Managed Keys (SSE-KMS)*:
                * similar ao SSE-S3, mas usa o KMS-Managed Keys para criptografar os dados
                * permite mais controle de permissão
                * melhor auditoria do acesso aos dados
            * *Customer-Provided Keys (SSE-C)*:
                * O cliente gerencia sua propria chave
                * S3 gerencia a criptografia quando escreve ou leem os dados

### <span style="color: #ff5733 ">Object Versioning</span>

* **S3 Versioning**:
    * armazenar e gerenciar todos os objetos old/new/deleted
    * desabilitado por padrão, uma vez ativo não pode mais ser desativado, apenas suspendido (impede que novas versões sejam criadas)
    * todos os objetos com versões, iram manter suas versões antigas
    * definido no bucket level e aplicado a todos os objetos do bucket
    * *lifecycle policies* podem ser aplicadas para especificar versões dos objetos
        * *versioning* e *lifecycle policies* podem estar habilitados ao mesmo tempo no bucket
        * *versioning* pode ser usado com o *lifecycle policies* para criar arquivamentos e soluções de backups
    
    * **Habilitando S3 Versioning**:
        * Objetos que ja existem permanecem inalterados (null version ID)
        * Novos objetos tem um ID de versão unicos gerados pelo S3
        * novas versões são cobradas como novos objetos
        * objetos são recuperados com a key e a versão

    * **Deleting Versioned Objects**:
        * Standard Workflow:
            * exclução feito em objetos, sem especificar a version ID, mas os objetos permanecem no bucket
            * S3 coloca uma flag na latest varsion do objeto
            * error 404 quando tenta baixar
            * pode pegar uma versão especifica do objeto pelo version ID
            * deletar permanentemente uma versão, precisa passar o version ID especifico

    * **Restoring Versioned Object**:
        * Deletar a versão atual, restaura a versão antiga (repetir o processo ate a que se deseja)
        * Copiar versões antigas do mesmo objeto, adicionando novamente com uma nova versão, preservando todas as versões anteriores

### <span style="color: #ff5733 ">Storage Classes and Amazon Glacier</span>

* **OBS**: S3 agora tem o  *Intelligent Tiering Storage Class* que aramzena entre classes automaticamente, entre objetos de dois acessos (FREQUENT ACCESS  e INFREQUENT ACCESS) baseado no acesso a os mesmos;

* **Storage Classes**:
    * Representa a classificação de cada objeto no S3
    * cada clase possui atributos especificos, como custo de armazenamento, disponibilidade, durabilidade e frequencia de acesso

    * **Standard**:
        * projetado para uso geral, para todos os fins de armazenamento
        * opção padrão
        * mais caro
    * **Reduced Redundancy Storage (RRS)**:
        * projetado para objetos não criticos
        * dados reproduziveis, com nivel inferior ao standard
        * mais barato que o standard
    * **Infrequent Access (S3-IA)**:
        * projetado para objetos que não são acessados frequentemente, mas imediatamente disponiveis quando forem acessados
        * mais barato que a standard e RRS
    * **Glacier**:
        * **archival storage**
        * configurado via lifecycle management
        * projetado para arquivos armazenados a longo prazo (não deve ser usado para backup)
        * demora alguns horas para o objeto ser restaurado e recuperado
        * modelo de armazenamento mais barato
        *Variação de preços:
            * *expedited*: 1-5 minutos
            * *standard*: 3-5 horas
            * *bulk*: 5-12 horas

### <span style="color: #ff5733 ">S3 Lifecycle Policies</span>

* regras atribuidas automaticamente que migra objetos entre classes diferentes, ou deleta, baseado no tempo especificado
* desabilitadas por padrão
* automatizar gerenciamento e reduzir custos
* usado com a criação de versões para criar um arquivamento e backup de soluções no S3
    * enviar versões não atuais, para o glacier depois de X dias
    * deleta permanentemente versões de objetos depois de Y dias
    * separa policies entre versões atuais e não atuais

### <span style="color: #ff5733 ">Hosting Static Websites</span>

* S3 possui opções de baixo custo, de armazenamento de websites
* sites staticos, incluindo HTML, CSS e Javascript, alem de imagens e fonts
* Ao criar o site statico,, incluir o index file e o error file:
    * index é o default do dominio
    * erroraparece para status 4XX
* sites são gerados com uma URL unica, variando com o tipo da região
* Route 53 pode ser usado para gerar um dominio próprio

### <span style="color: #ff5733 ">Enabling CORS Configuration</span>

* *Cross Origin Resource Sharing (CORS)*:
    * CORS é um metodo que impede que requisições sejam feitas de dominios desconhecidos
    * para AWS, um website hospedado no S3 so pode ser acessado por outro bucket S3
    * Configurações de CORS podem ser feitas dentro do S3 em cada bucket
