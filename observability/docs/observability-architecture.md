# Arquitetura de Observabilidade

Este projeto utiliza uma stack completa de observabilidade baseada em
**Prometheus** e **Grafana**, executando sobre **Kubernetes (k3s)** em ambiente
**AWS**.

O objetivo é fornecer visibilidade total sobre:
- Infraestrutura (nós)
- Cluster Kubernetes
- Tráfego HTTP (Ingress)
- Saúde e desempenho das aplicações

---

## Componentes

- **Prometheus**
  - Responsável pela coleta e armazenamento de métricas.
  - Gerenciado via Prometheus Operator.

- **Node Exporter**
  - Coleta métricas de nível de sistema operacional dos nós.
  - CPU, memória, disco, rede e load average.

- **kube-state-metrics**
  - Fornece métricas sobre objetos do Kubernetes.
  - Deployments, Pods, Services, Nodes, etc.

- **Ingress NGINX Metrics**
  - Métricas de tráfego HTTP.
  - Latência, códigos de resposta, throughput e erros.

- **Grafana**
  - Visualização e análise das métricas.
  - Dashboards importados e customizados.

---

## Acesso

- **Grafana (HTTPS)**  
  https://grafana.lucasdeliberal.com.br

- **Prometheus**
  - Exposto apenas internamente no cluster.
  - Consumido diretamente pelo Grafana.

---

## Dashboards Utilizados

- **Node Exporter Full**
  - Visão detalhada dos recursos dos nós.

- **Kubernetes Cluster Overview**
  - Estado geral do cluster Kubernetes.

- **NGINX Ingress Controller**
  - Métricas de tráfego e desempenho do Ingress.

Os dashboards são baseados em modelos amplamente utilizados pela comunidade e
exportados em JSON para versionamento no repositório.

---

## Segurança

- Comunicação via **HTTPS** com certificados gerados pelo **Let's Encrypt**.
- Exposição controlada através de **Ingress NGINX**.
- Prometheus e métricas não expostos publicamente.
- Integração com Kubernetes RBAC.

---

## Objetivo do Projeto

Demonstrar uma arquitetura realista de observabilidade em Kubernetes,
seguindo boas práticas utilizadas em ambientes produtivos, com foco em:

- Confiabilidade
- Segurança
- Escalabilidade
- Visibilidade operacional
