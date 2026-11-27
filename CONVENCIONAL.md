---
tags:
  - git
  - convencoes
  - conventional-commits
  - conventional-branch
---

![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=Conven%C3%A7%C3%B5es%20Git&fontSize=36&fontAlignY=35&animation=twinkling)

![visitors](https://visitor-badge.laobi.icu/badge?page_id=RapportTecnologia.calculadora-rtc-regime-regular-node_convencional)
[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC_BY--SA_4.0-blue.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
![Language: Portuguese](https://img.shields.io/badge/Language-Portuguese-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Ongoing-yellow)
[![GitHub Issues](https://img.shields.io/github/issues/RapportTecnologia/AgenticSpace)](https://github.com/RapportTecnologia/AgenticSpace/issues)

# Convenções de Commits e Branches

Este documento define as convenções obrigatórias para mensagens de commit e
nomes de branches neste repositório, baseadas em:

- **[Conventional Commits v1.0.0-beta.4](https://www.conventionalcommits.org/pt-br/v1.0.0-beta.4/)** — mensagens de commit;
- **[Conventional Branch v1.1.0](https://conventionalbranch.org/pt-br/)** — nomenclatura de branches.

---

## 1. Conventional Commits — Mensagens de Commit

A especificação Conventional Commits define regras para criar um histórico de
commits explícito, legível por humanos e máquinas, e compatível com
[Versionamento Semântico (SemVer)](https://semver.org/lang/pt-BR/).

### Estrutura

```text
<tipo>[escopo opcional]: <descrição>

[corpo opcional]

[rodapé opcional]
```

### Elementos

| Elemento | Obrigatório | Descrição |
|---|---|---|
| `tipo` | Sim | Substantivo que identifica a natureza do commit (`feat`, `fix`, etc.). |
| `escopo` | Não | Substantivo entre parênteses indicando a seção do código, ex.: `feat(parser):`. |
| `descrição` | Sim | Resumo curto das alterações, após `: `. |
| `corpo` | Não | Contexto adicional; começa uma linha em branco após a descrição. |
| `rodapé` | Não | Metadados (issues, BREAKING CHANGE, revisores); um item por linha. |

### Tipos principais

| Tipo | Uso | SemVer |
|---|---|---|
| `fix` | Correção de bug | `PATCH` |
| `feat` | Nova funcionalidade | `MINOR` |
| `BREAKING CHANGE` | Quebra de compatibilidade da API (no corpo ou rodapé) | `MAJOR` |

### Tipos adicionais recomendados

Baseados na [Convenção do Angular](https://github.com/angular/angular/blob/main/CONTRIBUTING.md)
(via `@commitlint/config-conventional`):

| Tipo | Uso |
|---|---|
| `chore` | Tarefas de manutenção sem impacto no código de produção |
| `docs` | Apenas documentação |
| `style` | Formatação (espaços, ponto-e-vírgula), sem alteração de lógica |
| `refactor` | Alteração de código que não corrige bug nem adiciona funcionalidade |
| `perf` | Melhoria de performance |
| `test` | Adição ou correção de testes |
| `build` | Sistema de build ou dependências externas |
| `ci` | Configuração de integração contínua |
| `revert` | Reversão de commit anterior |
| `improvement` | Melhoria de implementação existente (sem novo recurso nem bugfix) |

> Estes tipos não são obrigatórios pela especificação e não têm efeito
> implícito no versionamento semântico, salvo quando incluem
> `BREAKING CHANGE`.

### Quebra de compatibilidade (BREAKING CHANGE)

Uma modificação que quebra a compatibilidade DEVE ser indicada de duas formas:

1. `BREAKING CHANGE:` (sempre em maiúsculas) no início do corpo ou em uma linha
   do rodapé, seguido de `: ` e a descrição do que mudou na API;
2. Opcionalmente, um `!` antes dos dois-pontos no prefixo tipo/escopo para
   chamar atenção: `feat!:`, `fix(api)!:`.

### Regras resumidas

1. A mensagem DEVE começar com um tipo, seguido de escopo OPCIONAL e
   OBRIGATORIAMENTE `: ` (dois-pontos + espaço).
2. A descrição DEVE existir e resumir a mudança.
3. O corpo PODE ser fornecido após uma linha em branco.
4. O rodapé PODE seguir após uma linha em branco, um item por linha.
5. Tipos e escopos NÃO são sensíveis a maiúsculas/minúsculas, exceto
   `BREAKING CHANGE`, que DEVE ser maiúsculo.
6. Prefira um tipo por commit; se o commit abrange vários tipos, quebre-o em
   commits menores.

### Exemplos

```text
feat(calculo): adiciona cálculo de CBS e IBS no regime regular
```

```text
fix: corrige arredondamento de alíquota efetiva

O arredondamento utilizava duas casas decimais quando a legislação
exige quatro, gerando divergência nos relatórios.

closes issue #12
```

```text
feat!: migra configuração para variáveis de ambiente

BREAKING CHANGE: a chave `extends`, no arquivo de configuração, agora é
utilizada para estender outro arquivo de configuração
```

```text
docs: corrige ortografia do CHANGELOG
```

```text
chore(deps): atualiza express para 4.19.2
```

### Referência a issues

Todo commit relacionado a uma issue aberta DEVE referenciá-la no rodapé, por
exemplo:

```text
closes issue #1
refs issue #42
```

### Por que usar?

- Geração automatizada de CHANGELOGs;
- Determinação automática de versionamento semântico;
- Comunicação clara da natureza das mudanças para equipe e público;
- Disparo de pipelines de build e deploy;
- Histórico estruturado que facilita contribuições.

---

## 2. Conventional Branch — Nomes de Branches

A especificação Conventional Branch padroniza a nomeação de branches para
torná-los legíveis, acionáveis e úteis para automação de CI/CD.

### Estrutura

```text
<tipo>/<descrição>
```

Branches tronco (`main`, `master`, `develop`) não usam prefixo.

### Prefixos de propósito

| Prefixo | Uso | Exemplo |
|---|---|---|
| `feature/` ou `feat/` | Novas funcionalidades | `feature/add-login-page` |
| `bugfix/` ou `fix/` | Correções de bugs | `bugfix/fix-header-bug` |
| `hotfix/` | Correções urgentes em produção | `hotfix/security-patch` |
| `release/` | Preparação de versão | `release/v1.2.0` |
| `chore/` | Tarefas sem alteração de código (deps, docs) | `chore/update-dependencies` |

### Regras básicas

1. **Caracteres permitidos**: a descrição DEVE usar apenas letras minúsculas
   (`a-z`), números (`0-9`), hífens (`-`) e pontos (`.`). NÃO DEVE conter
   maiúsculas, caracteres especiais, underlines ou espaços.
2. **Sem hífens/pontos consecutivos, iniciais ou finais**: inválido
   `feature/novo--login`, `feature/-login`, `release/v1.2.0.`.
3. **Claro e conciso**: o nome DEVERIA descrever o propósito do trabalho.
4. **Número do ticket**: quando houver issue vinculada, a descrição DEVERIA
   incluir seu número em minúsculas, ex.: `feature/issue-123-novo-login`.

### Exemplos válidos e inválidos

| Nome | Válido | Notas |
|---|:---:|---|
| `main` | Sim | Branch tronco |
| `feature/add-login-page` | Sim | Nova funcionalidade |
| `feat/add-login-page` | Sim | Alias curto de `feature/` |
| `fix/header-bug` | Sim | Alias curto de `bugfix/` |
| `hotfix/security-patch` | Sim | Correção urgente |
| `release/v1.2.0` | Sim | Versão com pontos permitidos |
| `chore/update-dependencies` | Sim | Tarefa de manutenção |
| `feature/issue-123-novo-login` | Sim | Com referência de ticket |
| `feature/Add_Login` | Não | Maiúsculas e underline |
| `feature/novo--login` | Não | Hífens consecutivos |
| `feature/-novo-login` | Não | Hífen inicial |

### Uso combinado

- Crie uma branch `feature/issue-N-descricao` para cada issue;
- Faça commits Conventional Commits na branch;
- Abra PR para a branch tronco referenciando a issue (`closes #N`).

---

## Changelog

| Data | Versão | Descrição |
|---|---|---|
| 2026-11-27 | 0.1.0 | Documentação inicial das convenções de commits e branches |

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&animation=twinkling)
