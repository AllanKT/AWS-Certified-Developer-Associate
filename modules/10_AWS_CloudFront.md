# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Storage Services**</span>
## <span style="color:#FFC300 ">AWS CloudFront</span>

---
### <span style="color: #ff5733 ">CloudFront Essentials</span>

* **CloudFront Essentials**:
    * CloudFront é o Content Delivery Network (CDN) da AWS, que providencia um cacheamento de conteudo nos edge locations e são distribuidos pelo globo.
    * contem um *origin location* (S3 bucket, ELB) e um *edge location*
    * Essa abrodagem reduz latência para acessar os conteudos, e reduz custo computacional que são necessarios para rodar a aplicação.
    * pode ser integrado com Route 53para CNAMEs

    * **beneficios**:
        * reduz a latencia e custo de carregamento
        * reduz a carga e custo da aplicação

    * **updating cached files**:
        * cacheamento feito baseado no nome do objeto
        * novas versões de objetos, cria um novo objeto ou um "invalidation" baseado no nome do objeto
        * "invalidations" tem custo, se acontecer em uma larga distribuição, é melhor criar uma nova distribuição e mover os nomes de DNS
        * objetos são cacheados com uma expiração, ou definidos para não armazenar em cache
    
    * **Signed URLs**:
        * URLs assinado podem acessar conteudos privados e criar temporariamente, one-time-use baseado em segundos que precisa que esteja disponivel
        * assinado com certificado X.509
