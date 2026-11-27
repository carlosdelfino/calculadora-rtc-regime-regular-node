![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=Requisitos%20RTC&fontSize=36&fontAlignY=35&animation=twinkling)

![visitors](https://visitor-badge.laobi.icu/badge?page_id=RapportTecnologia.AgenticSpace.rtc_requirements)
[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC_BY--SA_4.0-blue.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
![Language: Portuguese](https://img.shields.io/badge/Language-Portuguese-brightgreen.svg)
![Status](https://img.shields.io/badge/Status-Ongoing-yellow)
[![GitHub Issues](https://img.shields.io/github/issues/RapportTecnologia/AgenticSpace)](https://github.com/RapportTecnologia/AgenticSpace/issues)

# Requisitos — migração incremental Java → Node.js

## Propósito e escopo

Registrar critérios verificáveis da primeira fatia de conversão. A referência é
`calculadora-rtc-regime-regular-java`, especialmente `BaseCalculoService.java`,
os DTOs `BaseCalculoCibsInput` e `BaseCalculoISMercadoriasInput`, e os testes
`Teste_BaseCalculoCibs_Controller` e `Teste_BaseCalculoIS_Controller`.
A implementação é de homologação, não uma certificação fiscal nem migração completa.

## Histórias e critérios de aceitação

| ID | História / requisito | Aceitação e evidência automatizada |
|---|---|---|
| RTC-001 | Como integrador, quero calcular bases de mercadorias CBS/IBS e IS com as fórmulas Java. | Mesmos componentes de soma e dedução; vetores Java 1290.00, 522.50, 1190.00 e 1345.00 reproduzidos em `backend/test/calculadora.test.js`. |
| RTC-002 | Como usuário, quero preservar valores decimais sem erros de ponto flutuante. | Strings de até 18 dígitos inteiros e 12 decimais; operações BigInt exatas; saída string com ao menos duas casas e sem arredondamento intermediário. Precisão superior é rejeitada. |
| RTC-003 | Como integrador, quero rejeição clara de entrada inconsistente. | Ano mínimo 2026 para CBS/IBS e 2027 para IS; PIS/COFINS rejeitados desde 2027, ICMS/ISS desde 2033; valores negativos, nulos, campos desconhecidos e base negativa rejeitados. |
| RTC-004 | Como operador, quero erros seguros e rastreabilidade sem dados fiscais nos logs. | JSON até 64 KiB; media type obrigatório; erros com code, message, details e nest_step; request ID, início, conclusão, status e duração nos logs; sem payloads/stack nas respostas. |
| RTC-005 | Como agente ou humano, quero descobrir e utilizar a API. | OpenAPI 3.1 em `/openapi.json`, Swagger em `/swagger`, ReDoc em `/redoc`; operações de cálculo declaram sem autenticação, nível público e uso humano permitido. |
| RTC-006 | Como usuário, quero exemplos de consumo extensíveis com estados de sucesso e falha. | React/TypeScript com cliente injetável via Factory, exemplos CBS/IBS e IS, timeout, formulário acessível e valores monetários enviados como strings; testes de cliente e E2E. |
| RTC-007 | Como operador, quero distribuir frontend e backend em uma única aplicação. | Build em `backend/public/`; Node serve assets, fallback SPA somente em navegação HTML e nunca para API; arquivos privados/ocultos e assets ausentes não são entregues; verificação E2E desktop/celular. |
| RTC-008 | Como mantenedor, quero portabilidade sem reescrever regras fiscais. | Núcleo sem imports Node/provedor; adaptadores Node, Vercel Fetch e Worker com ASSETS; testes locais dos contratos dos adaptadores. Validação nativa e deploy nos provedores permanecem pendentes. |

## Contrato e segurança

As duas operações POST preservam os caminhos Java em `/calculadora/base-calculo/`.
Componentes omitidos valem zero. Os valores retornados são strings decimais;
a validação de domínio usa HTTP 422, ao contrário do HTTP 400 nos testes Java.
JSON malformado usa 400, método inválido 405, limite de corpo 413, media type 415.
O campo de orientação é **`nest_step`**, conforme regra local, não `next_step`.
O documento OpenAPI é retornado diretamente como especificação, não envelopado.

Não há cadastro, login, persistência ou rotas privadas nesta fatia. Todas as
operações disponíveis são públicas, sem autenticação, para agente público e humanos.
Qualquer futura rota privada requer decisão específica de autenticação e autorização;
não há implementação de identidade blockchain nesta entrega. HTTPS e proteção
contra abuso devem ser configurados antes de exposição pública.
Swagger/ReDoc usam CDN versionada; a API e o frontend gerado não exigem a CDN.
Arquivos em `backend/public/` são públicos e não devem conter dados privados.

## Arquitetura e operação

Domínio determinístico → serviços compostos por Factory → aplicação Fetch →
adaptadores de transporte/arquivos. Estratégias por cálculo compartilham as
validações sem depender de servidor, banco ou provedor. Frontend organizado por
funcionalidade, com contratos tipados e sem regras fiscais duplicadas.

Backend e frontend são submódulos Git independentes. Não há workspace npm.
Use Node 22. Instale com `npm --prefix backend ci` e `npm --prefix frontend ci`.
`npm run build` na raiz gera o frontend em `backend/public/`; `npm start` inicia
o backend na porta 3000. `HOST` e `PORT` configuram a interface e porta.
O build não apaga arquivos existentes no destino; prefira checkout limpo em CI
para não acumular assets antigos. Artefatos são ignorados no Git.

## Estratégia de validação e PDCL

1. **Plan:** comparar fórmulas, DTOs, vigências e vetores Java, explicitando diferenças.
2. **Do:** implementar fatia pequena com testes determinísticos, logs seguros e documentação.
3. **Check Logs:** executar `npm test`, `npm run build`,
   `npm --prefix backend run test:coverage` e
   `PLAYWRIGHT_CHANNEL=chrome npm --prefix frontend run test:e2e` quando Chrome
   estiver instalado; caso contrário instalar Chromium do Playwright e omitir a variável.
4. **Loop:** corrigir divergências e repetir. Auditar dependências de ambos os módulos.

Os nomes dos testes registram os IDs acima. A suíte cobre unidades, HTTP real,
adaptadores com colaboradores de teste e navegador contra backend real, sem
chamadas fiscais externas. Testes Java não são executados pela suíte Node.
Cobertura é medida progressivamente; não há alegação de paridade integral.

## Evidências da primeira entrega — 2026-11-27

Validação executada com Node 22.23.4:

| Comando / camada | Resultado |
|---|---|
| `npm test` | 14 testes backend e 4 testes do cliente frontend aprovados. |
| `npm run build` | Verificação de sintaxe backend, TypeScript e geração Vite em `backend/public/` aprovadas. |
| `PLAYWRIGHT_CHANNEL=chrome npm --prefix frontend run test:e2e` | 2 cenários aprovados contra backend real: dois cálculos, rejeição fiscal, navegação SPA, API isolada e viewport móvel. |
| `npm --prefix backend run test:coverage` | Domínio com 100% de linhas, ramos e funções; aplicação HTTP com 100% de linhas e 95,92% de ramos; adaptador Node com 89,47% de linhas e 85,71% de ramos. |
| `npm audit` em backend e frontend | Nenhuma vulnerabilidade reportada após atualizar Vite para 6.4.6. |
| `git diff --check` na raiz e nos dois submódulos | Sem erros de whitespace. |

Na primeira medição, o domínio tinha 96,92% de linhas e 92,86% de ramos;
os testes de fronteira ampliaram ambos para 100%. Não havia módulo anterior
para comparação histórica. A cobertura do relatório inclui comentários/linhas
segundo o contador nativo do Node; não é evidência de paridade fiscal integral.
Continuam sem cobertura dirigida os erros de filesystem fora de ENOENT/ENOTDIR
e falhas de transporte depois do início da resposta. A suíte Java e os runtimes
nativos Vercel/Cloudflare não foram executados.

O E2E inicialmente detectou `Illegal invocation` ao chamar `fetch` como método
da instância do cliente. A invocação foi desacoplada do receiver, coberta por
regressão unitária e revalidada no navegador. Logs revisados mostraram respostas
200 para cálculos válidos, 422 para base negativa e 404 para API/assets ausentes,
sem registrar valores fiscais nem payloads. Requisitos RTC-001 a RTC-008 foram
exercitados no escopo local descrito na tabela de aceitação.

## Próximas fatias, fora desta entrega

- Base unificada e base NFS-e com seus enums e regras condicionais.
- Cálculo final de IBS/CBS/IS, reduções, diferimento e compras governamentais.
- Repositórios/tabelas fiscais versionados, classificação e vigência.
- Totalização, XML, pedágio e dados abertos.
- Configuração e validação nativa Vercel/Cloudflare, HTTPS e proteção de tráfego.

## Changelog

| Data | Versão | Descrição |
|---|---|---|
| 2026-11-27 | 0.2.0 | Critérios da primeira fatia Node/React e build integrado ao backend. |

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&animation=twinkling)
