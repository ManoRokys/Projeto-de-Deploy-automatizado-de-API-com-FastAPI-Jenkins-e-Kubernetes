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

### Instalação do Rancher Desktop e Ativação do Kubernetes
- Instale o Rancher Desktop.
- Ative o cluster Kubernetes local.

> ![Rancher e Kubernetes](INSIRA_LINK_DA_IMAGEM)

### Configuração do Docker Hub
- Adicione suas credenciais no Docker Hub.
- Gere um token de acesso pessoal.

> ![Configurações do Docker Hub](INSIRA_LINK_DA_IMAGEM)

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

```bash
cd backend
docker-compose up --build
```

> ![Primeira montagem](INSIRA_LINK_DA_IMAGEM)

Acesse a API em:  
[http://localhost:8000](http://localhost:8000)

> ![Sistema na porta 8000](INSIRA_LINK_DA_IMAGEM)

---

## 4. Configuração do Jenkins

### Instalação de Plugins

Instale os plugins:
- Git
- Docker
- Pipeline

### Configurações do Jenkins

- Configure credenciais para Docker Hub (`docker-hub-credentials`) e GitHub.

> ![Credenciais do Jenkins](INSIRA_LINK_DA_IMAGEM)

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
