# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Application Services**</span>
## <span style="color:#FFC300 ">AWS Step Functions</span>

---
### <span style="color: #ff5733 ">Step Function Essentials</span>

* **AWS Step Functions Esentials**:
    * coordenar serviços da aplciação atraves de etapas individuais
    * disponibiliza um workflow visual e ferramentas que ajudam a gerenciar a aplicação
    * frequentemente usado para ajudar a orquestrar e visualizar aplicações serverless

* *Components*:
    * Tasks
    * State Machines:
        * Definida usando JSON Amazon State Language, com Types e States

* *Benefits*:
    * workflow visual
    * aplicações largas por definição de JSON
    * reutilizar e editar facilmente os workflows
    * facilmente integrado com serviços AWS

* **AWS Steo Function - TASKS**:
    * as execuções dos estados definidos são feitos pelas tasks, que podem ser ativadas por lambda functions

    * *An Activity*:
        * codigo que responde usando StepFunction API actions
        * pode hospedar EC2, ECS, e dispositivos mobile
        * Integrar com GetActivityTask, SendTaskSuccess, SSendTaskFailure e SendTaskHeartbeat
    * *A Lambda Function*:
        * serverless function que responde a task

### <span style="color: #ff5733 ">Step Functions - State Types and Transitions</span>

* gerencia as tasks pelo state machine, onde cada state é um estado de decição da maquina baseada no input, execução, ações e output
    * **state**: componentes do state machine, onde cada state tem um nome unico
    * **task**: state que faz alguma trabalho
    * **choice**: states tomam decições entre diferentes remificações
    * **fail|succed**: states param a execução com falhas e sucessos
    * **pass**: state passam o input para o output, podendo adicionar e remover dados nos processos
    * **wait**: state delay onde o processo demora um tempo, ou ate um determinado momento
    * **parallel**: state inicial de execução

* **Basic Transitions**:
    * quando state machine executa, usa o "StartAt" para selecionar por onde começar
    * a proxima etapa é definida pelo "Next"
    * state controle o fluxo permitindo escolher multiplos "Next"
    * transições continuam até:
        * alcançar um state *"Type": Succed*, *"Type": Fail* ou *"End": true*
        * falha na execução
    * tem apenas um start state

* **Input Output**:
    * cada state é um JSON
    * states geram outputs pelo ultimo state ou, para o start state, é passado pela execução
    * state pass podem modificar ou não o input
    * state tem um input recebido, processado e então enviado para o proximo state
