# SLO / SLI – Portfolio Web Service

## Descrição do Serviço

Serviço web estático exposto via Kubernetes Ingress (ingress-nginx),
com observabilidade baseada em Prometheus.
O serviço é consumido diretamente por usuários finais via navegador.

## SLIs (Service Level Indicators)

### Disponibilidade
- Indicador: requisições HTTP recebidas pelo Ingress
- Métrica: nginx_ingress_controller_requests

### Latência
- Indicador: tempo de resposta das requisições
- Métrica: p95 da duração das requisições HTTP

### Taxa de erro
- Indicador: proporção de respostas HTTP 5xx
- Métrica: nginx_ingress_controller_requests com status 5xx

## SLOs (Service Level Objectives)

### Disponibilidade
- Objetivo: 99.9% mensal
- Downtime máximo permitido: ~43 minutos/mês

### Latência
- Objetivo: 95% das requisições com latência ≤ 1 segundo
- Métrica: p95

### Taxa de erro
- Objetivo: ≤ 1% de respostas HTTP 5xx

## Error Budget

O serviço possui um orçamento de erro de 0.1% mensal para disponibilidade.
Enquanto o consumo do error budget estiver dentro do limite,
mudanças e deploys podem ocorrer normalmente.

## Relação entre Alertas e SLOs

Alertas críticos indicam possível violação imediata de SLO
e consumo acelerado do error budget.

Alertas de warning indicam degradação ou tendência de falha,
permitindo ação preventiva antes de impacto ao usuário final.
