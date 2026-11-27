---
tags:
  - governanca
  - semver
  - processo-decisorio
---

![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=Governan%C3%A7a%20do%20Projeto&fontSize=36&fontAlignY=35&animation=twinkling)

![visitors](https://visitor-badge.laobi.icu/badge?page_id=RapportTecnologia.calculadora-rtc-regime-regular-node_governance)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
![Language: Portuguese](https://img.shields.io/badge/Language-Portuguese-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Ongoing-yellow)
[![GitHub Issues](https://img.shields.io/github/issues/carlosdelfino/calculadora-rtc-regime-regular-node)](https://github.com/carlosdelfino/calculadora-rtc-regime-regular-node/issues)

# Governança do Projeto

## 1. Objetivo

Este documento define as regras de governança da **Calculadora RTC — Regime
Regular (Node.js)**, port em Node.js do projeto de código aberto mantido pela
Receita Federal do Brasil (RFB) e desenvolvido em parceria com o SERPRO
([repositório original](https://github.com/ReceitaFederal/calculadora-rtc-regime-regular)).
O objetivo é garantir a qualidade, rastreabilidade e sustentabilidade do
projeto, definindo papéis, responsabilidades e processos de decisão.

## 2. Papéis e Responsabilidades

| Perfil            | Responsabilidade                                                                  | Instituição  |
|-------------------|-----------------------------------------------------------------------------------|--------------|
| **Administrador** | Gestão de permissões, criação de repositórios, auditoria de acessos               | RFB          |
| **Líder Técnico** | Decisões estratégicas, aprovação de mudanças arquiteturais, alinhamento institucional | RFB       |
| **Mantenedor**    | Revisão de código (code review), gestão de issues, garantia da qualidade e segurança | RFB / SERPRO |
| **Desenvolvedor** | Desenvolvimento de funcionalidades, correção de bugs, escrita de testes           | RFB / SERPRO |
| **Leitor**        | Leitura do código-fonte, abertura de Issues e participação em Discussions         | Externo      |

## 3. Versionamento

O projeto adota **Semantic Versioning (SemVer)** com a estrutura `MAJOR.MINOR.PATCH`:

- **MAJOR**: mudanças incompatíveis com versões anteriores da API;
- **MINOR**: novas funcionalidades retrocompatíveis;
- **PATCH**: correções de bugs retrocompatíveis.

O versionamento é derivado dos [Conventional Commits](./CONVENCIONAL.md)
(`fix` → PATCH, `feat` → MINOR, `BREAKING CHANGE` → MAJOR) e todas as versões
são registradas no [CHANGELOG.md](./CHANGELOG.md).

## 4. Processo Decisório

### 4.1 Mudanças de Rotina

Mudanças de rotina incluem correções de bugs, atualizações de tabelas
tributárias e melhorias incrementais sem impacto arquitetural. O processo é:

1. Abertura de issue descrevendo a necessidade e referência normativa (quando aplicável);
2. Avaliação interna pela equipe da RFB;
3. Se aprovada, incorporadas por meio dos processos internos de desenvolvimento;
4. Validação automática por pipeline de integração contínua internos.

### 4.2 Mudanças Arquiteturais

Mudanças que impactam a arquitetura, contratos de API ou estrutura de dados
exigem:

1. Elaboração de Architecture Decision Record (ADR) em `docs/`;
2. Revisão e aprovação pelo Líder Técnico e Mantenedores;
3. Validação de conformidade com as normas da Reforma Tributária sobre o Consumo;
4. Registro no CHANGELOG.md e atualização do ROADMAP.md quando aplicável.

### 4.3 Publicação de Novas Versões (Release)

O processo de publicação de novas versões segue:

1. Atualização do `package.json` com a nova versão SemVer;
2. Atualização do `CHANGELOG.md` com todas as alterações da versão;
3. Criação de tag Git com o número da versão (`vMAJOR.MINOR.PATCH`);
4. Publicação de release no repositório com as notas de versão.

### 4.4 Paridade com a implementação Java

Por ser um port, mudanças de regra de cálculo ou contratos devem manter
paridade com o [projeto original em Java](https://github.com/ReceitaFederal/calculadora-rtc-regime-regular).
Divergências intencionais devem ser justificadas em ADR.

## 5. Canais de Comunicação

- **Issues**: para relato de bugs e sugestões de melhoria técnica, examinadas pela equipe definida pela área de negócio da RFB;
- **Discussions**: para debate de propostas e esclarecimentos, examinadas pela equipe definida pela área de negócio da RFB;
- **Segurança**: vulnerabilidades seguem o canal privado descrito em [SECURITY.md](./SECURITY.md).

## Changelog

| Data | Versão | Descrição |
|---|---|---|
| 2026-11-27 | 0.1.0 | Governança inicial adaptada do projeto Java para o port Node.js |

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&animation=twinkling)
