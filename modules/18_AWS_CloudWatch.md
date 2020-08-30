# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Application Services**</span>
## <span style="color:#FFC300 ">CloudWatch</span>

---
### <span style="color: #ff5733 ">CloudWatch Essentials</span>

* usado para monitorar serviços AWS (EC2, ELB, S3, etc)
* monitora o ambiente com configurações e visualiza metricas especificas por cada serviço

* *Detailed vs Basic Level Monitoring*:
    * *Basic*: dado disponibilizado automatiamente a cada 5 minutos
    * *Detailed*: dado disponibilizado a cada 1 minuto

* Alarmes podem criar gatilhos ou outra ação na conta AWS, como SNS, baseado nas metricas obtidas
* Auto Scaling utiliza cloudwatch passando limites e alarmes para triggers que adicionam ou removem instancias do auto scaling group
