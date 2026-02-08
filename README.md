# ☁️ Projeto Cloud Infra — Kubernetes (k3s) na AWS

Projeto prático de **Infraestrutura Cloud, Kubernetes e SRE**, construído com foco em **ambiente realista de produção**, cobrindo **provisionamento, CI/CD, observabilidade, alertas e SLOs**.

Este projeto foi desenvolvido como **portfólio técnico**, priorizando:
- decisões arquiteturais conscientes  
- troubleshooting real  
- boas práticas de mercado  
- documentação clara e rastreável  

Tudo aqui reflete **cenários reais enfrentados por times de Infra, Cloud, DevOps e SRE**.

---

## 🎯 Objetivo do Projeto

Projetar, implementar, operar e documentar uma **infraestrutura Kubernetes funcional na AWS**, utilizando ferramentas open-source e soluções custo-efetivas, abordando:

- Kubernetes em cloud (k3s)
- Exposição segura de aplicações (Ingress + TLS)
- DNS e HTTPS com certificados válidos
- CI/CD com GitHub Actions
- Observabilidade completa (métricas, dashboards e alertas)
- Definição de SLIs, SLOs e Error Budget
- Troubleshooting real de cluster Kubernetes

---

## 🧱 Arquitetura Geral

### ☁️ Cloud & Infra

- **Cloud Provider:** AWS  
- **Região:** sa-east-1 (São Paulo)  
- **Sistema Operacional:** Ubuntu Server  
- **Rede:** VPC padrão AWS  
- **IP Público:** Elastic IP  
- **Domínio:** `lucasdeliberal.com.br`  

---

### ☸️ Cluster Kubernetes

- **Distribuição:** k3s (lightweight Kubernetes)
- **Topologia atual:**

| Função        | Quantidade | Observações |
|--------------|------------|-------------|
| Control Plane | 1 | API Server, Scheduler, Controllers |
| Worker Node   | 1 | Execução das workloads |
| Total         | 2 | Preparado para expansão |

- **CNI:** Flannel  
- **DNS interno:** CoreDNS  
- **Ingress Controller:** NGINX  

---

## 🐳 Aplicação

- **Tipo:** Site estático (portfolio técnico)
- **Servidor Web:** NGINX
- **Containerização:** Docker
- **Registry:** GitHub Container Registry (GHCR)
- **Imagem:** `ghcr.io/lucasdeliberal/portfolio-site:latest`

> A aplicação é propositalmente simples — o foco do projeto está **100% na infraestrutura**.

---

## 🌐 Exposição da Aplicação

Fluxo inspirado em ambientes de produção:

1. **Service (ClusterIP)**  
   Comunicação interna entre Pods.

2. **Ingress (NGINX)**  
   - Roteamento HTTP/HTTPS  
   - Terminação TLS  
   - Integração com cert-manager  

3. **DNS + Elastic IP (AWS)**  
   - Domínios apontando para Elastic IP  
   - Evita indisponibilidade após reinício de instâncias  

### 🔗 URLs Ativas

- **Aplicação (Portfolio):**  
  👉 https://portfolio.lucasdeliberal.com.br  

- **Grafana (Observabilidade):**  
  👉 https://grafana.lucasdeliberal.com.br  

---

## 🔐 HTTPS & Certificados

- **Ferramenta:** cert-manager  
- **CA:** Let’s Encrypt  
- **Validação:** HTTP-01  
- **Ingress:** NGINX  

Certificados TLS emitidos automaticamente e renovados sem intervenção manual.

---

## 🔁 CI/CD — GitHub Actions

Pipeline automatizado para **build e deploy contínuo no Kubernetes**.

### 🔄 Fluxo do Pipeline

1. Push para a branch `main`
2. Build da imagem Docker
3. Push da imagem para o **GitHub Container Registry**
4. Deploy automático no cluster Kubernetes via `kubectl`

### 🔐 Segurança e Autenticação

- ServiceAccount dedicada no cluster
- RBAC com permissões mínimas
- Kubeconfig exclusivo para CI
- Secrets armazenados de forma segura no GitHub

---

## 📊 Observabilidade

### Stack Utilizada

- Prometheus Operator
- Prometheus
- Alertmanager
- Grafana
- Node Exporter
- kube-state-metrics

Instalação via **Helm (kube-prometheus-stack)**.

---

### 📈 Dashboards

Dashboards configurados no Grafana para:

- Saúde geral do cluster
- Nodes (CPU, memória, disco)
- Kubernetes (pods, deployments, namespaces)
- Ingress NGINX (tráfego, latência, erros)

Dashboards customizados exportados e versionados no repositório.

---

## 🚨 Alertas (Prometheus)

Alertas definidos manualmente utilizando **PrometheusRule**, versionados em código.

### Estrutura

```text
k8s/monitoring/alerts/
├── infra/
├── kubernetes/
└── ingress/
