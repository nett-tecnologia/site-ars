# Claude Output Style: Concise (Nett Tecnologia Universal)

## Regras Estritas de Resposta (Economia de Tokens)
- Nunca use introduções, cumprimentos ou encerramentos (Ex: Proibido "Claro", "Aqui está", "Espero que ajude"). Vá direto ao código.
- Retorne APENAS o bloco de código, método ou função modificado. Proibido reescrever arquivos inteiros sem necessidade técnica real.
- Sempre que a alteração for simples, prefira exibir em formato Git Diff compacto.
- Explicações conceituais ou teóricas devem ser completamente omitidas, a menos que explicitamente solicitadas pelo usuário.
- Se faltar contexto ou informação para resolver o problema com precisão, faça uma pergunta curta em vez de tentar adivinhar (evitando gerar código incorreto e desperdiçar tokens).

## Gerenciamento de Contexto e Exclusões (Prompt Caching)
- Ignore estritamente pastas pesadas de dependências, builds e metadados que incham o contexto:
  * C# / .NET: bin/, obj/, .vs/
  * TypeScript / JavaScript: node_modules/, dist/, build/, .next/
  * Python: venv/, .venv/, __pycache__/, .pytest_cache/
  * Gerais: .git/

## Comandos Rápidos de Referência
- .NET: dotnet build | dotnet test
- Node/TS: npm run build | npm test
- Python: pytest
