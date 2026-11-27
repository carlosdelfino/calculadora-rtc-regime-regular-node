---
tags:
  - contribuicao
  - github-issues
  - boas-praticas
---

![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=Guia%20de%20Contribui%C3%A7%C3%A3o&fontSize=36&fontAlignY=35&animation=twinkling)

![visitors](https://visitor-badge.laobi.icu/badge?page_id=RapportTecnologia.calculadora-rtc-regime-regular-node_contributing)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
![Language: Portuguese](https://img.shields.io/badge/Language-Portuguese-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Ongoing-yellow)
[![GitHub Issues](https://img.shields.io/github/issues/carlosdelfino/calculadora-rtc-regime-regular-node)](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/issues)

# Guia de Contribuição

Este documento orienta colaboradores sobre como trabalhar com **GitHub Issues**,
**Pull Requests** e convenções do projeto. Baseado nas boas práticas do artigo
[Mastering GitHub Issues: Best Practices and Pro Tips](https://gitprotect.io/blog/mastering-github-issues-best-practices-and-pro-tips/).

## Fluxo de trabalho obrigatório

Todo trabalho neste repositório segue este ciclo:

1. **Abra uma issue** descrevendo o que será implementado e qual problema está
   relacionado;
2. **Crie uma branch convencional** a partir da `main` (ver
   [CONVENCIONAL.md](./CONVENCIONAL.md));
3. **Faça as alterações** com commits no formato Conventional Commits;
4. **Referencie a issue nos commits** (`refs issue #N` ou `closes issue #N`);
5. **Abra o Pull Request** usando o template, vinculando a issue;
6. **Comente na issue** explicando o que foi feito e por quê das escolhas;
7. **Finalize a issue** após o merge.

---

## 1. Antes de abrir uma issue

**Pesquise primeiro.** O GitHub não sugere duplicatas automaticamente — antes de
criar uma issue nova:

- Busque nas [issues abertas e fechadas](../../issues?q=is%3Aissue) por termos
  relacionados ao seu problema;
- Se já existe uma issue sobre o assunto, **vote nela (👍) ou comente** com
  informações adicionais em vez de duplicar;
- Votos e comentários ajudam a equipe a priorizar o trabalho.

## 2. Escolhendo o template correto

Ao abrir uma issue, selecione o template adequado:

| Template | Quando usar |
|---|---|
| **Relatório de Bug** | Comportamento incorreto, erros, falhas, regressões |
| **Novo Recurso** | Funcionalidade que ainda não existe |
| **Dúvida** | Perguntas sobre uso, configuração ou comportamento |
| **Sugestão** | Melhorias de processo, documentação, arquitetura ou ideias gerais |

> **Vulnerabilidades de segurança NÃO devem ser reportadas em issues públicas.**
> Siga o canal privado descrito em [SECURITY.md](./SECURITY.md).

## 3. Títulos descritivos e objetivos claros

- Use títulos que identifiquem o problema rapidamente:
  - Ruim: `Erro na calculadora`
  - Bom: `Cálculo de CBS retorna NaN quando base é zero`
- Descreva o objetivo e o contexto no corpo, preenchendo **todos os campos do
  template** — informações incompletas atrasam a triagem.

## 4. Durante a vida da issue

- **Documente o progresso em comentários**: atualizações regulares mantêm todos
  informados e criam histórico das decisões;
- **Use menções com propósito**: `@usuario` envia notificação — mencione apenas
  quem precisa agir ou opinar;
- **Vincule trabalhos relacionados**: referencie outras issues e PRs com `#N`
  para manter a rastreabilidade;
- **Evite discussões longas demais**: se a conversa sair do escopo, abra uma
  discussão ou issue separada.

## 5. Atribuição (assignees)

Colaboradores externos **não devem se auto-atribuir** nem atribuir issues a
outros. O fluxo é:

1. A equipe revisa issues novas regularmente;
2. O mantenedor atribui a issue ao desenvolvedor mais adequado (por expertise e
   carga de trabalho);
3. O reportante é mantido informado sobre quem está tratando a issue e
   expectativas de prazo;
4. O responsável atualiza a issue com progresso e resolução.

## 6. Labels

Labels categorizam e sinalizam o estado das issues. Use com moderação — excesso
de labels gera poluição visual.

| Prefixo | Finalidade | Exemplos |
|---|---|---|
| `type:` | Natureza da issue | `type: bug`, `type: feature`, `type: docs` |
| `state:` | Estado do fluxo | `state: to triage`, `state: in progress`, `state: needs info` |
| `priority:` | Urgência | `priority: high`, `priority: low` |
| especiais | Convite à comunidade | `good first issue`, `help wanted` |

- `state: to triage` marca issues aguardando avaliação inicial;
- `state: needs info` sinaliza que faltam detalhes do reportante;
- `good first issue` e `help wanted` convidam contribuições da comunidade.

## 7. Fechando issues corretamente

- **Nunca deixe issues resolvidas abertas** — isso polui o tracker e
  desinforma;
- Feche via sintaxe especial em commits ou PRs: `closes #N`, `fixes #N`,
  `resolves #N` — a issue fecha automaticamente ao mergear na `main`;
- Ao fechar, **registre um resumo de encerramento**: o que foi feito, por quê,
  e links para documentação ou resultados relevantes;
- Confirme que a issue está genuinamente resolvida e que ações de follow-up
  estão documentadas nos comentários.

## 8. Pull Requests

- Todo PR deve **vincular a issue correspondente** (`closes #N` na descrição);
- Preencha o template de PR: resumo, mudanças, checklist de testes e
  documentação;
- Commits devem seguir [Conventional Commits](./CONVENCIONAL.md);
- Branches devem seguir [Conventional Branch](./CONVENCIONAL.md);
- Mantenha PRs pequenos e focados — um propósito por PR.

## 9. Boas práticas gerais

- **Task lists** em issues grandes quebram o trabalho em entregas menores;
- **Milestones** agrupam issues por release;
- **Cross-linking** de issues relacionadas facilita rastrear dependências;
- Trate issues como canal oficial de decisões — o que foi decidido deve estar
  registrado na issue, não apenas em conversas externas.

---

## Changelog

| Data | Versão | Descrição |
|---|---|---|
| 2026-11-27 | 0.1.0 | Guia inicial de contribuição baseado nas boas práticas de GitHub Issues |

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&animation=twinkling)
