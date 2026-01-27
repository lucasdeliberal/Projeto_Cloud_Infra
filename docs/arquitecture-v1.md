# Arquitetura – Projeto Cloud Infra (v1)

## Visão Geral

Este projeto implementa uma aplicação containerizada rodando em Kubernetes (k3s) na AWS,
com exposição segura via Ingress NGINX, DNS público e HTTPS com Let’s Encrypt.

---

## Componentes

### Cloud Provider
- AWS (VPC padrão)
- Elastic IP para acesso externo estável
- Security Groups controlando SSH, HTTP e HTTPS

### Kubernetes
- Distribuição: k3s
- Nodes:
  - 1 Control Plane
  - 1 Worker
- CNI: padrão do k3s
- DNS interno: CoreDNS

### Exposição
- Service: ClusterIP
- Ingress Controller: NGINX
- Ingress: Host-based routing
- TLS: cert-manager + Let’s Encrypt

---

## Fluxo de Requisição

1. Cliente acessa `https://portfolio.lucasdeliberal.com.br`
2. DNS resolve para Elastic IP do Worker
3. Ingress NGINX recebe a requisição
4. TLS é terminado no Ingress
5. Requisição encaminhada ao Service
6. Service direciona para um Pod ativo

---

## Pontos Críticos Resolvidos

- Conflito entre Traefik (default do k3s) e NGINX
- DNS interno inconsistente (CoreDNS)
- Webhooks do ingress-nginx
- Validação ACME (HTTP-01)
- Conectividade interna entre Pods e Services

---

## Estado Atual

✔ Aplicação funcional  
✔ HTTPS válido  
✔ DNS público configurado  
✔ Arquitetura documentada  

---

## Próximas Evoluções

- CI/CD com GitHub Actions
- Helm Charts
- Monitoramento com Prometheus e Grafana
- Gerenciamento com Rancher
