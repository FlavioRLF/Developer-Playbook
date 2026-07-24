# Observabilidade

Observabilidade combina sinais que permitem inferir o estado interno de um
sistema a partir de suas saídas.

## Sinais

- **logs:** eventos discretos com contexto;
- **métricas:** séries temporais agregáveis;
- **traces:** caminho de uma requisição entre componentes;
- **profiles:** custo de CPU, memória e outras dimensões ao longo do tempo.

## Logs estruturados

Campos recomendados:

```json
{
  "timestamp": "2026-01-01T12:00:00Z",
  "level": "INFO",
  "service": "example-service",
  "event": "request_completed",
  "trace_id": "example-trace-id",
  "duration_ms": 42,
  "status_code": 200
}
```

Não registre tokens, senhas, payloads pessoais ou cabeçalhos sensíveis.

## Métricas para serviços

Comece pelos "quatro sinais dourados":

- latência;
- tráfego;
- erros;
- saturação.

## Alertas

Um alerta deve indicar impacto, urgência e ação possível. Prefira alertas
baseados em sintomas percebidos pelo usuário ou consumo do orçamento de erro,
em vez de alertar sobre toda variação interna.

## Correlação

Propague identificadores de trace seguindo padrões abertos. Use IDs de
correlação adicionais somente quando houver uma necessidade de domínio clara.
