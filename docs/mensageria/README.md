# Mensageria

## Conceitos essenciais

- **at-most-once:** pode perder mensagens, mas não repete a entrega;
- **at-least-once:** evita perda ao custo de possíveis duplicatas;
- **effectively-once:** efeitos duplicados são impedidos por idempotência e
  controle transacional;
- **ordenação:** normalmente é garantida somente dentro de uma partição ou
  chave;
- **backpressure:** consumidores precisam limitar trabalho conforme a
  capacidade disponível.

## Consumidor idempotente

Uma estratégia comum:

1. atribuir um identificador estável ao evento;
2. iniciar uma transação;
3. registrar o identificador processado com restrição de unicidade;
4. aplicar a mudança de domínio;
5. confirmar a transação;
6. reconhecer a mensagem conforme a semântica do broker.

## Retentativas

Use atraso exponencial com jitter e limite de tentativas. Separe:

- falhas transitórias, que podem ser tentadas novamente;
- falhas permanentes, que exigem correção ou descarte controlado;
- mensagens envenenadas, que devem ir para uma DLQ com contexto suficiente para
  análise, sem expor dados sensíveis.

## Checklist de diagnóstico

- lag por consumidor ou partição;
- taxa de publicação, consumo, erro e retentativa;
- idade da mensagem mais antiga;
- rebalanceamentos;
- tempo de processamento e timeouts;
- capacidade da DLQ;
- compatibilidade de schema;
- correlação entre mensagem e trace.
