# Dia 2

> As anotações, nesse README, são anotações sobre a prática, vista no Dia 2 do treinamento. Anotações sobre teoria estão condençadas na pasta [/notes](/notes).

Os pods podem ser criados de duas formas: utilizando um comando no terminal ou por meio de um arquivo de manifesto `yaml`. Vamos começar com os comandos e, depois, com os manifestos.

## Criando um Pod com Comando

Para criar um pod pela linha de comando, podemos utilizar:

```bash
kubectl run giropops --image=nginx --port=80
```

## Listar Pods

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

> É possível customizar a exibição dos dados dos Pods, com o argumento `-o`
>
> kubectl get pods <nome_do_pod> -o json
>
> Temos as opções: json, yaml e wide, sendo que wide mostra mais detalhes sobre o Pod como, por exemplo, o IP do Pod e o Node onde o Pod está sendo executado.

## Descrevendo os Pods

Para descrever os dados de um `pod` podemos utilizar

```bash
kubectl describe pods nome-do-pod
```

## Deletando um Pod

Para deletar um pod basta executar:

```bash
kubectl delete pods giropops
```

## Criando um Pod com arquivos manifestos

Você pode criar um arquivo manifesto como o arquivo [pod1.yaml](./yaml/pod1.yaml) e aplicar o seu conteúdo utilizando o comando:

```bash
kubectl apply -f pod1.yaml
```

> Caso o objeto já exista, o comando apply irá atualizar o mesmo. Assim, é possível editar o arquivo yaml e depois aplicar novamente.
>
> O comando create também cria o objeto que está descrito no arquivo yaml no cluster. Porém, caso o objeto já exista, ele irá retornar um erro. Por esse motivo, o comando apply é mais utilizado.

Para criar um pod com mais containers basta adicionar em `spec.containers`. Exemplo disso está no arquivo [pod2.yaml](./yaml/pod2.yaml).

## Se conectando e executando comandos no Pod

O comando `attach` é utilizado para se conectar a um container que está rodando dentro de um Pod. Nesse caso, não estamos criando um processo, apenas nos conectando ao container, então se um serviço como, por exemplo, o nginx estiver rodando, ficaremos conectados vendo o processo do nginx.

Por isso, existe o comando `exec` que cria um novo processo dentro do container. Assim:

```bash
kubectl attach girus
```

```bash
kubectl exec girus -it -- sh
```

> O parâmetro -it é usado para que o comando `exec` crie um processo dentro do container com interatividade e com um terminal, fazendo com que o comando `exec` se comporte como um `attach`, porém criando um novo processo no container.

## Limites de memória e CPU

Podemos adicionar limites de recursos fazendo, conforme disponível no arquivo [pod3-limits.yaml](./yaml/pod3-limits.yaml):

```yaml
# ...
spec:
  containers:
    - image: ubuntu
      # ...
      resources:
        limits:
          cpu: "0.5"
          memory: "128Mi"
        requests:
          cpu: "0.3"
          memory: "64Mi"
```

O campo `limits` é utilizado para definir os limites máximos de recursos que o container pode utilizar e o campo `requests` é utilizado para definir os recursos garantidos ao container.
