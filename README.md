# ☁️ Projeto Cloud Infra — Kubernetes (k3s) na AWS

Projeto prático de **Infraestrutura Cloud e Kubernetes**, desenvolvido com foco em **ambiente realista de produção**, cobrindo desde provisionamento até **CI/CD, observabilidade, alertas e SLOs**.

Este projeto foi construído como **portfólio técnico**, priorizando decisões arquiteturais, troubleshooting real, boas práticas e documentação clara — exatamente como ocorre no dia a dia de times de **Infra, Cloud, DevOps e SRE**.

---

## 🎯 Objetivo do Projeto

Projetar, implementar, operar e documentar uma **infraestrutura Kubernetes funcional na AWS**, utilizando componentes open-source e soluções custo-efetivas, abordando:

- Kubernetes (k3s) em ambiente cloud
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
- **Domínio:** `lucasdeliberal.com.br` (Registro.br + Route 53)

### ☸️ Cluster Kubernetes

- **Distribuição:** k3s (lightweight Kubernetes)
- **Topologia:**

| Função        | Quantidade | Observações |
|--------------|------------|-------------|
| Control Plane | 1 | API Server, Scheduler e Controllers |
| Worker Node   | 1 | Execução das workloads |
| Total         | 2 | Preparado para expansão |

- **Ingress Controller:** NGINX  
- **CNI:** Flannel  
- **DNS Interno:** CoreDNS  

---

## 🐳 Aplicação

- **Tipo:** Site estático
- **Servidor Web:** NGINX
- **Containerização:** Docker
- **Imagem:** Publicada no GitHub Container Registry (GHCR)
- **Objetivo:** Aplicação simples por design, com foco total na infraestrutura

---

## 🌐 Exposição da Aplicação

Fluxo de exposição semelhante a ambientes de produção:

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

- **Aplicação:**  
  👉 https://portfolio.lucasdeliberal.com.br

- **Grafana (Observabilidade):**  
  👉 https://grafana.lucasdeliberal.com.br

---

## 🔐 HTTPS & Certificados

- **Ferramenta:** cert-manager  
- **CA:** Let’s Encrypt  
- **Validação:** HTTP-01  
- **Ingress:** NGINX  

Certificados emitidos automaticamente e renovados sem intervenção manual.

---

## 🔁 CI/CD — GitHub Actions

Pipeline automatizado para **build e deploy no Kubernetes**:

### 🔄 Fluxo

1. Push para a branch `main`
2. Build da imagem Docker
3. Push da imagem para o **GitHub Container Registry**
4. Deploy automático no cluster Kubernetes via `kubectl`

### 🔐 Autenticação

- ServiceAccount dedicada no cluster
- RBAC com permissões mínimas necessárias
- Kubeconfig gerado especificamente para CI
- Secrets armazenados de forma segura no GitHub

---

## 📊 Observabilidade

### Stack Utilizada

- **Prometheus Operator**
- **Prometheus**
- **Alertmanager**
- **Grafana**
- **Node Exporter**
- **kube-state-metrics**

Instalação realizada via **Helm (kube-prometheus-stack)**.

---

### 📈 Dashboards

Dashboards configurados no Grafana para:

- Saúde do cluster
- Nodes (CPU, memória, disco)
- Kubernetes (pods, deployments, namespaces)
- Ingress NGINX (tráfego, latência, erros)

Dashboards customizados exportados e versionados.

---

## 🚨 Alertas (Prometheus)

Alertas criados manualmente utilizando **PrometheusRule**, versionados no repositório.

### Estrutura

```text
k8s/monitoring/alerts/
├── infra/
├── kubernetes/
└── ingress/
