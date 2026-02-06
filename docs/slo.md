# \# SLO / SLI — Service Level Objectives \& Indicators

# 

# \## Visão Geral

# 

# Esta etapa do projeto teve como objetivo definir SLIs e SLOs claros e realistas, alinhados com práticas de SRE e observabilidade utilizadas no mercado, sem realizar alterações técnicas no cluster Kubernetes.

# 

# O foco foi traduzir métricas e alertas já existentes em objetivos de confiabilidade mensuráveis, conectando operação, monitoramento e impacto no usuário final.

# 

# ---

# 

# \## Serviço Avaliado

# 

# \*\*Nome do serviço\*\*  

# Portfolio Site (aplicação web exposta via Ingress NGINX)

# 

# \*\*Descrição\*\*  

# Aplicação web pública hospedada em Kubernetes (k3s na AWS), acessada via HTTPS, com observabilidade completa utilizando Prometheus, Grafana e Alertmanager.

# 

# \*\*Componentes críticos\*\*

# \- Ingress NGINX

# \- Pods da aplicação

# \- Nodes do cluster

# \- DNS e TLS

# 

# ---

# 

# \## SLIs — Service Level Indicators

# 

# Os SLIs foram definidos com base nas métricas já coletadas pelo Prometheus, sem necessidade de novos exporters ou instrumentação adicional.

# 

# \### Disponibilidade

# 

# \*\*Definição\*\*  

# Percentual de tempo em que o serviço responde com sucesso (HTTP 2xx e 3xx).

# 

# \*\*Métricas base\*\*

# \- Métrica `up`

# \- Métricas HTTP do Ingress NGINX

# 

# \*\*Indicador\*\*

# \- Ingress respondendo corretamente

# \- Pods prontos

# \- Ausência de falhas de roteamento

# 

# ---

# 

# \### Latência

# 

# \*\*Definição\*\*  

# Tempo de resposta percebido pelo usuário final.

# 

# \*\*Métrica base\*\*

# \- Latência p95 do Ingress NGINX

# 

# \*\*Indicador\*\*

# \- Percentil 95 do tempo de resposta das requisições HTTP

# 

# ---

# 

# \### Taxa de Erro

# 

# \*\*Definição\*\*  

# Percentual de requisições que resultam em erro para o usuário.

# 

# \*\*Métrica base\*\*

# \- Respostas HTTP 5xx no Ingress NGINX

# 

# \*\*Indicador\*\*

# \- Proporção de respostas 5xx em relação ao total de requisições

# 

# ---

# 

# \## SLOs — Service Level Objectives

# 

# Os SLOs abaixo foram definidos com foco em realismo operacional, evitando metas irreais para um ambiente de portfólio, mas mantendo alinhamento com padrões profissionais.

# 

# \### Disponibilidade

# 

# \*\*Objetivo\*\*

# \- 99,9% de disponibilidade mensal

# 

# \*\*Impacto\*\*

# \- Até aproximadamente 43 minutos de indisponibilidade por mês são aceitáveis

# 

# ---

# 

# \### Latência

# 

# \*\*Objetivo\*\*

# \- 95% das requisições com latência menor ou igual a 500ms

# 

# \*\*Impacto\*\*

# \- Usuário percebe o serviço como rápido e responsivo

# 

# ---

# 

# \### Taxa de Erro

# 

# \*\*Objetivo\*\*

# \- Menos de 1% de respostas HTTP 5xx

# 

# \*\*Impacto\*\*

# \- Erros ocasionais são toleráveis, desde que não persistentes

# 

# ---

# 

# \## Error Budget

# 

# O Error Budget representa o quanto o serviço pode falhar sem violar os SLOs definidos.

# 

# \### Exemplo — Disponibilidade

# 

# \- SLO: 99,9%

# \- Error Budget: 0,1% do tempo mensal

# \- Aproximadamente 43 minutos por mês

# 

# O error budget é consumido quando:

# \- O serviço fica indisponível

# \- A taxa de erros HTTP 5xx aumenta

# \- A latência ultrapassa os limites definidos

# 

# ---

# 

# \## Relação entre Alertas e SLOs

# 

# Os alertas existentes no projeto foram mapeados diretamente aos SLOs definidos.

# 

# \### Infraestrutura

# 

# | Alerta              | Impacto                         |

# |---------------------|----------------------------------|

# | NodeDown            | Indisponibilidade total          |

# | NodeHighCPU         | Aumento de latência              |

# | NodeHighMemory      | Risco de falhas                  |

# | NodeDiskAlmostFull  | Risco de indisponibilidade       |

# 

# ---

# 

# \### Kubernetes

# 

# | Alerta                     | Impacto                          |

# |----------------------------|-----------------------------------|

# | PodCrashLoopBackOff        | Falha parcial ou total            |

# | PodNotReady                | Redução de capacidade             |

# | DeploymentNoReplicas       | Indisponibilidade                 |

# 

# ---

# 

# \### Ingress

# 

# | Alerta               | Impacto                          |

# |----------------------|-----------------------------------|

# | Ingress5xxHigh       | Violação de taxa de erro          |

# | IngressLatencyHigh   | Violação de latência              |

# | IngressNoTraffic     | Indisponibilidade total           |

# 

# ---

# 

# \## Observações

# 

# \- Nenhum alerta novo foi criado nesta etapa

# \- Nenhuma alteração técnica foi realizada no cluster

# \- Burn rate alerts, alertas baseados em error budget e simulações de falha ficaram como evolução futura

# 

# Esta etapa teve foco exclusivamente conceitual e documental, consolidando a maturidade de observabilidade do projeto.

# 

# ---

# 

# \## Próximos Passos Possíveis

# 

# \- Implementação de burn rate alerts

# \- Alertas baseados em consumo de error budget

# \- Simulação controlada de falhas

# \- Estratégias de auto-remediação

# \- Documentação final de arquitetura e maturidade SRE



