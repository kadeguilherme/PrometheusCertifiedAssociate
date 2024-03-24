# 1  Observability Concepts


# 1.1  Metrics, Tracing e Logging
A observability está definida em 3 pilares fundamentais: **Metrics, Tracing e Logging.**

Metrics:
--
São representacão numeréricas do estado do sistema ao longo do tempo. Metricas são fundamentais não somente para entender o comportamento do sistema, mas habilitam outra funcão bastante importante, os alertas.

Definir quais métricas monitorar sempre foi um desafio, de fato, uma grande de coisas monitoradas nunca são utilizadas. Atualmente os métodos mais aceitos para métricas sao o USE  (Utilization, Saturation e Error) e o RED (Request Rate, Error Rate e Duration of request).

Tracing
--
Tracing é a capacidade de rastrear o caminho completo da execucão de uma requisicão ou transacão através do sistema. Em sistema distribuídos, conseguir entender o fluxo das requisicões, quais servićos foram acionados e quanto tempo foi gasto em da um deles, é fundamental para definir **onde** está o problema.

Algumas iniciativas se propõem a resolver esse problema através da padronização de APIs e frameworks para instrumentação de código para observability, como é o caso do projeto Opentracing, ou ainda através da utilização de ferramentas que permitam que os times de Dev e Ops possam ter acesso fácil a essas informações, como é o exemplo do projeto opensource Zipkin, originado no Twitter e baseado no paper Dapper do Google, ou ainda do Jaeger, que tem o mesmo propósito, é suportado pela Cloud Native Computing Foundation e foi desenhado para ser executado sob um orquestrador de containers (ex: Kubernetes).


Logging
---
Capturar e armazenar logs é sem dúvida a prática mais comumente utilizada como ferramenta para identificação e resolução de incidentes. Logs são, independente do formato (ex: Texto, JSON, Binário), um objeto composto por um timestamp associado à dados que descrevem um evento de qualquer natureza. Logs como único instrumento para determinar a causa de um incidente é bastante efetivo se o problema em questão estiver limitado a um único processo ou poucos elementos interconectados. Como já descrevemos anteriormente, em sistemas distribuídos complexos, as muitas interdependências tornam difícil ou até impossível identificar o fato causador do incidente apenas analisando logs de forma isolada.

Outro aspecto importante a ser considerado ao habilitar a captura de logs é que processa-los e armazena-los é bastante custoso e requer um planejamento adequado. A maioria das linguagens e frameworks de programação oferecem bibliotecas padrão para geração de logs, porém nem todas são eficientes e muitas delas podem consumir muitos recursos ou ainda impactar negativamente o desempenho dos próprios sistemas, como pode ser o caso de uma classe de logs que, por exemplo, grave logs em arquivos texto de forma serial e sob um alto volume de acesso ou com o nível de verbosidade inadequado, possa acabar causando algum tipo de enfileiramento e consequente exaustão do thread pool do application server.

Também é importante observar que a maioria dos logs, exceto para os registros necessário para efeitos legais e regulatórios, se tornam desnecessários após alguns poucos dias, é importante criar as condições de armazenar uma amostra representativa dos eventos por um período limitado de tempo e também criar as condições para tratar os logs como um fluxo contínuo de eventos e, quando necessário (durante um incidente por exemplo) manipula-los e extrair as informações necessárias para entender o PORQUE dos incidentes. Existe uma quantidade razoável de ferramentas que permitem tratar logs como event streams e aplicar transformações estatísticas sobre esse fluxo de dados antes de agrega-los e armazena-los.
##
# 1.2  Understand events
Os dois tipos são usados para diferentes propositos, O log tem o proposito de troubleshootin e analizar a causa raiz do probema, enuanto o events é usado para dar insights da aplicacão.
Existem pesquisadores que a observabilidade é composta por 4 pilares: **Logs, Metrics, Traces e Events (MELT)**

Events
---
Telemetria de eventos envolve ações discretas que ocorrem em um momento específico no tempo. Pense nos eventos como um histórico do que aconteceu em seu sistema, o que pode ser útil ao analisar comportamentos de usuário e mais.