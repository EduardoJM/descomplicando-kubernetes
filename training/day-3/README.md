# Dia 3

> As anotações, nesse README, são anotações sobre a prática, vista no Dia 2 do treinamento. Anotações sobre teoria estão condençadas na pasta [/notes](/notes).

## Deployment

Um `Deployment` é um objeto que representauma aplicação. Ele é responsável por gerenciar os Pods que compõem uma aplicação. Ele é uma abstração que permite atualizar os Pods e, também, fazer o rollback para uma versão anterior.

> Quando criamos um `Deployment` é possível definir o número de réplicas que queremos que ele tenha. O `Deployment` irá garantir que o número de Pods que ele esteja gerenciando seja o mesmo número de réplicas definido. Quando criamos um `Deployment`, automaticamente um `ReplicaSet` é criado junto. O `ReplicaSet` é o resposável por gerenciar os Pods para o `Deployment`.

## Criando um Deployment

Para criar um deployment, precisamos de um arquivo `yaml` conforme o exemplo [deployment.yaml](./yaml/deployment.yaml) e executamos o comando:

```bash
kubectl apply -f deployment.yaml
```

### Pontos importantes do Manifesto

O seletor é utilizado para identificar os Pods que o Deployment irá gerenciar, então é importante se atentar que os Pods tenham essas labels:

```yaml
# ...
spec:
  # ...
  selector:
    matchLabels:
      app: nginx-deployment
  template:
    metadata:
      labels:
        app: nginx-deployment
```

## Verificando o Deployment

É possível verificar os deployments fazendo:

```bash
kubectl get deployments
```

É possível filtrar por labels:

```bash
kubectl get deployments -l app=nginx-deployment
```

## Verificando o ReplicaSet

É possível verificar o replicaset:

```bash
kubectl get replicasets -l app=nginx-deployment
```

## Detalhando o Deployment

É possível detalhar o Deployment com:

```bash
kubectl describe deployment nginx-deployment
```

## Estratégias de Deployment

Existem duas estratégias de atualização para os Deployments no Kubernetes:

- RollingUpdate
- Recreate

### RollingUpdate

É a estratégia padrão do Kubernetes, ela é utilizada para atualizar os Pods de um Deployment de forma gradual, ou seja, ele atualiza um Pod por vez, ou um grupo de Pods por vez.

É possível definir como será a atualização dos Pods. Por exemplo, podemos definir a quantidade máxima de Pods que podem ficar indisponíveis durante a atualização ou podemos definir a quantidade máxima de Pods que podem ser criados durante a atualização.

Um exemplo de como funcionam as configurações está no arquivo: [deployment-rolling-update.yaml](./yaml/deployment-rolling-update.yaml). Detalhe para:

```yaml
# ...
spec:
  replicas: 10
  # ...
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
```

- `maxSurge`: define a quantidade máxima de Pods que podem ser criados a mais durante a atualização, ou seja, durante o processo de atualização. Podemos ter1 Pod a mais do que o número de Pods definidos no Deployment. Isso é útil pois agiliza o processo de atualização, já que o Kubernetes não precisa esperar que um Pod seja atualizado para criar um novo Pod.
- `maxUnavailable`: define a quantidade máxima de Pods que podem ficar indisponíveis durante a atualização, ou seja, durante o processo de atualização. Nós podemos ter 1 Pod indisponível por vez. Isso é útil pois garante que o serviço não fique indisponível durante a atualização.

### Recreate

A estratégia Recreate é uma estratégia de atualização que irá remover todos os Pods do Deployment e criar novos Pods com a nova versão da imagem. A parteboa é que o deploy acontecerá rapidamente, porém o ponto negativo é que o serviço ficará indisponível durante o processo de atualização.

> O tipo Recreate não possui nenhuma configuração.

> Exemplo de onde é mais usado: aplicações que não permitem rodar duas versões ao mesmo tempo.

## O comando rollout

O comando `rollout status` é utilizado para acompanhar o processo de atualização de um Deployment, ReplicaSet, DaemonSet, StatefulSet, Job e CronJob. O comando `rollout status` é muito útil pois ele nos informa se o processo de atualização está em andamento, se ele foi concluído com sucesso ou se ele falhou.

Exemplo:

```bash
kubectl rollout status deployment nginx-deployment
```

## Fazendo rollback

Para fazer um rollback da versão das imagens dos containers, podemos utilizar o comando:

```bash
kubectl rollout undo deployment nginx-deployment
```

é possível, visualizar o histórico das atualizações:

```bash
kubectl rollout history deployment nginx-deployment
```

e ver o arquivo do histórico:

```bash
kubectl rollout history deployment nginx-deployment --revision=1
```

e fazer o rollback para a versão específica:

```bash
kubectl rollout undo deployment nginx-deployment --to-revision=1
```
