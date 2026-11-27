---
layout: page
title: Calculadora RTC — Regime Regular
description: Calculadora da Reforma Tributária do Consumo para o Regime Regular — port Node.js do projeto Java da Receita Federal.
image: /images/illustrations/rtc-calculo.jpg
---

<figure class="rtc-visual rtc-visual--hero">
  <picture>
    <source type="image/webp" srcset="{{ '/images/illustrations/rtc-calculo-768.webp' | relative_url }} 768w, {{ '/images/illustrations/rtc-calculo.webp' | relative_url }} 1536w" sizes="(min-width: 1200px) 730px, (min-width: 768px) 65vw, calc(100vw - 30px)">
    <img src="{{ '/images/illustrations/rtc-calculo.jpg' | relative_url }}" width="1536" height="1024" alt="Calculadora azul com teclas verdes, documento e blocos representando o cálculo tributário digital." fetchpriority="high" decoding="async">
  </picture>
  <figcaption>Tecnologia aberta para o cálculo da Reforma Tributária do Consumo.</figcaption>
</figure>

## Sobre o projeto

**Calculadora da Reforma Tributária do Consumo (RTC)** para o **Regime
Regular**, implementada em **Node.js 22**.

Este monorepo é um **port para Node.js** do projeto original em Java mantido
pela Receita Federal do Brasil e o SERPRO:
[ReceitaFederal/calculadora-rtc-regime-regular](https://github.com/ReceitaFederal/calculadora-rtc-regime-regular).

## A Reforma Tributária do Consumo

<figure class="rtc-tax-visual">
  <picture>
    <source media="(max-width: 575px)" srcset="{{ '/images/illustrations/tributos-rtc-mobile.svg' | relative_url }}" width="480" height="300">
    <img src="{{ '/images/illustrations/tributos-rtc.svg' | relative_url }}" width="960" height="240" alt="Três tributos contemplados pela calculadora: IBS, CBS e Imposto Seletivo." loading="lazy" decoding="async">
  </picture>
</figure>

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

<figure class="rtc-visual rtc-visual--components">
  <picture>
    <source type="image/webp" srcset="{{ '/images/illustrations/rtc-componentes-768.webp' | relative_url }} 768w, {{ '/images/illustrations/rtc-componentes.webp' | relative_url }} 1536w" sizes="(min-width: 992px) 620px, (min-width: 768px) 65vw, calc(100vw - 30px)">
    <img src="{{ '/images/illustrations/rtc-componentes.jpg' | relative_url }}" width="1536" height="1024" alt="Interface web conectada a uma calculadora e a módulos de servidor, representando a integração entre frontend e backend." loading="lazy" decoding="async">
  </picture>
  <figcaption>Frontend e backend conectados pelo cálculo.</figcaption>
</figure>

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
