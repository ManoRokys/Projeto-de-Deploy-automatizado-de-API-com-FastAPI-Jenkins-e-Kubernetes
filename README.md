# Projeto de Deploy Automatizado de API com FastAPI, Jenkins e Kubernetes

Este projeto demonstra a automação do ciclo de vida de uma API desenvolvida com FastAPI, utilizando Jenkins para build, push e deploy em um cluster Kubernetes local gerenciado pelo Rancher Desktop.

Abaixo, você encontrará os passos para reproduzir o projeto, as tecnologias utilizadas, capturas de tela do processo e uma visão geral da pipeline funcionando.

---

## 1. Pré-requisitos

- Instale o **Docker Desktop** para gerenciar contêineres.
- Instale o **Rancher Desktop** para configurar um cluster Kubernetes local.
- Instale o **Jenkins** em um ambiente Windows.
- Configure um repositório no GitHub:  
  [https://github.com/ManoRoKys/Projeto-de-Deploy-automatizado-de-API-com-FastAPI-Jenkins-e-Kubernetes](https://github.com/ManoRoKys/Projeto-de-Deploy-automatizado-de-API-com-FastAPI-Jenkins-e-Kubernetes)
- Crie uma conta no **Docker Hub** para armazenar as imagens.

---

## 2. Configuração Inicial

### Instalação do Jenkins
- Baixe e instale o Jenkins no Windows.
- Configure-o para rodar em `http://localhost:8080`.

Obs: Escolha os diretórios ou configurações que mais te agradem caso for necessário.
> ![Captura de tela 2025-06-10 090852](https://github.com/user-attachments/assets/508481d1-ed30-4653-8637-f91d8492741c)
> ![Captura de tela 2025-06-10 090902](https://github.com/user-attachments/assets/73eac217-8280-448b-8807-4980cd549d3f)
> ![Captura de tela 2025-06-10 090923](https://github.com/user-attachments/assets/8de66117-28b8-4829-8bc2-af88a094dde2)
> ![Captura de tela 2025-06-10 090933](https://github.com/user-attachments/assets/d2ecd387-9ebc-4cba-8c91-d50b0f649182)
> ![Captura de tela 2025-06-10 090944](https://github.com/user-attachments/assets/f685a4d5-8bd4-4d38-9674-4276f058f3e6)
> ![Captura de tela 2025-06-10 091001](https://github.com/user-attachments/assets/8d777e06-ac47-4019-af45-370806596ec8)
> ![Captura de tela 2025-06-10 091015](https://github.com/user-attachments/assets/14d07a8c-88db-4339-a8be-d8adb85e2003)

Acesse `http://localhost:8080` para terminar as configurações iniciais.
> ![Captura de tela 2025-06-10 091225](https://github.com/user-attachments/assets/2d540a04-694b-4465-907c-455983a7d5f6)
> ![Captura de tela 2025-06-10 091613](https://github.com/user-attachments/assets/06bcfa62-504c-49b1-b88d-470b145b6dcc)
Tela inicial do Jenkins.
> ![Captura de tela 2025-06-10 091856](https://github.com/user-attachments/assets/98ddf5f3-f1da-451d-8edb-40c607e896da)




### Instalação do Rancher Desktop e Ativação do Kubernetes
- Instale o Rancher Desktop.
- Ative o cluster Kubernetes local.

Obs: Escolha os diretórios ou configurações que mais te agradem caso for necessário.
> ![Captura de tela 2025-06-10 092021](https://github.com/user-attachments/assets/50b6fbf8-f62b-484e-b4b2-d4aa3e75838b)
> ![Captura de tela 2025-06-10 092032](https://github.com/user-attachments/assets/700c076e-f0bd-4de3-bf0e-bb46931446aa)
>
> Após o passo seguinte irá abrir uma tela de confirmação de administrador, coloque a senha ou apenas aprove.
> ![Captura de tela 2025-06-10 092040](https://github.com/user-attachments/assets/c9ca7ffb-0c05-4cf9-a046-5915ccdc58d4)
> ![Captura de tela 2025-06-10 092113](https://github.com/user-attachments/assets/a529f65b-e64e-4db3-8e23-100d772c7c16)

> Espere a tela do rancher desktop abrir
> 
> ![Captura de tela 2025-06-10 092607](https://github.com/user-attachments/assets/ce84fd6a-9306-4c36-ba9d-67052e1891c2)
> ![Captura de tela 2025-06-10 092551](https://github.com/user-attachments/assets/6f51ff6a-3a8a-4752-b60d-59f2c2df0a0c)
> ![Captura de tela 2025-06-10 092557](https://github.com/user-attachments/assets/83edc173-1ba6-4e71-a301-ab97dd983777)



### Configuração do Docker Hub
- Crie uma conta (caso não tenha uma) no Docker Hub.
- Acesse os seus repositórios.

> ![Captura de tela 2025-06-10 093956](https://github.com/user-attachments/assets/63472a46-fb8d-4611-b0ae-5862213fb19a)
> ![Captura de tela 2025-06-10 094014](https://github.com/user-attachments/assets/68bdb1a7-d83e-4479-8577-7bc8901651df)


---

## 3. Estrutura do Projeto

Clone o repositório:

```bash
git clone https://github.com/ManoRoKys/Projeto-de-Deploy-automatizado-de-API-com-FastAPI-Jenkins-e-Kubernetes.git
cd Projeto-de-Deploy-automatizado-de-API-com-FastAPI-Jenkins-e-Kubernetes
```

### Estrutura de Arquivos

- `backend/Dockerfile`: Define a imagem da API.
- `backend/Jenkinsfile`: Configura a pipeline Jenkins.
- `backend/deployment.yaml` e `backend/service.yaml`: Configuram o deploy no Kubernetes.
- `backend/main.py`: Código da API FastAPI.
- `backend/requirements.txt`: Dependências Python.

### Primeira Montagem do Projeto

Execute a API localmente:

entre na pasta /backend e rode:

> ![Captura de tela 2025-06-10 101558](https://github.com/user-attachments/assets/bbf9b2e8-885e-4b67-a051-7aa9107448a0)
> 
> ![Captura de tela 2025-06-10 101645](https://github.com/user-attachments/assets/7760720a-61f0-4f9b-85f9-188f8526c35e)

Acesse a API em:  
[http://127.0.0.1:8000]
> ![Captura de tela 2025-06-10 101713](https://github.com/user-attachments/assets/15a22e9a-a30f-472a-bc19-465df90adf36)
>
> Testando a rota /cat
> 
> ![Captura de tela 2025-06-10 104658](https://github.com/user-attachments/assets/bae776e2-8654-4116-ae40-2c8a4f7c21c9)

Executando a API localmente com o Docker:

> Faça o login com o comando
> ![Captura de tela 2025-06-11 091638](https://github.com/user-attachments/assets/971ebfd7-c8d4-415b-8b1d-0cb5714e7d84)
>
> Copie o codigo informado no passo anterior e cole no site
>
> ![Captura de tela 2025-06-11 091651](https://github.com/user-attachments/assets/85ca652f-bf72-47d6-8584-df02f0eebe30)
>
> Espere essa mensagem aparecer
>
> ![Captura de tela 2025-06-11 091732](https://github.com/user-attachments/assets/8fcf57e2-8fba-4316-9f39-9387b7e3b87b)
>
> Faça o Build e o Push da imagem normalmente
>
> ![Captura de tela 2025-06-11 091346](https://github.com/user-attachments/assets/872d623a-9991-4872-9b4a-24c7ac45f7ea)
> ![Captura de tela 2025-06-11 091512](https://github.com/user-attachments/assets/8ec72956-0d43-4643-bed2-0c6dbab1f0df)
> ![Captura de tela 2025-06-11 091809](https://github.com/user-attachments/assets/6b8c108b-d336-4a01-a1ed-2bd6465352c5)
>
> Docker refletido no repositório do Docker Hub
>
> ![Captura de tela 2025-06-11 091911](https://github.com/user-attachments/assets/d496b4e0-ba54-49ca-b470-37604da29115)

Ou usar o docker-compose
> ![Captura de tela 2025-06-11 092317](https://github.com/user-attachments/assets/5f3368ec-1136-42cd-ac36-5094ff0feb80)
> ![Captura de tela 2025-06-11 092330](https://github.com/user-attachments/assets/eb52a241-e44b-4aad-b386-ed4e4bcf55a8)
> 
```bash
docker-compose up --build
```

Acesse a API em:  
[http://localhost:8000]

>  ![Captura de tela 2025-06-11 092415](https://github.com/user-attachments/assets/13f36e91-6f8c-4871-b9c0-c63ca1ab6a05)
> 
>  Testando a rota /cat
>
> ![Captura de tela 2025-06-11 092427](https://github.com/user-attachments/assets/0482e274-7661-40ae-b221-e5a9ee96192a)

Criando os arquivos do kubernetes no sistema:

> ![Captura de tela 2025-06-11 094059](https://github.com/user-attachments/assets/16723ad1-81b6-43c2-9ed1-14fe336dfbd5)
> 
> ![Captura de tela 2025-06-11 094241](https://github.com/user-attachments/assets/2992e45b-e3c0-42bd-bdeb-0ef48be681c4)
> 
> ![Captura de tela 2025-06-11 094558](https://github.com/user-attachments/assets/eafeabc4-84bd-43f2-9099-4cfba1690600)
> 
> ![Captura de tela 2025-06-11 094649](https://github.com/user-attachments/assets/a2939890-d384-4fcf-ba98-f686e973a3a9)
>
> ![Captura de tela 2025-06-11 094734](https://github.com/user-attachments/assets/44ed7cb0-24b6-496a-af22-3d8fa9bf1ac5)
> 
> ![Captura de tela 2025-06-11 094739](https://github.com/user-attachments/assets/5f04562d-3e9b-4ccb-8cf7-14a1a1d807b1)
> 
> ![Captura de tela 2025-06-11 095615](https://github.com/user-attachments/assets/0be9edd8-50b1-4349-a6c7-68b53a03e2b7)
> 
> ![Captura de tela 2025-06-11 095640](https://github.com/user-attachments/assets/5859a72e-c1d6-49df-88b5-9fb40da2c4eb)

Acesse a API em:  
[http://localhost:30001]

> ![Captura de tela 2025-06-11 095702](https://github.com/user-attachments/assets/7221fc4b-8d39-428e-b02f-85fa3f0f9441)
>
>  Testando a rota /cat
>
> ![Captura de tela 2025-06-11 095710](https://github.com/user-attachments/assets/5c7c36f9-e6a9-4913-ad55-0baa79b0c9df)


---

## 4. Configuração do Jenkins

### Instalação de Plugins

Instale os plugins:
- Docker
- Docker Pipeline
- Kubernetes CLI

> ![Captura de tela 2025-06-10 091917](https://github.com/user-attachments/assets/711db3a0-3245-45f4-bfe7-d7b5da252e3c)
> 
> ![Captura de tela 2025-06-10 091921](https://github.com/user-attachments/assets/2712badf-e1c1-4fd2-a481-78a673515e62)
> ![Captura de tela 2025-06-10 092759](https://github.com/user-attachments/assets/59347ae6-335d-47b0-a56d-de392cc84403)
> ![Captura de tela 2025-06-10 092923](https://github.com/user-attachments/assets/743aea4f-ebb1-4086-a7d9-32ce644972e0)
> ![Captura de tela 2025-06-10 093041](https://github.com/user-attachments/assets/69c03e55-5202-4372-9508-1c28d18f8d4f)


### Configurações do Jenkins

- Configure credenciais para kubeconfig localizado nessa pasta:
- ![Captura de tela 2025-06-10 093838](https://github.com/user-attachments/assets/78657c26-fa50-48f6-899d-8c0d264cc7bc)
(`kubeconfig`).

> ![Captura de tela 2025-06-10 093132](https://github.com/user-attachments/assets/7828c396-fb87-4c24-88a5-514a5bb93c14)
> ![Captura de tela 2025-06-10 093711](https://github.com/user-attachments/assets/2590d36f-85ff-4d49-8c53-6303bbc83f6a)
> ![Captura de tela 2025-06-10 093719](https://github.com/user-attachments/assets/b89fa3fa-c32c-4445-a153-3f87869b3772)
> ![Captura de tela 2025-06-10 093854](https://github.com/user-attachments/assets/d293cbbf-d98b-4aee-9c0a-2802b7875212)


### Criação da Pipeline

- Crie uma pipeline chamada `fastapi-pipeline`.
- Configure o SCM como Git, apontando para `backend/Jenkinsfile`.

> ![Pipeline configurada](INSIRA_LINK_DA_IMAGEM)

### Primeiras Execuções

- Execute a pipeline manualmente pela primeira vez.

> ![Pipeline executando](INSIRA_LINK_DA_IMAGEM)

---

## 5. Automação com GitHub e ngrok

### Git Push

Execute:

```bash
git add .
git commit -m "Atualização do código"
git push origin dev
```

> ![Git push](INSIRA_LINK_DA_IMAGEM)

### Configuração do Webhook

- Use o ngrok para expor o Jenkins local:
  ```bash
  ngrok http 8080
  ```
- Configure o webhook no GitHub com a URL gerada (ex.: `https://abc123.ngrok.io/github-webhook/`).

> ![Webhook configurado](INSIRA_LINK_DA_IMAGEM)

---

## 6. Deploy no Kubernetes

### Configuração do `kubectl`

- Configure o `kubeconfig` no Jenkins como **Secret File** (nome: `kubeconfig`).

### Execução do Deploy

- Após o push, a pipeline executa o deploy automático via Jenkins.

> ![Execução do kubectl](INSIRA_LINK_DA_IMAGEM)

### Verificação

Execute:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

> ![Verificação do cluster](INSIRA_LINK_DA_IMAGEM)

Acesse a API em:  
[http://localhost:30001](http://localhost:30001)

> ![API funcionando](INSIRA_LINK_DA_IMAGEM)

---

## 7. Testes

### Captura da Execução do Docker

> ![Execução do Docker](INSIRA_LINK_DA_IMAGEM)

### Testes Após o Deploy

> ![API funcionando após deploy](INSIRA_LINK_DA_IMAGEM)

---

## Tecnologias Usadas

- **FastAPI**: Framework para criar a API em Python.
- **Docker**: Para containerização da aplicação.
- **Docker Compose**: Para orquestração local dos contêineres.  
  > ![docker-compose](INSIRA_LINK_DA_IMAGEM)
- **Jenkins**: Para automação do CI/CD (build, push e deploy).
- **Kubernetes**: Para orquestração e deploy da aplicação (via Rancher Desktop).
- **GitHub**: Para controle de versão e integração com webhooks.
- **ngrok**: Para expor o Jenkins localmente.

---

## Licença

Este projeto é livre para uso educacional e pessoal. Contribuições são bem-vindas!
