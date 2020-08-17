# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Application Services**</span>
## <span style="color:#FFC300 ">Amazon Simple Queue Service (SQS)</span>

---
### <span style="color: #ff5733 ">SQS Essentials</span>

* **SQS Essentials**:
    * filas com alta disponibilidade usadas para enviar e receber mensagens entre producers e consumers
    * criação de componentes de aplicações destribuida/desacoplada
    * mensagens entre servidores são recuperadas atravez do **polling**
        * *Long Polling* (1-20 sec):
            * ocorre apenas quando a fila ou mensagem possui um *WaitTimeSeconds*
            * espera ate que uma mensagem esteja disponivel na fila antes de enviar a resposta
            * long polling reduz requisições as apis
            * mais barato por precisar de menos requisições
        * *Short Polling* (0 sec):
            * metodo padrão
            * ocorre quando o *WaitTimeSeconds* é 0 ou a fila tem especificado na mensagem o *ReceiveMessage API*
            * exibe uma subnet de servers e retorna uma mensagem para estes
            * não envia todas as possiveis mensagens na fila
            * Aumenta requisições as apis, o que aumenta o custo

* *Important Facts*:
    * dois tipos de filas:
        * **Standard Queues**:
            * suporta grande quantidade de mensagens por segundo
            * suporta multiplos producers e consumers
            * garante entrega das mensagens ordenadas, pelo menos uma vez
        * **First-in-first-out (FIFO) Queue**:
            * até 3000 mensagens por segundo em batch
            * até 300 mensagens por segundo sem batch
            * suporta multiplos producers e consumers (estes por Group IDs):
                * Group ID pode para ordenar as mensagens na FIFO
                * mensagens processadas em ordem
            * FIFO garante que as mensagens são enviadas e processadas em ordem
    * Alta disponibilidade e redundancia
    * PCI Compliant e pode encriptar mensagens usando KMS

* **SQS Producers**: qualquer aplicação que pode gerar uma mensagem SQS e enviar para a fila
* **SQS Consumers**: qualquer aplicação que processe a mensagem SQS. Também são responsaveis por deletar mensagens das filas
* **SQS Queue**: host com alta disponibilidadde de armazenamento de mandagens
* **SQS Message**: informação de texto criada e enviada ao SQS que pode ser XML, JSON ou PlainText

* **Queue Settings**:
    * *Dead Letter Queues*: lidar com dados mal formatados
    * *Delay Seconds*: tempo para mensagem ser adicionada a fila, apos a criação
    * *Visibility Timeout*: Tempo para mensagens são invisiveis, apos recebido por um consumidor

### <span style="color: #ff5733 ">Managing Access to SQS Resources</span>

* **SQS Resource Bases Access Control Policies**
    * garante acesso a filas sqs de outra conta AWS
    * SQS AddPermission API gera automaticamente a policy para o SQS
    * Garante acesso para algumas contas e serviços AWS para a fila
    * Pode usar IAM Policies e Access Control policies ao mesmo tempo

### <span style="color: #ff5733 ">SQS API Actions and Errors</span>

* **SQS API Actions**:
    * CreateQueue
    * GetQueueUrl
    * SendMessage (utilizado pelos consumers para enviar as mensagens)
    * ReceiveMessage (utilizado pelos consumers para ler as mensagens)
    * ChangeMessageVisibility (alterar a visibilidade da mensagem na fila)
    * DeleteMessage

<span style="color: #2980b9 ">**QUIZ: AWS SNS Essentials for Developers**</span>

**1**: Which of the following is true if long polling is enabled?

* The reader will listen to the queue until a message is available or until timeout (Long polling waits for messages to come into the queue until there are messages or the ReceiveMessageWaitTimeSeconds attribute limit is reached.)

* <span style="color:  #c0392b  ">If long polling is enabled, then each poll only polls a subset of SQS servers; in order for all messages to be received, polling must continuously occur (Sorry! Long polling actually checks all servers and will wait for any message that comes in within the period defined by the API request.)</span>

**2**: Which of the following statements about SQS standard queues are true?

* Message order can be indeterminate - you're not guaranteed to get messages in the same order they were sent in 
* Messages can be delivered one or more times

**3**: Company B is using Amazon SQS to decouple their systems for scaleability. However, they need to send messages up to 400KB in size. What might Company B do in order to send more than 256KB of data?

* Store the data in S3 or DynamoDB and attach message instructions to the message for the worker to retrieve the data

**4**: Company B provides an online image recognition service and utilizes SQS to decouple system components for scalability. The SQS consumers poll the imaging queue as often as possible to keep end-to-end throughput as high as possible. However, Company B is realizing that polling in tight loops is burning CPU cycles and increasing costs with empty responses. How can Company B reduce the number empty responses?

* Set the imaging queue ReceiveMessageWaitTimeSeconds Attribute to 20 seconds (Enabling long polling reduces the amount of false and empty responses from SQS service. It also reduces the number of calls that need to be made to a queue by staying connected to the queue until all messages have been received or until timeout. In order to enable long polling the ReceiveMessageWaitTimeSeconds attribute needs to be set to a number greater than 0. If it is set to 0 then short polling is enabled.)

* <span style="color:  #c0392b  ">Set the imaging queue VisibilityTimeout attribute to 20 seconds (Sorry! This will really only impact messages after they're already picked up by consumers of the queue. It doesn't really apply here. Setting a higher VisibilityTimeout will actually make messages not appear in the queue for a time.)</span>

---

# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**MODULE**</span>
## <span style="color:#FFC300 ">MODULE</span>
### <span style="color: #ff5733 ">CLASS</span>
<span style="color: #2980b9 ">**QUIZ**</span>
* <span style="color:  #c0392b ">ERROR</span>