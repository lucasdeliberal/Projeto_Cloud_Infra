# Projeto Cloud Infra – Kubernetes (k3s) na AWS

Projeto prático de infraestrutura cloud com foco em Kubernetes, alta disponibilidade básica e boas práticas de segurança, desenvolvido para demonstrar experiência real em ambientes de produção.

---

## 🎯 Objetivo
Construir e documentar uma infraestrutura funcional em cloud utilizando Kubernetes, com aplicação containerizada distribuída em múltiplos nodes, simulando um cenário real de ambiente corporativo.

---

## 🧱 Arquitetura (v1)
- Cloud Provider: AWS
- Região: sa-east-1 (São Paulo)
- Cluster Kubernetes: k3s (lightweight Kubernetes)
- Nodes:
  - 1 Control Plane
  - 1 Worker
- Sistema Operacional: Ubuntu Server
- Rede: VPC padrão AWS
- Exposição de serviço: Kubernetes Service (NodePort)

A aplicação é distribuída entre os nodes e acessada externamente por meio de um Service, garantindo balanceamento básico e tolerância a falhas.

---

## 🐳 Aplicação
- Site estático simples
- Containerizado com Docker
- Baseado em NGINX
- Imagem distribuída entre os nodes do cluster

---

## ☸️ Kubernetes
- Deployment com múltiplos replicas
- Service do tipo NodePort
- Pods distribuídos entre control-plane e worker
- Comunicação interna restrita via Security Group
- Exposição externa controlada (temporária para testes)

---

## 🔐 Segurança
- Acesso SSH restrito por IP
- Comunicação entre nodes permitida apenas via Security Group
- Range de NodePort liberado somente para comunicação interna
- Porta externa aberta apenas durante testes e posteriormente removida

---

## 📂 Estrutura do Repositório
```text
docker/
  ├── Dockerfile
  └── index.html

k8s/
  ├── deployment.yaml
  └── service.yaml

docs/
  └── architecture-v1.md
