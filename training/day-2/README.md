# Dia 2

> As anotações, nesse README, são anotações sobre a prática, vista no Dia 2 do treinamento. Anotações sobre teoria estão condençadas na pasta [/notes](/notes).

É possível ver os `pods` que estão em execução usando o comando:

```bash
kubectl get pods
```

O comando acima vai trazer os `pods` que estão rodando no `namespace` default. Para explicitar o `namespace` (por exemplo kube-system) podemos utilizar:

```bash
kubectl get pods -n kube-system
```

Para trazer todos os `pods` podemos utilizar:

```bash
kubectl get pods --all-namespaces
kubectl get pods -A
```

Para descrever os dados de um `pod` podemos utilizar

```bash
kubectl describe pods nome-do-pod
```
