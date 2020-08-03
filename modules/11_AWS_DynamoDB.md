# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Database Services**</span>
## <span style="color:#FFC300 ">DynamoDB</span>

---
### <span style="color: #ff5733 ">DynamoDB Overview</span>

* **DynamoDB Key Features**:
    * NoSQL database:
        * escalavel internamente
        * gerenciamento de dados
        * monitoramento embutido
        * sem esquemas (aramzenamento chave-valor)
    * consistente e rapida performance
        * armazenamento rapido em SSDs
        * controle de rendimento com capacidade read/write
        * replicavel entre multi AZs
        * **DynamoDB Global Tables** permitem replicar em diferentes regioes
    * facil de configurar e comunicar:
        * AWS console ou APIs
        * CLI ou SDKs
        * facil de integrar com serviços AWS
        * **DynamoDB Streams** permite que outros serviços AWS tomem ações baseadas em mudanças de itens
    * criptografia opcional at rest
    * 256 tabelas por região

* **DynamoDB Pricing**:
    * *Core Pricing Components*:
        * mensalmente por escrita (Write Capacity Unit - WCU)
        * mensalmente por leitura (Read Capacity Unit - RCU)
        * Armazenamento indexado (taxa horária por gigabyte de dados da tabela)

    * *Others*:
        * Capacidade de reserva
        * Auto scaling
        * Global tables (Replicate Write Capacity Units - rWCUs)
        * Buckup sob demanda
        * Restauramento sob demanda
        * DynamoDB Accelerator (DAX)
        * DynamoDB Streams

### <span style="color: #ff5733 ">DynamoDB Core Concepts</span>

* **Partition Keys**:
    * determinam a partição fisica onde o item está armazenado
    * Todas as tabelas precisam de uma partition key (has attribute), que contem apenas um tipo de valor
    * Utiliza a partition key em uma hash function para determinar em que partição o dado está armazenado
    * deve ser string, number ou binary

* **Sort Keys**:
    * determinam a ordem que os itens irão aparecer na partição
    * Não são obrigatorias
    * Sort keys (range attribute) deve ser escalar, e contem apenas um tipo de valor
    * depois do dynamo usar o partition key para determinar a partição, sort key, é utilizado para ordenar os dados na partição

* **Pimary Key**:
    * valores unicos para identificar um item
    * **Simple Primary Key**:
        * contem apenas a partition key
    * **Composite Primary Key**:
        * contem a partition key e a sort key

* **DynamoDB Items**:
    * grupos de atributos que compo~em um dado

* **DynamoDB Attributes**:
    * dado basico do DynamoDB, se assimilando a campos e colunas em databases
    * Tipos:
        * Scalar Types (String, Numbers, Binary, Boolean, Null)
        * Document Types (List, Map)
        * Set (Number Sets, String Sets, Binary Sets)

### <span style="color: #ff5733 ">Provisioned Throughput</span>

* **Taxas de tranferencia DynamoDB (Write/Read)**:
    * Valor a ser pago, pelo consumo das tabelas e index
    * quando a taxa é alcançada, requisições de get são "estranguladas"
    * usar auto scaling para evitar estrangulamento, aumentando ou diminuindo a capacidade necessaria peioricamente
    * mensurar a capacidade de leitura e escrita
    * taxa de tranferencia está definido no nível da tabela, mas se divide e é consumido no nivel de partição, então algumas partições podem precisar de capacidades enquanto outras estão bem.

### <span style="color: #ff5733 ">DynamoDB Read Operations</span>

* **DynamoDB Read Operations**:
    * *GetItem*: leitura eficiente de um único item da tabela, a partir de sua primary key
    * *BatchGetItem*: lê até 100 itens, de uma ou mais tabelas, cada leitura com seu RCU
    * *Query*: Lê itens com a mesma partition key (pode usar a sort key, para ordenar os itens). retorna todos os itens tratados com uma RCU unica, onde é compudato o tamanho total dos itens e arredondado para os próximos 4KB.
    * *Scan*: lê todos os itens da tabela, considerando o tamanho dos itens avaliados, não do que será retornado.

    * Podem ser de dois tipos:
        * *Eventual consistency*: não garante a escrita mais recente da tabela
        * *Strong consistency*: garante que a leitura reflita a escrita mais recente

### <span style="color: #ff5733 ">Local and Global Secondary Indexes</span>

