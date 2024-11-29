# O que são os Probes no Kubernetes

Kubernetes tem vários tipos de **Probes**:

- Liveness probe
- Readiness probe
- Startup probe

<br>

## Liveness probe

<br>

**liveness probe** determinam quando reiniciar um container. Por exemplo, **liveness probe**  podem detectar um impasse quando um aplicativo está em execução, mas não consegue progredir.

Se um container falhar repetidamente em sua verificação de atividade, o kubelet reinicia o container.

**liveness probe**  não esperam que as *readiness probes* sejam bem-sucedidas. Se quiser esperar antes de executar uma sondagem de atividade, você pode definir `initialDelaySeconds` ou usar uma *startup probe*.

<br>

## Readiness probe

<br>

As **readiness probe** determinam quando um container está pronto para começar a aceitar tráfego. Isso é útil quando aguarda que um aplicativo execute tarefas inicias demoradas, como estabelecer conexão de rede, carregar arquivos e aquecer caches.

Isso é útil ao aguardar que um aplicativo execute tarefas iniciais demoradas, como estabelecer conexões de rede, carregar arquivos e aquecer caches.

As **readiness probe** são executadas no container durante todo o seu ciclo de vida.

<br>

## Startup probe

<br>

A **startup probe** verifica se o aplicativo em um container foi iniciado. Isso pode ser usado para adotar *liveness probe* em containers de inicialização lenta, evitando que sejam encerrados pelo *kubelet* antes de estarem em funcionamento.

Se a **startup probe** estiver configurada, ela desabilitará as *liveness probe* e *readiness probe* até que seja bem-sucedida.

A **startup probe** é executado apenas na inicialização, diferentemente das *liveness probe* e *readiness probe*, que são executados periodicamente.

<br>

## Saiba mais
[Kubernetes: Liveness, Readiness, and Startup Probes](https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/)