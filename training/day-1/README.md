# Dia 1

> As anotações, nesse README, são anotações sobre a prática, vista no Dia 1 do treinamento. Anotações sobre teoria estão condençadas na pasta [/notes](/notes).

É possível criar um `cluster` com o comando `kind` utilizando a configuração, em `yaml` utilizando o comando:

```bash
kind create cluster --config cluster.yaml --name my_cluster
```

Podemos ver os `nodes` utilizando o comando:

```bash
kubectl get nodes
```

> O mesmo comando pode ser utilizado com diversos outros recursos, como, por exemplo, `kubectl get pods`.

## dry-run

O dry-run simula a execução da criação de recursos, como os pods. Por exemplo, o arquivo `./pod.yaml` foi criado utilizando o modo `dry-run` da seguinte forma:

```bash
kubectl run --image nginx --port 80 pop --dry-run=client -o yaml > pod.yml
```

## apply

Para poder criar o pod, a partir do `yaml` gerado pelo modo `dry-run` é possível utilizar:

```bash
kubectl apply -f pod.yaml
```
