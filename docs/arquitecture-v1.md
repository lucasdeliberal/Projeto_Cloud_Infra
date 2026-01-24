\# Projeto Cloud Infra – Kubernetes (k3s) na AWS



Projeto prático de infraestrutura cloud com foco em Kubernetes, alta disponibilidade básica e boas práticas de segurança, desenvolvido para demonstrar experiência real em ambientes de produção.



---



\## 🎯 Objetivo

Construir e documentar uma infraestrutura funcional em cloud utilizando Kubernetes, com aplicação containerizada distribuída em múltiplos nodes, simulando um cenário real de ambiente corporativo.



---



\## 🧱 Arquitetura (v1)

\- Cloud Provider: AWS

\- Região: sa-east-1 (São Paulo)

\- Cluster Kubernetes: k3s

\- Nodes:

&nbsp; - 1 Control Plane

&nbsp; - 1 Worker

\- Sistema Operacional: Ubuntu Server

\- Rede: VPC padrão AWS

\- Exposição de serviço: Kubernetes Service (NodePort)



---



\## 🐳 Aplicação

\- Site estático simples

\- Containerizado com Docker

\- Baseado em NGINX

\- Imagem distribuída entre os nodes do cluster



---



\## ☸️ Kubernetes

\- Deployment com múltiplos replicas

\- Service do tipo NodePort

\- Pods distribuídos entre control-plane e worker

\- Balanceamento básico de tráfego



---



\## 🔐 Segurança

\- Acesso SSH restrito por IP

\- Comunicação entre nodes permitida apenas via Security Group

\- NodePort exposto externamente apenas para testes controlados



---



\## 📂 Estrutura do Repositório

```text

docker/

&nbsp; ├── Dockerfile

&nbsp; └── index.html



k8s/

&nbsp; ├── deployment.yaml

&nbsp; └── service.yaml



docs/

&nbsp; └── architecture-v1.md



