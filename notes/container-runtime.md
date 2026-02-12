# Container Runtime

É o responsável por executar os containers nos nós. Quando você está utilizando Docker ou `Podman` para executar containers em sua máquina, por exemplo, você está fazendo uso de algum container runtime, ou melhor, o seu container engine está fazendo o uso de algum container runtime.

## Tipos de Container Runtime

- Low-level: são executados diretamente pelo Kernel, como o `runc`, o `crun` e o `runsc`.
- High-Level: são executados por um Container Engine, como o `containerd` , o `CRI-O` e o `Podman`.
- Sandbox: são executados por um Container Engine e são responsáveis por executar containers de forma segura em `unikernels` ou utilizando algum proxy para fazer a comunicação com o kernel. Exemplo: `gVisor` .
- Virtualized: são executados por um Container Engine e que são responsáveis por executar containers de forma segura em máquinas virtuais. A performance aqui é um pouco menor do que quando temos um sendo executado nativamente. Exemplo: `Kata Containers`.
