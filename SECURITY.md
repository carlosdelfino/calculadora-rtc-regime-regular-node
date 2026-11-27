---
tags:
  - seguranca
  - vulnerabilidade
  - politica
---

![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=Pol%C3%ADtica%20de%20Seguran%C3%A7a&fontSize=36&fontAlignY=35&animation=twinkling)

![visitors](https://visitor-badge.laobi.icu/badge?page_id=RapportTecnologia.calculadora-rtc-regime-regular-node_security)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
![Language: Portuguese](https://img.shields.io/badge/Language-Portuguese-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Ongoing-yellow)
[![GitHub Issues](https://img.shields.io/github/issues/carlosdelfino/calculadora-rtc-regime-regular-node)](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/issues)

# Política de Segurança

## Versões suportadas

| Versão | Suportada |
|---|---|
| 0.1.x (atual) | Sim |
| < 0.1.0 | Não |

Apenas a versão mais recente recebe correções de segurança, conforme o processo
de release descrito em [GOVERNANCE.md](./GOVERNANCE.md).

## Como reportar uma vulnerabilidade

**Não abra issue pública para vulnerabilidades de segurança.** Issues públicas
são inadequadas para relatos que possam expor usuários a riscos antes da
correção.

Reporte pelo canal privado:

- **E-mail**: consultoria@carlosdelfino.eti.br
- **WhatsApp**: +55 (85) 98520-5490

Inclua no relato:

1. Descrição da vulnerabilidade e do impacto potencial;
2. Versão/commit afetado e ambiente (Node.js, SO);
3. Passos para reproduzir ou prova de conceito;
4. Sugestão de mitigação, se houver.

## O que esperar

- **Confirmação de recebimento** em até 3 dias úteis;
- **Avaliação inicial** com classificação de severidade em até 7 dias úteis;
- **Atualizações de progresso** no próprio thread de contato;
- **Divulgação coordenada**: a correção é publicada primeiro; o detalhamento da
  vulnerabilidade ocorre após o release, com crédito ao reportante (se desejado).

## Escopo

São considerados no escopo desta política:

- Falhas na lógica de cálculo tributário que gerem resultados incorretos de
  forma sistemática ou explorável;
- Vulnerabilidades em dependências (informe também via `npm audit`);
- Exposição de dados, segredos ou informações sensíveis;
- Problemas de autenticação, autorização e validação de entrada;
- Qualquer comportamento que permita execução de código ou acesso indevido.

Fora de escopo: issues de usabilidade, bugs sem impacto de segurança e
vulnerabilidades já corrigidas na versão mais recente — use os
[templates de issue](./CONTRIBUTING.md) para esses casos.

## Práticas de segurança do projeto

- Segredos e chaves privadas **nunca** são versionados — use `.env`
  (git-ignorado) e variáveis de ambiente;
- Validação e sanitização de toda entrada externa;
- Mensagens de erro seguras, sem stack traces ou detalhes exploráveis;
- Logs estruturados sem dados sensíveis;
- Menor privilégio em tokens, chaves e integrações.

## Changelog

| Data | Versão | Descrição |
|---|---|---|
| 2026-11-27 | 0.1.0 | Política de segurança inicial |

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&animation=twinkling)
