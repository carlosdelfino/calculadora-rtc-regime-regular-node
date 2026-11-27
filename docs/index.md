---
layout: page
title: Calculadora RTC — Regime Regular
description: Calculadora da Reforma Tributária do Consumo para o Regime Regular — port Node.js do projeto Java da Receita Federal.
---

## Sobre o projeto

**Calculadora da Reforma Tributária do Consumo (RTC)** para o **Regime
Regular**, implementada em **Node.js 22**.

Este monorepo é um **port para Node.js** do projeto original em Java mantido
pela Receita Federal do Brasil e o SERPRO:
[ReceitaFederal/calculadora-rtc-regime-regular](https://github.com/ReceitaFederal/calculadora-rtc-regime-regular).

## A Reforma Tributária do Consumo

Instituída pela **EC 132/2023**, a RTC substitui PIS/Cofins, ICMS e ISS por um
IVA dual cobrado no destino:

| Tributos extintos | Novos tributos |
|---|---|
| PIS / Cofins | **CBS** — União (Receita Federal) |
| ICMS + ISS | **IBS** — Estados, DF e Municípios (via CGIBS) |
| IPI (zerado em 2027) | **Imposto Seletivo** — bens prejudiciais |

O **Regime Regular** é a regra geral de incidência: tributação não cumulativa,
ampla e uniforme, com direito a crédito pleno e cobrança no destino.

### Legislação

- [EC 132/2023](https://www.planalto.gov.br/ccivil_03/constituicao/emendas/emc/emc132.htm) — reforma constitucional
- [LC 214/2025](https://www.planalto.gov.br/ccivil_03/leis/lcp/lcp214.htm) — institui IBS, CBS e IS
- [LC 227/2026](https://www.planalto.gov.br/ccivil_03/leis/lcp/lcp227.htm) — Comitê Gestor do IBS

## Componentes

| Componente | Repositório | Stack |
|---|---|---|
| **Backend** | [node-backend](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node-backend) | Node.js 22 — API do cálculo |
| **Frontend** | [node-frontend](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node-frontend) | Vite + TypeScript + React Router + Redux Toolkit + Refine |

## Documentação

- [README](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/blob/main/README.md) — visão geral e uso
- [GOVERNANCE](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/blob/main/GOVERNANCE.md) — papéis e processo decisório
- [CONTRIBUTING](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/blob/main/CONTRIBUTING.md) — como contribuir
- [CONVENCIONAL](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/blob/main/CONVENCIONAL.md) — commits e branches
- [SECURITY](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/blob/main/SECURITY.md) — política de segurança
- [CHANGELOG](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/blob/main/CHANGELOG.md) — histórico de versões

## Autor

**Carlos Delfino** — <consultoria@carlosdelfino.eti.br> ·
[Rapport Tecnologia](https://rapport.tec.br)
