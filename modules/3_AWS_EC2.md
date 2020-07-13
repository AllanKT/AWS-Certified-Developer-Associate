# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span> 

## <span style="color:#884ea0 ">**Server Based Compute Services**</span> 
## <span style="color:#FFC300 ">Elastic Compute Cloud</span> 
---
### <span style="color: #ff5733 ">EC2 Fundamentals</span> 

* EC2 (Elastic Cloud Compute)
* **EC2 Essentials**:
    * providencia servidores virtuais escalaveis (instancias) na nuvem com diferentes tamanhos e tipos, rodando sob diferentes SO, mas comumente Linux e Windows;
* possuem design para imitar servers on-premises, sendo pago sob demanda com facil escalabilidade e elasticidade;
* *Componentes*:
    * Amazon Machine Image (AMI): O sistema Operacional;
    * Instance Types: O poder computacional do hardware, RAM, largura de banda da rede, etc;
    * Network Interface: publico, privado ou endereços de IPs elasticos;
    * Storage: instancias de "hard drive":
        * Elastic Block Store (EBS): armazenamento persistente de rede;
        * Elastic File System (EFS): armazenamento de arquivos elastico e escalavel;
        * Instance Store: armazenamento efêmero, temporario;
* Um *ecutiry group* deve ser relacionado a instancia durante a criação;
* cada instancia deve ser colocada em uma VPC, availability zone e subnet;
* comandos de inicialização personalidados podem ser passados para a instancia via *user-data* script;
* *Tags* devem ser usadas para ajudar a organizar as instancias;
* criptografia key-pairs é usada para gerenciar a autenticação por login;
* existem limites para a quantidade de instâncias que você pode executar em uma região a qualquer momento específico (mantenha em mente caso sua aplicação precise de uma capacidade computacional signifcante)

* **Amazon Machine Images (IAMs)**:
    * pacote de pré configuração:
        * Sistema Operacional
        * Software Packages
        * Outros (tipo de armazenamento root & tipo de virtualização)
    * usa Auto Scaling para subir e recuperar rapidamente servidores sob demanda;
    * AMIs podem ser criadas e customizadas;

    * tres categorias:
        * Community AMIs:
            * free to use
            * geralmente, apenas seleciona o SO
        * AWS Marketplace AMIs:
            * Pay to use
            * geralmente, vem com adicionais, licença de software
        * My AMIs:
            * AMIs que foram criadas por você

* **EC2 Instance Types**:
    * Componentes de hardware utilizados:
        * Poder computacional (processador/vCPU);
        * Memoria (RAM);
        * Opções de armazenamento (hard drive);
        * Performance de rede (largura de banda);
    * Agrupadas em familias e tipos (april 2018):
        * Propositos Gerais (T2, M5, M4):
            * T2: desempenho exploravel, bom para muitos propositos gerais;
            * M4/M5: pequeno ou medio porte;
        * Computador Otimizados (C4 C5):
            * Alta performance de web servers, engenheiros e cientistas;
        * Memoria Otimizada (X1e, X1, R4):
            * Alta performance de databases, in-memory, processamento de dados;
        * Accelerated Computing (P3, P2, G3, F1):
            * P2/P3: Maquinas de deeplearning, alta performance de dados, GPU;
            * G3: visualização e renderização 3D, aplicação de streaming, videos, server graphics;
            * F1: pesquisa genômica, analise financeira, big data e segurança;
        * Armazenamento orimizado (H1, I3, D2):
            * D2/H1: MapReduce, HDFS, file system, processamento de dados de aplicações;
            * I3: NoSQL (Cassandra/Mongo/Redis), data warehouse, ElasticSearch;

### <span style="color: #ff5733 ">EC2 Purchasing Options</span>

* **EC2 Opções de compra**:
    * **ON-DEMAND**:
        * escolha de qualquer tipo de instancia, provisionamento/encerramento a qualquer momento;
        * Opção mais cara;
        * Opção mais flexivel;
        * cobrado quando a instancia está rodando (cobrado por segundo);
    * **RESERVED INSTANCE (RI)**:
        * Comprar a instancia por um periodo (1-3 anos);
        * mais barato que a on-demand;
        * pode pagar adiantado, adiantado parcial ou sem adiantamento;
        * Comprar em uma AZ especifica, providencia capacidade reservada nesta AZ;
    * **SPOT INSTANCES**:
        * Lances por instancias, pagando pelas instancias com o valor menor ou igual ao do lance;
        * venda de instancias não utilizadas, por um curto periodo de tempo, com um disconto substancial;
        * Preços das instancias variam
        * Cobrado por segundo;
        * O uso da instancia termina quando o preço fica maior que o do lance;
    * **DEDICATED HOSTS**:
        * Maquina fisica dedicada com acesso total;

### <span style="color: #ff5733 ">EC2 Instance Configuration </span>

* **EC2 IP addresses**:
    * Private IP Address:
        * todas são iniciadas automaticamente com PRIVATE IP;
        * Usado por comunicação interna entre instancias (por VPC);
    * Public IP Address:
        * Ao criar uma instancia, pode habilitar ip publico (ou por atribuição automatica);
        * Usado para comunicar a instancia com recursos por rede aberta;
        * A atribuição automática baseia-se na configuração da sub-rede selecionada na qual você está provisionando a instância
    * Elastic ID Address (EIP):
        * IPV4 estatico e publico, feito para computação em nuvem;
        * usar um ip publico em uma EC2, se foi criada apenas com ip privado
        * mascarar falhas de uma instancia, fazendo um remapeamento dos endereços da instancia
        * usar EIP trocará por ips publicos enquanto estiver sendo usado;
