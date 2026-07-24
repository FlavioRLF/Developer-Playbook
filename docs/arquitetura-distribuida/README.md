# Arquitetura de sistemas distribuídos

## Princípios

- falhas parciais são normais;
- rede tem latência, limites e interrupções;
- relógios não são perfeitamente sincronizados;
- mensagens podem atrasar, duplicar ou chegar fora de ordem;
- consistência, disponibilidade e custo exigem escolhas explícitas;
- operação e evolução fazem parte do desenho.

## Padrões de resiliência

| Padrão | Objetivo | Cuidado |
| --- | --- | --- |
| Timeout | Limitar espera | Deve caber no orçamento de latência |
| Retry | Superar falha transitória | Use backoff, jitter e limite |
| Circuit breaker | Evitar pressão sobre dependência falha | Defina recuperação e observabilidade |
| Bulkhead | Isolar recursos | Evite partições rígidas demais |
| Idempotência | Tornar repetição segura | Exige chave e janela bem definidas |
| Load shedding | Preservar o núcleo sob saturação | Priorize tráfego explicitamente |

## Orçamento de tempo

O timeout do chamador deve ser maior que a soma dos orçamentos internos, mas
cada dependência precisa de um limite menor que o tempo restante. Retentativas
devem respeitar o deadline original.

## Consistência

Antes de escolher uma solução, documente:

- qual invariante precisa ser preservado;
- quando o dado pode ficar temporariamente desatualizado;
- como conflitos são detectados e resolvidos;
- como uma operação incompleta é retomada ou compensada;
- qual é a fonte de verdade;
- como o estado é reconstruído e auditado.

## Checklist de revisão

- limites e propriedade dos dados;
- contratos e compatibilidade;
- timeouts, retries e idempotência;
- capacidade, filas e backpressure;
- segurança entre serviços;
- logs, métricas, traces e SLOs;
- deploy, rollback e migração;
- recuperação de desastre;
- custo operacional e simplicidade.
