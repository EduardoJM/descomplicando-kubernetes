# Virtualização vs Containers

## Virtualização

A virtualização é uma solução para o problema de isolar e ter dois ambientes compartilhando a mesma máquina. O problema é que a virtualização tem um custo: os dois sistemas não compartilham o mesmo Kernel. Se quisermos uma aplicação web pequena, virtualizada, precisaríamos inicializar um kernel e carregar muitas bibliotecas. É útil para quem quer um sistema operacional totalmente virtualizado mas não é o ideal para aplicações gerais.

## Container

Os containers compartilham os mesmo recursos físicos da máquina. Em resumo, um container é um espaço isolado em nosso computador onde podemos executar um sistema operacional diferente e a partir desse sistema, instalar o que quisermos e executar qualquer comando sem afetar a máquina principal (o host).

## Principais Benefícios

- Experimentação: como as dependências pertencem ao container, não temos problema de conflito de bibliotecas e versões, bem como não precisamos ficar instalando e desinstalando coisas.
- Mudança de Contexto: as vezes trabalhamos em vários projetos e trocar de contextos: por exemplo, um projeto usando PostgreSQL 9.5 e outro usando PostgreSQL 11, é muito difícil fazer essa troca de forma manual.
- Uniformização: utilizando um container, temos controle total sobre o aplicativo, pois independente de onde esteja rodando, o container é isolado, executando as mesmas versões de bibliotecas e etc.
- Agnóstico ao lugar de Deploy: independente de onde for fazer o deploy, os comandos serão os mesmos, além de que todas as provedoras de nuvem vão ter meios fáceis de executar seus containers.

[Thinking Like Containers](https://dev.to/leandronsp/thinking-like-containers-3k24)
