# Projeto Cloud Infra – Kubernetes (k3s) na AWS

Projeto prático de **infraestrutura cloud** com foco em **Kubernetes, containerização, rede, segurança, exposição de serviços e TLS**, desenvolvido para demonstrar **experiência prática real** em ambientes próximos de produção.

---

## 🎯 Objetivo do Projeto

Projetar, implementar e documentar uma **infraestrutura Kubernetes funcional na AWS**, utilizando soluções leves e custo-efetivas, aplicando conceitos reais de:

- Orquestração de containers
- Balanceamento de carga
- Exposição segura de aplicações
- DNS e HTTPS
- Observabilidade de problemas reais de cluster
- Resolução de incidentes comuns em Kubernetes

O projeto foi desenvolvido como **portfólio técnico**, simulando decisões, erros, investigações e soluções encontradas no dia a dia de times de **Infra / Cloud / SRE**.

---

## 🧱 Arquitetura Geral

### Visão Geral

- **Cloud Provider:** AWS  
- **Região:** sa-east-1 (São Paulo)  
- **Cluster Kubernetes:** k3s (lightweight Kubernetes)  
- **Sistema Operacional:** Ubuntu Server  
- **Rede:** VPC padrão AWS  
- **Domínio:** `lucasdeliberal.com.br` (Registro.br + Route 53)  

### Topologia do Cluster

| Função          | Quantidade | Observações |
|-----------------|------------|-------------|
| Control Plane   | 1          | API Server, Scheduler e Controllers |
| Worker Node     | 1          | Execução das aplicações |
| Total de Nodes  | 2          | Preparado para testes de escalabilidade |

---

## 🌐 Exposição da Aplicação

A aplicação é exposta seguindo um **fluxo real de produção**:

1. **Service (ClusterIP)**  
   Comunicação interna entre Pods.

2. **Ingress Controller (NGINX)**  
   Responsável por:
   - Roteamento HTTP/HTTPS
   - Terminação TLS
   - Integração com cert-manager

3. **DNS + Elastic IP (AWS)**
   - Domínio apontando para um **Elastic IP**
   - Evita perda de acesso após reinicialização das instâncias

---

## 🐳 Aplicação

- **Tipo:** Site estático
- **Servidor:** NGINX
- **Containerização:** Docker
- **Imagem:** Build local
- **Objetivo:** Simples por design, foco total na infraestrutura

---

## ☸️ Kubernetes — Detalhes Técnicos

### Recursos Utilizados

- **Deployment**
  - Múltiplas réplicas
  - Distribuição entre nodes
- **Service**
  - Tipo: `ClusterIP`
- **Ingress**
  - Controller: NGINX
  - Host-based routing
  - TLS habilitado
- **IngressClass**
- **cert-manager**
  - Emissão automática de certificados TLS (Let’s Encrypt)

---

## 🔐 Segurança

### AWS

- **Security Groups**
  - SSH restrito por IP
  - Comunicação entre nodes permitida apenas via SG
  - NodePorts abertos somente quando necessário
- **Elastic IP**
  - Evita dependência de IP dinâmico

### Kubernetes

- Comunicação interna via Service
- TLS com certificado válido (HTTPS)
- Nenhum segredo sensível versionado no repositório

---

## 🔒 HTTPS & Certificados

- **Ferramenta:** cert-manager
- **Autoridade Certificadora:** Let’s Encrypt
- **Validação:** HTTP-01
- **Ingress:** NGINX

### Resultado

✅ HTTPS funcional em:  
**https://portfolio.lucasdeliberal.com.br**

---

## 🧪 Problemas Reais Enfrentados e Soluções

Durante a implementação, foram identificados e resolvidos diversos problemas reais, incluindo:

- Conflito entre **Traefik (default do k3s)** e **NGINX Ingress**
- Webhook do ingress-nginx indisponível
- DNS interno do cluster (CoreDNS) inoperante
- Falhas de resolução de serviços internos
- Timeouts na validação ACME (Let’s Encrypt)
- Ajustes manuais de CNI e rede
- Troubleshooting de NodePort, Ingress e LoadBalancer
- Diferença de comportamento entre Node 1 e Node 2

Esses problemas foram tratados com:
- Análise de logs
- Testes internos com Pods utilitários
- Reconfiguração de serviços
- Reinicialização controlada de componentes críticos
- Validação fim a fim (DNS → Ingress → Service → Pod)

---

## 📂 Estrutura do Repositório

```text
docker/
 ├── Dockerfile
 └── index.html

k8s/
 ├── deployment.yaml
 ├── service.yaml
 ├── ingress.yaml
cert-manager/
 └── clusterissuer.yaml

docs/
 └── architecture-v1.md

