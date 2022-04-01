# Conteirizando sua aplicação Python/MongoDB e Implantando em Cluster Kubernetes

Neste repositório apresento o resultado do encapsulamento de uma aplicação construída em Python e MongoDB em um <b>Container Docker</b> e posteriormente realizando o deploy/implantação da aplicação em um ambiente <b>Kubernetes</b>.

O arquivo de encapsulamento <b>Dockerfile</b> segue uma configuração básica, cujo o principal objetivo é demonstra a facilidade na configuração, distribuição e execução de uma aplicação encapsulada em containers.

Há diversos benefícios em encapsular uma aplicação em container, mas o principal é a portabilidade, já que o projeto pode ser executado em qualquer máquina que possua o [Docker](https://docs.docker.com/get-docker/) instalado, tornando a Aplicação independente de SO e/ou qualquer outra configuração/instalação.

De forma análoga, segue o arquivo de <b>manifesto na linguagem YAML</b>, exemplificado a realização do deploy no Kubernetes de forma declarativa.

O [Kubernetes](https://kubernetes.io/pt-br/) é um orquestrador de containers, que automatiza a gerencia de aplicações em containers, auxiliando na implantação e dimensionamento dos containers, nos processos de garantia de disponibilidade, balanceamento de carga e escalabilidade das aplicações nos containers.

### Iniciativa Kubernetes - Aula 02:

Este repositório é parte da atividade prática da Aula 02 do Curso [Iniciativa Kubernetes](https://iniciativakubernetes.com.br/), ocorrido de 28 de março a 01 de abril de 2022, promovido pela [Kubedev.io](https://kubedev.io/).

## 🛒 Requisitos do Projeto:

Antes de começar, você vai precisar ter instalado em sua máquina os seguintes recursos:

- [Git](https://git-scm.com/);
- [Docker](https://docs.docker.com/get-docker/);
- [K3D](https://k3d.io/v5.4.1/); e
- [Kubectl CLI](https://kubernetes.io/docs/tasks/tools/).

## 📀 Executando o Projeto:

Para testarmos a aplicação, temos que executar os 6 passos a seguir:

1. [Fazer download do Projeto](#download-github)
2. [Criar Imagem Docker](#build-image)
3. [Enviar Imagem ao seu DockerHub](#push-image)
4. [Criar Cluster Kubernetes](#create-cluster)
5. [Aplicar Manifesto Kubernetes](#apply-manifest)
6. [Acessar a Aplicação](#acessando-app)

<a name="download-github"></a>

### 1. Fazer download do Projeto

- Baixe este Repositório, executando o comando Git:

```bash
git clone https://github.com/aguiardafa/rotten-potatoes
```

<a name="build-image"></a>

### 2. Criar Imagem Docker do Projeto

1. Acesse a pasta `src` do Repositório pelo terminal de comandos;
2. Execute o comando abaixo para criar a imagem Docker do projeto:

```bash
docker image build -t <seu-username-dockerhub>/rotten-potatoes:v1 .
```

<a name="push-image"></a>

### 3. Enviar Imagem Docker do Projeto ao seu Repositório no DockerHub

1. Ainda pelo terminal, aberto na raiz da pasta `src` do Repositório, primeiramente execute o comando para realizar o login no [Docker Hub](https://hub.docker.com/):

```bash
docker login
```

- <b>Obs.:</b> Você deverá realizar login com suas credenciais do Docker Hub.

2. Após logado, execute de envio da imagem criada para seu repositório de imagens no DockerHub:

```bash
docker push <seu-username-dockerhub>/rotten-potatoes:v1
```

<a name="create-cluster"></a>

### 4. Criar Cluster Kubernetes

1. Execute o comando abaixo, que irá criar e executar o Cluster Kubernetes, expondo o `Load Balance` na porta `8080` do computador:

```bash
k3d cluster create meucluster --agents 1 --servers 1 -p "8080:30000@loadbalancer"
```

<a name="apply-manifest"></a>

### 5. Aplicar Manifesto Kubernetes no Cluster criado

1. Acesse a pasta `k8s` do Repositório pelo terminal de comandos;
2. Execute o comando abaixo para aplicar os comandos configurados no arquivo `deployment.yaml`, referente ao Manifesto Kubernetes, no Cluster recém criado:

```bash
kubectl apply -f  deployment.yaml
```

- <b>Obs.:</b> Antes de aplicar o manifesto, você deverá editar o arquivo na `linha 58`, inserindo o nome da imagem que você enviou ao DockerHub: `<seu-username-dockerhub>/rotten-potatoes:v1`.

<a name="acessando-app"></a>

### 6. Acessar a Aplicação Python/MongoDB

1. Pelo navegador de sua preferência, acesse a url `http://localhost:8080` para visualizar a Aplicação;
2. Se os passos anteriores foram executados corretamente, a resposta será semelhante a tela abaixo:
<p align="center"><img alt="rotten-potatoes" id="foto1" title="#FotoProjeto" height="450px" src="https://raw.githubusercontent.com/aguiardafa/rotten-potatoes/main/.github/rotten-potatoes.png" /></p>

## 👨‍💻Autor

<a href="https://github.com/aguiardafa" style="text-decoration: none;">
<img style="border-radius: 50% !important;" src="https://avatars.githubusercontent.com/u/16319889?v=4" width="48px" height="48px" alt="Diego Aguiar"/>
<br />
<span> Feito por Diego Aguiar 👋 Entre em contato! </span> 
</a>
