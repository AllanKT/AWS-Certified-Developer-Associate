# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span> 

## <span style="color:#884ea0 ">**AWS VPC Networking**</span> 
## <span style="color:#FFC300 ">Amazon Virtual Private Cloud (VPC) Fundamentals</span>
---
### <span style="color: #ff5733 ">VPC Essentials</span>

* **Virtual Private Cloud (VPC)**:
    * Permite utilizar recursos AWS dentro de uma rede virtual definida, que se assemelha a uma rede tradicional, operada por datacenters, mas com o beneficio de ser escalavel com a infra da AWS;
    * assemelha-se a *Datacenters on-primese privados* e *redes corporativas privadas*;
    * Caracteristicas:
        * sub-redes publicas e privadas
        * arquitetura escalonavel
        * capacidade de extender a rede corporativa/on-premise para rede em nuvem (VPN);
    *Fatos importantes:
        * VPC fica dentro de uma região escolhida
        * VPC abrange varias AZs da região, permitindo provisionar recursos redundantes em AZs separadas enquanto elas são acessadas pela mesma network (Alta disponibilidade e Tolerancia a falhas);
        * Servidor DNS para a VPC para cada instancia, permitindo ter um caching das opções de DHCP configuradas na VPC;

    * **Beneficios**:
        * capacidade de iniciar instancias em uma subnet;
        * difinição de CIDR (IP range) custoizado dentro de cada subnet;
        * configurar rotas entre subnets com o *route tables*;
        * configurar um internet gatway para fornecer rotas para a internet para recursos dentro da VPC;
        * criar camadas de rede dos recursos;
        * expandir redes on-premise para a nuvem com VPN/VPG e tuneis de IPsec VPN;
        * Camadas de segurança:
            * Security Groups (firewall em nivel de instancia)
            * ACLs (firewall em nivel de subnets)
    
    * **Default VPC**:
        * Pro padrão um VPC ja vem pre configurado na conta AWS, quando é criada;
        * a VPC default tem uma pre configuração diferente das non-default;
        * a VPC default permitir ao usuário acesso fácil a um vpc sem precisar configurá-lo do zero;
        * nesta, todas as subnets tem uma rota para a internet com o *route table* conectado ao IGW;
        * cada instancia desta VPC tem IPs publicos e privados, definidos nas configuracoes da subnet;

    * **Limites**:
        * 5 VPCs por região (disponibilizam mais se requisitar)
        * 5 internet gateway por regiao
        * 50 client gateways por regiao
        * 50 VPN conectadas por gerião
        * 200 *route tables* por regiao / 50 entradas por *route table*
        * 5 elastic IP address
        * 500 security groups por VPC
        * 50 regras de security group
        * 5 ecurity groups por interface de rede

### <span style="color: #ff5733 ">VPC Networking Basics</span>

* **Internet Gateway (IGW)**:
    * Componente da VPC que permite comunicação das instancias dentro da VPC com a internet;
    * é escalado horizontalmente, redundante e com alta disponibilidade (não tem risco de indisponibilidade e restrições na largura de banda durante o tráfego);
    * transição NAT para instancias com IP publico;

    * **Regras e Detalhes**:
        * Apenas 1 IGW conectado a VPC por vez;
        * Não pode conectar um IGW em uma VPC que tenha recursos ativos
        * deve ser conectado a VPC se os recursos dentro dela, precisam ser conectados à recursos da internet

* **Route Table**:
    * Pro padrão uma route table default (main) ja vem pre configurado na VPC default;
    * contem um conjunto de regras (**routes**), usadas para trafegar os dados;
    * Dois componentes:
        * *destination*: CIDR (bloco de ranges de IPs)
        * *target*: nome para onde os dados estão sendo roteados
    * por padrão, o trafego é permitido para cada outra subnet disponivel na VPC que é chamada de local route
    * a local route não pode ser modificada
    * pode-se ter várias reoute tables na VPC
    * uma route table não pode ser deletada se tem dependencias

    * **Best practice**: deixar a route table padrão e criar uma nova route table quando novas rotas forem necessárias para uma subnet específica

* **Subnets**:
    * Pro padrão uma subnet é associada a route table default (main) da VPC default;
    * uma VPC abrange todas as AZs da região, podendo ser adicionados uma ou mais subnets para cada AZ. Cada subnet deve residir apenas em uma AZ, sem abrangir zonas.

    * deve estar associada a uma route table;
    * uma subnete publica **TEM** rotas para a internet
    * uma subnete privada **NÃO TEM** rotas para a internet 

    * instancias de uma subnet privada não podem se comunicar com a internet, sendo um alto nivel de segurança, mas cria uma limitação pois a instancia não pode fazer downloads, atualizações de software, etc (solucionado com roteamento através do NAT);
    * trafego das subnetes é permitido para cada subnet disponivel, com a route table *local*;
    * uma subnet existe apenas em uma AZ

