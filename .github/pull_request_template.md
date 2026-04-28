## Pull Request Checklist

## Resumo

- 

## Tipo de alteração

- [ ] Bugfix
- [ ] Feature
- [ ] Enhancement
- [ ] Refactor
- [ ] Documentation
- [ ] Workflow / automation
- [ ] Security
- [ ] Dependency / Poetry lockfile

## Validação obrigatória

- [ ] `poetry check`
- [ ] `pytest`
- [ ] Alterações são mínimas, focadas e relacionadas ao objetivo do PR
- [ ] Documentação relevante foi atualizada

## Regras para Poetry / dependências

- [ ] `pyproject.toml` foi revisado quando houve alteração de constraints
- [ ] `poetry.lock` foi regenerado de forma única e coerente
- [ ] Não há múltiplas atualizações conflitantes de lockfile sendo mescladas individualmente
- [ ] PRs Dependabot com `mergeable=false` não foram mescladas individualmente
- [ ] Atualizações de segurança conflitantes foram consolidadas conforme `DEPENDENCY_SECURITY_UPDATE_PLAN.md`

## Segurança e dados

- [ ] Não há credenciais reais, tokens, API keys, private keys ou senhas no commit
- [ ] `.env.example` contém apenas placeholders
- [ ] Alterações em autenticação/autorização foram revisadas
- [ ] Alterações em datastore/vector DB foram revisadas
- [ ] Alterações em upload/processamento de arquivos foram revisadas
- [ ] Logs não expõem documentos privados, tokens ou dados sensíveis
- [ ] Integrações OpenAI/vector DB não introduzem vazamento de dados

## Risco operacional

- [ ] Sem impacto em endpoints públicos
- [ ] Sem impacto em autenticação
- [ ] Sem impacto em dados/documentos privados
- [ ] Sem impacto em compatibilidade de datastore

## Issue relacionada

Fixes/Closes: 

## Observações

- 

## Branch naming convention

Use:

```text
<type>/<short-description>-<issue-number>
```

Examples:

```text
feature/advanced-chunking-strategy-123
bugfix/datastore-query-filter-456
```
