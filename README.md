![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=Calculadora%20RTC%20—%20Regime%20Regular&fontSize=36&fontAlignY=35&animation=twinkling)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
![Language: Portuguese](https://img.shields.io/badge/Language-Portuguese-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Ongoing-yellow)
![Node](https://img.shields.io/badge/Node.js-%3E%3D18-brightgreen)

# Calculadora RTC — Regime Regular (Node.js)

Calculadora da Reforma Tributária do Consumo (RTC) para o **Regime Regular**,
implementada em Node.js. Projeto da Rapport Tecnologia para a Receita Federal
do Brasil.

> **Origem do projeto:** este repositório é um **port para Node.js** do projeto
> original em Java, mantido em
> [ReceitaFederal/calculadora-rtc-regime-regular](https://github.com/ReceitaFederal/calculadora-rtc-regime-regular).
> A lógica de cálculo, regras de negócio e contratos são portados daquele
> repositório, que permanece a referência de implementação.

## O que é a Reforma Tributária do Consumo

A Reforma Tributária do Consumo (RTC) é a reforma do Sistema Tributário
Nacional instituida pela **Emenda Constitucional nº 132, de 20 de dezembro de
2023**. Ela substitui o atual modelo de tributação sobre o consumo — marcado
por fragmentação, cumulatividade e complexidade — por um Imposto sobre Valor
Agregado (IVA) dual, cobrado sobre o destino e com amplo direito a crédito.

### Tributos extintos e tributos criados

| Tributos extintos | Novos tributos |
|---|---|
| PIS e Cofins (federais) | **CBS** — Contribuição sobre Bens e Serviços (União, administrada pela Receita Federal) |
| ICMS (estadual) e ISS (municipal) | **IBS** — Imposto sobre Bens e Serviços (compartilhado entre Estados, Municípios e DF) |
| IPI (alíquota zero a partir de 2027, exceto ZFM) | **Imposto Seletivo (IS)** — sobre bens e serviços prejudiciais à saúde ou ao meio ambiente |

O IBS é administrado pelo **Comitê Gestor do IBS (CGIBS)**, órgão conjunto dos
entes federativos, que arrecada e distribui a receita ao ente de destino.

### Regime Regular

O **Regime Regular** é a regra geral de incidência do IBS e da CBS: tributação
não cumulativa, ampla e uniforme sobre operações com bens e serviços
(incluindo direitos), com destaque do imposto, direito a crédito amplo e
cobrança no destino. A ele se contrapõem os **regimes diferenciados, específicos
e favorecidos** previstos na LC 214/2025 — por isso esta calculadora implementa
apenas o cálculo da regra geral.

### Cronograma de transição

| Período | O que acontece |
|---|---|
| 2026 | Ano de teste: CBS e IBS com alíquota de referência de 0,9% + 0,1% (compensável com PIS/Cofins) |
| 2027 | CBS e Imposto Seletivo em vigor; PIS/Cofins extintos; IPI zerado (exceto ZFM) |
| 2029–2032 | IBS inicia cobrança com aumento gradual; ICMS e ISS reduzidos na mesma proporção |
| 2033 | ICMS e ISS extintos; novo sistema em pleno vigor |

### Legislação de referência

| Norma | Data | O que faz |
|---|---|---|
| [EC 132/2023](https://www.planalto.gov.br/ccivil_03/constituicao/emendas/emc/emc132.htm) | 20/12/2023 | Reforma constitucional: cria IBS, CBS e IS; define extinções e transição |
| [LC 214/2025](https://www.planalto.gov.br/ccivil_03/leis/lcp/lcp214.htm) | 16/01/2025 | Institui IBS, CBS e Imposto Seletivo: incidência, cesta básica, cashback, regimes e transição |
| [LC 227/2026](https://www.planalto.gov.br/ccivil_03/leis/lcp/lcp227.htm) | 13/01/2026 | Institui o Comitê Gestor do IBS (CGIBS) e o processo administrativo do IBS |
| Decreto nº 12.955/2026 | 29/04/2026 | Regulamenta a LC 214/2025 |

Referências institucionais:
[Ministério da Fazenda — Reforma Tributária](https://www.gov.br/fazenda/pt-br/acesso-a-informacao/acoes-e-programas/reforma-tributaria) ·
[PGFN — Por dentro da Reforma Tributária do Consumo](https://www.gov.br/pgfn/pt-br/cidadania-tributaria/por-dentro-da-reforma-tributaria-do-consumo)

## Requisitos

- Node.js >= 18

## Uso

```bash
npm start
```

## Convenções

Este projeto adota convenções obrigatórias para commits e branches.
Consulte [CONVENCIONAL.md](./CONVENCIONAL.md):

- **Commits:** [Conventional Commits v1.0.0-beta.4](https://www.conventionalcommits.org/pt-br/v1.0.0-beta.4/)
- **Branches:** [Conventional Branch v1.1.0](https://conventionalbranch.org/pt-br/)

## Documentos do projeto

| Documento | Conteúdo |
|---|---|
| [GOVERNANCE.md](./GOVERNANCE.md) | Papéis, versionamento SemVer e processo decisório |
| [CONTRIBUTING.md](./CONTRIBUTING.md) | Guia de contribuição e boas práticas de GitHub Issues |
| [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) | Código de Conduta (Contributor Covenant 2.1) |
| [SECURITY.md](./SECURITY.md) | Política de segurança e canal privado de reporte |
| [CHANGELOG.md](./CHANGELOG.md) | Histórico de versões (Keep a Changelog) |
| [LICENSE](./LICENSE) | Licença MIT |

## Fluxo de trabalho Git

1. Abra uma issue descrevendo o que será implementado e o problema relacionado;
2. Crie uma branch convencional (`feature/`, `fix/`, `chore/`, ...);
3. Faça commits no formato Conventional Commits referenciando a issue;
4. Comente na issue explicando o que foi feito e por quê;
5. Finalize a issue após o merge.

## Autor

Carlos Delfino — <consultoria@carlosdelfino.eti.br>
WhatsApp: +55 (85) 98520-5490

## Changelog

| Data | Versão | Descrição |
|---|---|---|
| 2026-11-27 | 0.1.0 | Inicialização do projeto e convenções Git |
| 2026-11-27 | 0.1.1 | Adicionada seção sobre a Reforma Tributária do Consumo com legislação de referência |
| 2026-11-27 | 0.1.2 | Documentada origem como port Node.js do projeto Java da Receita Federal |
| 2026-11-27 | 0.1.3 | Adicionados GOVERNANCE, CHANGELOG, LICENSE (MIT), Código de Conduta e Política de Segurança |

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&animation=twinkling)
