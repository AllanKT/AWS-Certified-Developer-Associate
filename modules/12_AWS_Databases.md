# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Database Services**</span>
## <span style="color:#FFC300 ">Other AWS Database Services</span>

---
### <span style="color: #ff5733 ">RDS Essentials</span>

* Gerenciador de bancos relacionais
    * não permite acesso subjacente de operações no sistema
    * conecta aos bancos da mesma forma que se faz no on-premise
    * provisiona/redimensiona a demanda do hardware de forma escalonavel
    * habilitar multi AZ deployment para backup e alta disponibilidade
    * utilizar ReadReplicas para evitar leituras no banco principal

    * *Beneficios*:
        * updates automaticos
        * backup automatico (snapshots)
        * não requer operar um sistema gerenciavel
        * multi AZ
        * recuperação automatica de eventos e falhas

### <span style="color: #ff5733 ">Encrypting RDS Databases</span>

* adicionar apenas no momento de criação do database
* snapshots podem ser criptografados
* read replicas sempre serão criptografadas ou não, dependendo do rds
* migrar o banco criptografado entre regiões, precisa especificar a region no KMS
* criptografar rds e snapshots habilitando esta opção no RDS DB Instances
* dados criptografados são armazenados no banco são automaticamente feito nos backups, ReadReplicas e Snapshots
* não precisa modificar o banco para usar a criptografia
* gerenciar as keys usadas, deve-se usar o KMS (Key Management Service)
* Usar o KMS, pode criar keys e definir policies control para onde serão utilizadas
* duas camadas de hierarquia usando criptografia envelopada:
    * uma unica key criptografa os dados
    * KMS Master Keys encriptografa a key

### <span style="color: #ff5733 ">What Is Redshift?</span>

* **Data analytics**
* **Redshipt Essentials**:
    * serviço de armazenamento de dados em escala de petabytes (warehousing)
    * totalmente gerenciavel e escalavel
    * geralmente usado por big data analytics
    * pode ser integrado com ferramentas de negocio populares (Jaspersoft, Pentaho, Tableau, Cognos, etc)

### <span style="color: #ff5733 ">Amazon ElastiCache and Caching Strategies</span>

* totalmente gerenciavel
* in-memory cache, usado para melhorar a performance dos databases com cacheamento de resultados e queries realizados
* otimo para grandes, alta performance e altas atribuições de queries - que podem ser armazenados nos caches (**Elastic Cache Cluster**) e acessados posteriormente, em vez de repetir requisições continuas as banco principal
* disponibilidade do ElasticCache inclue *Redis* e *Memcached*
* opções populares como MySQL tem plugins para o Memcached, permitindo integração

* **caching strategies**:
    * Lazy Loading:
        * escreve em cache quando falta o dado no cache
        * evita preencher no cache quando o dado não vai ser requisitado
        * dado em cache pode se tornar obsoleto se implementado sozinho
    * Write Through:
        * armazena em cache sempre que uma escrita, update ou delete é realizado
        * permite que o cache esteja sempre atualizado
        * aumenta o tempo de espera das aplicações
        * sem um TTL pode resultar em um cacheamento de dados que nunca serão lidos
    * Adding Time To Live (TTL):
        * desvantagens do lazy loading e write through podem ser resolvidas com TTL
        * tempo de expiração para as keys
        * quando le um valor de uma key que expirou, a aplicação vai direto no database
        * não garante o dado atualizado se implementado sozinho, mas permite que o dado seja recente e também pode sobreescrever o dado atual