### <span style="color: #ff5733 ">VPC Security Basics</span>

* **Network Access Control List (ACLs)**:
    * Pro padrão uma VPC defaut já tem uma NACL associado com as subnets default;
    * ACLs operam no nivel de rede/subnet
    * permite/nega trafego dentro ou fora da subnet
    * **stateless**: o trafego de retorno deve ser permitido através do *outbound rule*
    * processo de regras em ordem numerica, para decidir se o trafego é permitido, avaliadas em ordem crescente
        * *se o tráfego for negado em um número de regra mais baixo e permitido em um número de regra mais alto, a regra de permissão será ignorada e o tráfego será negado*
    * a ultima regra do ACL nega as outras regras, a menos q o protocolo/porta esta explicito para permissão
    * Network access control list (NACLs) é uma camada adicional de segurança na VPC, como um firewall que controla o trafego dentro e fora de uma ou mais subnets
    * **Best Practices**: incrementar o numero de regras em 10, pois, se precisar colocar uma regra em uma determinada ordem, isso não criará um problema

* **Secutiry Groups**:
    * Similar aos NACLs, permitindo ou negando o trafego, porem, trabalha na camada de segurança a nivel de instancia
    * As regras trabalham de forma diferente da ALC:
        * apenas regras de permissão
        * **stateful**: a solicitação de retorno de tráfego é permitida, independentemente das regras
        * todas as regras são avaliadas, antes de dar permissão a requisição
    * **Best Practices**: permitir apenas o tráfego necessário

### <span style="color: #ff5733 ">VPC Networking for High Availability and Fault Tolerance</span>

* **Elastic Load Balancer (ELB)**:
    * load balancers são utilizados para distribuir o trafego entre os servidores;
    * O ELB processa de forma automatica essa distribuição de acessos, entre todas as instancias associadas a este ELB, balanceando os acessos, mesmo que entre EC2 de multipas AZs (permitindo alta disponibilidade e tolerancia a falhas);
    * ELB emparelhado com **Auto Scaling** melhora a auta disponibilidade e tolerancia a falhas, e permite a escalabilidade e elasticidade;
    * tem seu proprio DNS permitindo acesso direto com a internet;

    * **Fatos importantes**:
        * Quando usado com uma VPC, o ELB pode atuar como um balanceador de carga interno e balanceador de carga para o EC2 interno na subnet privada;
        * trabalha com um health check, deixando de mandar trafego para uma instancia que possa se ternar prejudicial
        * ajuda a redizir o poder computacional da EC2, habilitando um SSL aplicado diretamente ao ELB;
* **Auto Scaling Group (ASG)**:
    * serviço para automaticamente, adicionar e remover o numero de instancias para aplicação, baseado em metricas do CloudWatch (elasticidade);
    * *Dois compenentes*: 
        * Lauch Configuration: template EC2 usado quando o auto scaling group precisa provisionar instancias adicionais;
        * Auto Scaling Group: regras configuradas se/quando uma EC2 é provisionada ou encerrada automaticamente;
            * Numero min/max de instancias permitidas
            * VPC e AZs para a instancia 
            * Se a instancia provisionada recebera trafico da ELB
            * policies de escalonamento (metricas do cloudwatch como eventos de escalonamento)
            * SNS notificações

    * **OBS**: para uma arquitetura com alta disponibilidade e tolerancia a falhas, é necessario o uso de ELB e ASG com o minimo de 2 instancias separadas em AZs;

### <span style="color: #ff5733 ">VPC Networking with a Bastion Host and NAT Gateway</span>

* **Bastion Host**:
    * conectado em subnets publicas, usado como um gateway para trafego entre determinadas instancias, em subnets privadas (trafego entre subnet publica e privada);
    * considerado *critical strong point* da rede (todo trafego passa por ele primeiro)
    * aumenta a segurança da VPC, como uma 3° camada se segurança e monitoramento de softwares;
    * usado para acesso SSH em rede interna, sem uma VPN

* **NAT Gateway**:
    * Providencia uma EC2 para subnets com uma rota para a internet
    * previne qualquer host fora da VPC de inciar uma conexão com instancias associadas a ele;
    * só receberá tráfego de entrada se uma solicitação for originada de uma instância em uma sub-rede privada;
    * necessário para que instancias de uma subnet privada possam se comunicar com a internet
    * cria alto nivel de segurança, mas limita intancias que não podem fazr downloads e atualizações de softwares;

    * *OBS*: 
        * DEVE ser criado em uam subnet publica
        * DEVE ser parte de uma route table de subnets privadas
    
* **NAT instance**:
    * Identica ao NAT gateway nesse proposito, entretanto, executa diferetnes configurações da EC2 para o mesmo job;
    * torna-se um recurso legado na AWS
