# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Application Services**</span>
## <span style="color:#FFC300 ">Amazon Simple Notification Service (SNS)</span>

---
### <span style="color: #ff5733 ">Introduction to SNS</span>

* **SNS**: Simple Notification Services
* Aplicação de mensageria para envio de informações de alertas e criação de desacoplamento de ambientes, para gerenciar de tarefas do fluxo de trabalho.
* serviço pub-sub de mensagens e notificações mobile
* SNS coordena e gerencia o envio e recebimento de mensagens para um endpoint especifico
* integrado com muitos serviços AWS, para notificação sobre o que acontece na conta aws
* Com **CloudWatch** e **SNS** uma solução de monitoramento pode ser criada para notificar os administradores com alertas, capacidades de maquinas, tempo de inatividade, mudanças nos ambientes, etc;
* pode ser utilizado para publicar notificações em aplicativos e criar automações basseadas em notificações;

* *Components*:
    * Topic:
        * grupo de *subscriptions* para envio de mensagens
        * nome unico de ate 256 caracteres
        * armazenado de forma redundante em vários servidores e data centers
    * Subscription:
        * endpoint para envio de mensagens (HTTP/s, email, json, sqs, lambda, etc)
    * Publisher:
        * o gatilho "entity" que envia a mensagem (AWS CLI, SDKs, S3 events, cloudwatch, lambda, etc)

* *SNS Benefits*:
    * Escalavel e alta confiabilidade
    * usado pelo console, apis, cli e sdk

### <span style="color: #ff5733 ">Managing Access to SNS Resources</span>

* **SNS Access Control Policies**:
    * Garante acesso para topicos SNS de outras contas AWS (Amazon SNS API - AddPermission):
        * Topic, AWS Account IDs, Actions, Label
    * Garante acesso para algumas contas e serviços AWS para publicar os topicos
    * Pode usar IAM Policies e Access Control policies ao mesmo tempo

### <span style="color: #ff5733 ">SNS Message Data</span>

* **SNS Messages**:
    * Formato JSON, permite capturem dados e enviem na mensagem
    * POST com HTTPs endpoint com headers especifico com autenticação
    * o conteudo da mensagem depende do *subscriber*

* Message Attrubites
    * utilizado pelo SQS e envio de notificações mobile
    * envia com a mensagem
    * cada atributo da mensagem tem Name, Type e Value

### <span style="color: #ff5733 ">Mobile Apps: Mobile Push with SNS</span>

* **SNS Mobile Push**:
    * Envia notificações para apps mobile, por endpoints que aparecem como mensagens de alerta, badges, e sons de alerta

* **Mobile Push Notification Services**:
    * Diferentes provedores permitem o envio de notificação para diferentes dispositivos
        * Amazon Device Messaging (ADM)
        * Apple Push Notification Service (APNS)
        * Baidu Cloud Push

* Processo:
    * **SNS Publisher** -> **SNS Topic** -> **MPNS Providers** -> **Mobile Device**

* MPNS Process:
    * SNS precisa do *device token* ou *registrations IDs*, dependendo da plataforma, para envio de notificação para os dispositivos

<span style="color: #2980b9 ">**QUIZ: AWS SNS Essentials for Developers**</span>

**1**: You have just set up a push notification service to send a message to an app installed on a device with the Apple Push Notification Service. It seems to work fine. You now want to send a message to an app installed on devices for multiple platforms, those being the Apple Push Notification Service(APNS) and Google Cloud Messaging for Android (GCM). What do you need to do first for this to be successful?

* Get a set of credentials in order to be able to connect to the push notification service you are trying to setup. (To use Amazon SNS mobile push notifications, you need to establish a connection with a supported push notification service. This connection is established using a set of credentials. For details, see https://docs.aws.amazon.com/sns/latest/dg/mobile-push-send-register.html)

* <span style="color:  #c0392b  ">Request a Token from Mobile Platforms, so that each device has the correct access control policies to access the SNS publisher. (Sorry! To use Amazon SNS mobile push notifications, you need to establish a connection with a supported push notification service. This connection is established using a set of credentials.)</span>

**2**: What is the simplest way to enable an S3 bucket to be able to send messages to your SNS topic?

* Configure S3 to publish an event directly to SNS.

**3**: Which of these is an API action you would use to send messages to an SNS topic?

* Publish

**4**: Which of these options is a good example of an SNS publisher?

* AWS Services (S3 Events, CloudWatch alarms, Lambda Functions)
* An EC2 service that sends messages to SNS using the Publish API action