* **Bootstrapping & User-Data/Meta-Data**:
    * Bootstrapping:
        * "auto-partida" com um comando sem necessidade de um input externo;
        * comandos customizados (installação de softwares, etc)
    * User-Data:
        * na criação da EC2, pode-se incluir comandos customizados via script (bash script);
        * Exibido durante a criação da instancia nos logs;

### <span style="color: #ff5733 ">EC2 Storage Basics</span>

* **EC2 Elastic Block Store (EBS) Basics**:
    * são persistentes, durante a vida da EC2;
    * pode conectar/desconectar de varias instancias EC2;
    * Pode ser conectado a APENAS UMA instancia por vez;
    * pode fazer backup em um snapshot, e reestruturar em um novo EBS;
    * por padrão, EBSs são replicados em um AZ
    * por default, são feitos para o file system */dev/sda1* ou */dev/xvda*

* **EBS Performance**:
    * Medem operações de IOPS (I/O):
        * I/O por segundo
        * AWS mede IOPS em pedaços de 256KB ou menos (512KB, medido em 2 IOPS)
    * O tipo de EBS influencia na performance de IOPS
* Initializing:
    * volumes criados de um EBS snapshot devem ser inicializados;
    * Ocorre na primeira vez que o bloco armazenado pe lido - a performance pode ser imactada em 50%
    * Evitar isso em produção, lendo manualmente todos os blocos;

* **EBS Types**:
    * Proposito geral SSD:
        * Usado para ambeintes de dev/test e pequenos bancos;
    * Provisionamento IOPS SSD:
        * Usado para aplicações criticas;
        * Grandes bancos com carga de tabalho;
    * Taxa de tranferencia Otimizada HDD e Cold HDD (Throughput):
        * Mais barato e com menor desempenho
        * acesso menos frequente
    * EBS Magnetico:
        * Baixo custo para armazenamento
        * Usado para cargas de trabalho onde a performance é importante;

* **EC2 Store Volumes**:
    * dispositivos virtuais, cujo hardware é fisico e conectado ao host do computador que roda a instancia
    * São dados efemeros (temporarios - durante o ciclo de vida da instancia)
    * instancia é "stopped" ou "shutdown" o dado é apagado
    * nem todos os tipos de instancias podem usar

* **SnapShots**:
    * "ponto no tempo" do backup do EBS salvo no S3;

    * *Propriedades*:
        * incrementados naturalmente;
        * um snapshot armazena mudanças, desdo o ultimo snapshot
        * se o snapshot original é deletado, as outros também serão
        * Podem ser usados para restaurar um volume EBS
    
    * frequentemente snapshots dos dados aumentam sua durabilidade (RECOMENDADO);
    * Snapshots diminuem a performance do EBS, então deve ser realizado apenas deve ocorrer durante as horas de não-produção ou de fora do horario de pico;

* **Elastic File System (EFS)**:
    * Opção de aramzenamento para EC2, permite armazenamento escalavel;
    * elastico, ou seja, a capacidade aumenta e diminui com adição ou remoção de arquivos;
    * totalmente gerenciado
    * *Beneficios*:
        * Pode ser acessado por mais de uma EC2 simultaneamente;
        * escala pentabytes de dados, enquanto mantem baixa latencia e alta taxa de tranferencia;
        * pago pelo tamanho do armazenamento utilizado;

### <span style="color: #ff5733 ">EC2 Key Pairs</span>

* **EC2 Key Pairs**:
    * Duas chaves criptografadas, utilizadas pela AWS para autenticar um cliente;
    * Consiste de uma chave publica e uma privada
    * a AWS aemazena a publica na instancia, e o usuário é responsavel pela privada

        * Linux: Não tem senha e loga com SSH
        * Windows: par de chaves para senha de adm, e loga usando RDP

### <span style="color: #ff5733 ">Elastic Load Balancers and Session State</span>

* **Elastic Load Balancer (ELB)**:
    * Utilizado para distribuir trafico entre os servidores
    * serviço automatizado de processos distribuindo o trafico de eventos para todas as instancias associadas as ELB, mesmo que localizadas em multiplas AZs;
    *  *Estado de sessão*:
        * ELB Option 1: Load Balancer Generated Cookie Stickiness:
            * gera cookie se o usuário não tem
            * envia ao usuário uma instancia baseada no cookie
        * ELB Option 2: Application Generated Cookie Stickiness:
            * ELB usa uma aplicação para gerar o cookie, e associar a sessão a instancia
            * envia ao usuário uma instancia baseada no cookie
        * Non-ELB Option (RECOMENDADO): Usa um caching, como o Amazon ElasticCache:
            * Requisições são eventos distribuidos entre as instancias
            * Instancia checa o cache para a sessão
            * Se existe, a instancia pode checar os dados

### <span style="color: #ff5733 ">EC2 API Actions/Errors and the AWS Shared Responsibility Model</span>

* **Shared Responsability Model**:
    * **Cliente** é responsavel por gerenciar o nivel de segurança do softeare e instancias, incluindo:
        * Secutiry Groups
        * Firewalls
        * criptografia EBS
            * utilizando Kay Management Service (KMS)
            * criptografia de arquivos usando encypted file system
        * Aplicar SSL no ELB
    * **AWS** é responsavel por gerenciar o Hypervisor e camadas fisicas de segurança do EC2:
        * Proteção contra DDOS
        * Proteção de portas
        * filtragem de rede de entrada

<span style="color: #2980b9 ">**QUIZ**</span>

**1**: a
    * a


* <span style="color:  #c0392b ">ERROR</span>