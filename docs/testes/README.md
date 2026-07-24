# Testes

## Pirâmide prática

- muitos testes unitários rápidos para regras isoladas;
- testes de integração para banco, filas, HTTP e configuração;
- poucos testes de ponta a ponta para jornadas críticas;
- testes de contrato nas fronteiras entre serviços.

## Estrutura

Use Arrange, Act, Assert:

```text
Arrange: preparar entradas e colaboradores.
Act: executar uma única ação observável.
Assert: verificar resultado e efeitos relevantes.
```

## Qualidade

Um teste confiável deve ser:

- determinístico;
- independente de ordem;
- legível como especificação;
- rápido o suficiente para o nível em que roda;
- explícito sobre relógio, aleatoriedade, rede e concorrência.

## Diagnóstico de teste instável

1. execute isoladamente e em conjunto;
2. repita com uma seed registrada;
3. procure estado global, relógio real e portas fixas;
4. verifique concorrência e timeouts;
5. capture os artefatos mínimos necessários;
6. corrija a causa — não apenas aumente retentativas.

Cobertura ajuda a localizar código não exercitado, mas não mede a qualidade das
asserções nem substitui uma estratégia de risco.
