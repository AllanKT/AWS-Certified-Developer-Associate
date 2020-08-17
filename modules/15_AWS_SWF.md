# <span style="color:#900C3F">AWS Certified Developer - Associate Level</span>
## <span style="color:#884ea0 ">**AWS Application Services**</span>
## <span style="color:#FFC300 ">Amazon Simple Workflow Service (SWF)</span>

---
### <span style="color: #ff5733 ">SWF Essentials</span>

* **Simple Workflow Essentials (SWF)**
    * permite implementar de forma distribuida, aplicações assincronas com um fluxo de trabalho
    * executa e gerencia a execução de atividades que rodam de forma assincrona entre multiplas maquians
    * tem execução consistente
    * garante ordem nas tarefas executadas
    * não duplica tarefas
    * pode ser usado em on-premise, por ser uma API

* *Componentes*:
    * *Workflows*: sequencia de etapas para uma tarefa especifica (*decider*)
    * *Activities*: unidade de etapa do workflow
    * *Tasks*: interação com *workers* como parte do wrokflow:
        * Activity Tasks: como o worker executa a função
        * Decision Tasks: decidir o estado da execução do workflow e decidir a proxima activity a executar
    * *Workers*: responsavel por receber a tarefa e tomar uma ação (pode ser uma EC2, ou ate uma pessoa)

* *SWF e SQS*:
    * Similar:
        * usados para criar sistemas distribuidos
        * permite que cada componente escale de forma independente
    * Diferenças:
        * SWF pode ter interação humana
        * SWF workflow e tasks permanecem por 1 ano, SQS messagens apenas 14 dias

* *SWF e StepFunction*:
    * Similar:
        * ajuda a criar aplicações coordenadas
    * Diferenças:
        * SWF usa um decider, não um JSON-defined state machine, para tomar decições
        * SWF não tem uma ferramenta de fluxo visual
        * SWF dá o controle completo da logica de orquestração mas adiciona complexidade a aplicação