* **DynamoDB Secondary Indexes**:
    * Permite realizar queries mais eficientes de atributos não primarios
    * index secundarios são associados a uma tabela, que podem conter varios indexes
    * DynamoDB automaticamente mantem um index secundario, quando a tabela base é atualizada os index tbm são

* **Local Secondary Index (LSIs)**:
    * permite ordenar a tabela com sort key
    * deve ter o mesmo partition key que a tabela original
    * LSI é composto por partition e sort keys
    * Cada LSI age como um sort key, mantendo uma sincronia com os dados
    * RCU/WCU do LSI ocupam a capacidade da propria tabela
    * LSI deve ser criado quando a tabela é criada

* **Global Secondary Index (GSIs)**:
    * cada GSI são formas de realizar queries usando diferentes partition e sort keys
    * como o LSI, o GSI é automaticamente sincronizado com o tabela principal
    * não se pode realizar leituras consistentes com GSI
    * GSI utiliza RCU e WCU independentes da tabela principal
    * podem ser criados depois da tabela ja estar criada

### <span style="color: #ff5733 ">Conditional Writes and Atomic Counters</span>

* **Atomic Counters**:
    * escritas são aplicadas em ordem de recebimento, então para que possam ser usados para incrementar valores existentes, para propositos de regras de negocio, como um contador de visitas no site.
    * Se a operação falhar, o valor é restaurado
    * isso corre o risco de atualizar o item duas vezes e, possivelmente, sub ou superconta

* **Conditional Writes**:
    * usado quando se precisa de um controle sobre as condições de sucesso  de escritas que podem ser usadas como condições de escrita
    * escritas só serão bem-sucedidas se os atributos do item que estão gravando atendem a uma ou mais condições aceitas

### <span style="color: #ff5733 ">DynamoDB Auto Scaling and On-Demand</span>

* Processo do auto scaling:
    * criar uma aplicação auto scaling policy na tabela
    * publica metricas de consumo no CloudWatch
    * se o consumo da tabela excede a utilização planejada por um tempo especifico, o CloudWatch notifica os owners. O alarme pode ser visualizado no console aws e receber notificações com o SNS
    * Os alarmes CloudWatch chamam o auto scaling para avaliar as policies de escalonamento
    * Application Auto Scaling emite uma solicitação de atualização da tabela para ajustar a taxa de transferência provisionada de suas tabelas
    * processos de auto scaling, dinamicamente incrementam/decrementam a taxa de transferencia provisionada nas capacidades das tabelas

### <span style="color: #ff5733 ">DynamoDB DAX</span>

* **DAX - In-Memory Acceleration**:
    * projetado para escalar e ser performatico
    * tempo de resposta muito rapido, contudo, existem certos casos de uso que requerem resposta em microsegundos
    * **DAX** entrega tempos de resposta rápidos para acessar dados eventualmente consistentes, dando beneficios para performance de dados in-memory para aplicações
    * Casos de uso:
        * quando precisa de tempo de leitura muito rapido
        * lê um pequeno numero de itens mais frequentemente que outros
        * leitura intensa, mas são sensiveis ao custo
        * leituras repetitivas contra um grande conjunto de dados

### <span style="color: #ff5733 ">DynamoDB Throttling Issues (Limitações)</span>

* itens são armazenados em partições, de acordo com o partition key
* cada partição compartilha o RCU e WCU da tabela
* requisições analizam as partições dos dados e a capacidade da partições determina se a requisição é bem sucedida ou rejeitada (estrangulada)
* erros de estrangulamento devem ser esperados e tratados pela aplicação
    * receber muitas requisições
    * limitações de capacidade: a tabela não tem um valor ideal de RCU e WCU
* o que acontece quando ha muito estrangulamento:
    * perda de dados, e não ha retentativas de escrita
    * processamento lento se as retentativas são excessivas
    * dados podem se tornar desatualizados, se a escrita é estrangulada e a leitura não

* **TTL (Time To Live)**: Define um tempo de expiração dos dados na tabela.

### <span style="color: #ff5733 ">DynamoDB Streams with Lambda</span>

* captura sequencias de itens modificados em uma tabela e armazena essa informação em um log por até 24 horas
* aplicações podem acessar esse log e visuzaliar os itens antes e depois da modificação, quase em tempo real
* habilitar o stream, o DynamoDB captura informações sobre toda informação de modificação nos dados
* realtime que permite aplicações consumirem o stream e tomar ações baseadas em seus conteudos
* AWS mantém endpoints separados do DynamoDB e do DynamoDB Stream
