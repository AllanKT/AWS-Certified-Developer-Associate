# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS VPC Networking **</span> 
## <span style="color:#FFC300 ">AWS Load Balancing</span> 
---
### <span style="color: #ff5733 ">Application Load Balancers</span>

* Trabanha na camada de aplicação (ALB)/transporte (NLB) do modelo de camadas OSI

* **Classic Load Balancer (CLB)**:
    * Toma decisões de roteamento na camada de transporte (TCP/SSL) ou na camada de aplicação (HTTP/HTTPS);
    * Suportado para EC2-Classic:
        * EC2-Classic é a EC2 original da AWS, onde as instancias rodam um uma rede unica, compartilhada com os clientes. Com o EC2-VPC, instancias rodam em uma VPC isolada logicamente para apenas uma conta AWS;

* **Aplication Load Balancer (ALB)**:
    * ponto unico de controle para o trafego, distribuindo requisições as aplicações via HTTP entre multiplos servers, atraves dos listeners, checando a requisição de clientes, encaminhando para um ou mais grupos baseado nas regras definidas;
    * é especificado um grupo, uma condição e prioridade para cada regra
    * usa um health check configurado, para monitorar a saude da aplicação
    * envia requisições apenas para pelo menos duas instancias saudaveis

    * *Beneficios*:
        * Tomam decisões de roteamento para a camada de aplicação (HTTP/HTTPS)
        * suporta roteamento path-based, configrados em regras para o listener encaminhar as requisições baseadas na URL da requisição;
        * suporta roteamento host-based, configrados em regras para o listener encaminhar as requisições baseadas no host no header do HTTP;
        * suporta roteamento de requisições para multiplas aplicações em uma unica instancia EC2. Pode-se registrar cada instancia ou IP com o mesmo grupo de destino, usando multiplas portas;

### <span style="color: #ff5733 ">Network Load Balancers</span>

* Toma decisões de roteametno na camada de transporte do modelo OSI (TCP/SSL);
* consegue lidar com várias requisições por segundo;
* encaminha as requisições sem modificar o header;
* suporta mapeamento de portas dinamicas;
* consegue lidar com cargas de trabalho volatil e escalar varias requisições por segundo;
* suporte para endereços de IPs estaticos para o load balancer(pode-se também por um IP elastico por subnete ativado para load balancer);

### <span style="color: #ff5733 ">Dynamic Ports</span>

---
# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**MODULE**</span> 
## <span style="color:#FFC300 ">MODULE</span> 
### <span style="color: #ff5733 ">CLASS</span>
<span style="color: #2980b9 ">**QUIZ**</span>
* <span style="color:  #c0392b ">ERROR</span>
