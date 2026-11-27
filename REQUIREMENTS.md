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
| RTC-002 | Como usuário dos cálculos de mercadorias, quero preservar valores decimais sem erros de ponto flutuante. | Strings de até 18 dígitos inteiros e 12 decimais; operações BigInt exatas; saída string com ao menos duas casas e sem arredondamento intermediário. Precisão superior é rejeitada. |
| RTC-003 | Como integrador dos cálculos de mercadorias, quero rejeição clara de entrada inconsistente. | Ano mínimo 2026 para CBS/IBS e 2027 para IS; PIS/COFINS rejeitados desde 2027, ICMS/ISS desde 2033; valores negativos, nulos, campos desconhecidos e base negativa rejeitados. |
| RTC-004 | Como operador, quero erros seguros e rastreabilidade sem dados fiscais nos logs. | JSON até 64 KiB; media type obrigatório; erros com code, message, details e nest_step; request ID, início, conclusão, status e duração nos logs; sem payloads/stack nas respostas. |
| RTC-005 | Como agente ou humano, quero descobrir e utilizar a API. | OpenAPI 3.1 em `/openapi.json`, Swagger em `/swagger`, ReDoc em `/redoc`; operações de cálculo declaram sem autenticação, nível público e uso humano permitido. |
| RTC-006 | Como usuário, quero exemplos de consumo extensíveis com estados de sucesso e falha. | React/TypeScript com cliente injetável via Factory, exemplos CBS/IBS e IS, timeout, formulário acessível e valores monetários enviados como strings; testes de cliente e E2E. |
| RTC-007 | Como operador, quero distribuir frontend e backend em uma única aplicação. | Build em `backend/public/`; Node serve assets, fallback SPA somente em navegação HTML e nunca para API; arquivos privados/ocultos e assets ausentes não são entregues; verificação E2E desktop/celular. |
| RTC-008 | Como mantenedor, quero portabilidade sem reescrever regras fiscais. | Núcleo sem imports Node/provedor; adaptadores Node, Vercel Fetch e Worker com ASSETS; testes locais dos contratos dos adaptadores. Validação nativa e deploy nos provedores permanecem pendentes. |
| RTC-009 | Como integrador, quero obter as bases RG, IS e SN em uma operação NF-e/NFC-e. | Endpoint `/calculadora/base-calculo/base-calculo-unificada`; vetores Java NF-e 850.00, NFC-e 830.00, serviço 980.00 e base negativa -100.00 em `backend/test/unificada.test.js`; três bases publicadas. |
| RTC-010 | Como usuário, quero avisos quando o contexto torna um componente inaplicável. | Catálogo dos 15 elementos Java, modelos 55/65 e natureza BEM/SERVICO; prioridade vigência → natureza → modelo; apenas não zero gera aviso; nulo/omitido vale zero; valores negativos são rejeitados mesmo ignorados; ordem estável no Node. |
| RTC-011 | Como integrador, quero publicação idêntica à política numérica do endpoint Java. | Soma/subtração exatas e publicação HALF_EVEN uma vez em duas casas; empates pares/ímpares, resultados negativos, transporte de centavo e zero negativo testados. Os contratos do primeiro pacote não mudam. |
| RTC-012 | Como operador, quero descobrir e rastrear a nova operação sem dados fiscais nos logs. | OpenAPI/Swagger/ReDoc com contrato flat, erros, acesso público e nest_step; logs de avisos somente com quantidade, tipo e request ID; testes de HTTP e adaptadores. |
| RTC-013 | Como usuário, quero explorar cenários da base unificada no frontend. | Formulário contextual, três resultados, avisos, cenários restauráveis, JSON e layout móvel; cliente tipado e E2E contra backend real. |

## Contrato e segurança

As três operações POST preservam os caminhos Java em `/calculadora/base-calculo/`.
Componentes omitidos valem zero. Os valores retornados são strings decimais;
a validação de domínio usa HTTP 422, ao contrário do HTTP 400 nos testes Java.
JSON malformado usa 400, método inválido 405, limite de corpo 413, media type 415.
O campo de orientação é **`nest_step`**, conforme regra local, não `next_step`.
O documento OpenAPI é retornado diretamente como especificação, não envelopado.

O endpoint unificado preserva o contrato flat do DTO Java: `anoFatoGerador`,
`tipoDocumento` 55/65, `natureza` e quinze componentes opcionais. Publica as três
bases com duas casas HALF_EVEN. Nulos valem zero, componentes não negativos fora
de contexto são ignorados com aviso e bases negativas são permitidas, conforme
Java; isso não modifica RTC-002/003 dos endpoints de mercadorias. A normalização
aceita caixa e acentos em BEM/SERVICO. Há limite operacional local de ano 1–9999
e de entrada monetária de 18 inteiros/12 decimais; maior precisão é rejeitada,
sem truncamento. O BigDecimal Java possui precisão interna mais ampla.

O catálogo portado termina em 2033; fora de 2026–2033, todas as bases são zero,
com aviso por componente não zero. Não inferimos vigência futura nem rejeitamos
um ano fora do catálogo como se fosse uma regra fiscal do Java. A ordem dos
avisos é determinística no Node; o serviço original itera um Set sem ordem garantida.
O novo cálculo é público e não adiciona persistência, login ou integração externa.

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

## Evidências do segundo pacote — 2026-11-27

Escopo: RTC-009 a RTC-013, preservando RTC-001 a RTC-008. Foram transcritos os
vetores de `BaseCalculoUnificadaServiceTest.java` e as quinze regras de
`ElementoBaseCalculo.java`; a suíte Java não foi executada nem alterada.

- `npm test`: **22 testes backend e 5 testes de cliente aprovados**
  (antes: 14 e 4). O teste inicial falhou pela ausência da Factory unificada;
  a implementação passou após adicionar serviço, catálogo e rota.
- `npm run build`: sintaxe backend, TypeScript e Vite aprovados; artefatos em
  `backend/public/`, sem dependências adicionais.
- `PLAYWRIGHT_CHANNEL=chrome npm --prefix frontend run test:e2e`: **4 cenários
  aprovados** (antes: 2), incluindo as três bases, avisos, restauração de cenário,
  tela móvel e recuperação após falha de transporte induzida. As respostas fiscais
  usam backend real; o teste de indisponibilidade apenas interrompe a chamada local.
- `npm --prefix backend run test:coverage`: domínio anterior manteve **100% de
  linhas/ramos/funções**; novos módulos `base-unificada`, `fiscal-decimal` e
  `validation-error` também atingiram **100%**. Aplicação HTTP: ramos de 95,92%
  para **96,72%**, mantendo 100% de linhas e funções. Continuam os riscos de I/O
  e transporte do adaptador Node já descritos na primeira entrega.
- Adaptadores Worker/Vercel locais reproduziram sucesso, avisos, HALF_EVEN e 422
  do novo endpoint. Não houve deploy nem execução nos runtimes nativos.
- Logs revisados: `calculation.warnings` com `kind`, `count` e `requestId`, sem
  componentes monetários; respostas 200 e rejeições 422 esperadas. Campos não
  aplicáveis e bases negativas não são tratados como erro no endpoint unificado.

Documentos atualizados são renderizados localmente com Python-Markdown (tabelas
e blocos de código) e os novos destinos locais foram conferidos. O build completo
Jekyll não foi executado: o binário Bundler instalado não possui interpretador
funcional neste ambiente. Não houve alteração de Ruby, Git ou configuração de CI.

## Próximas fatias, fora desta entrega

- Base NFS-e com seus enums e regras condicionais (não confundir com serviço em NF-e).
- Cálculo final de IBS/CBS/IS, reduções, diferimento e compras governamentais.
- Repositórios/tabelas fiscais versionados, classificação e vigência.
- Totalização, XML, pedágio e dados abertos.
- Configuração e validação nativa Vercel/Cloudflare, HTTPS e proteção de tráfego.

## Changelog

| Data | Versão | Descrição |
|---|---|---|
| 2026-11-27 | 0.3.0 | Base unificada NF-e/NFC-e, HALF_EVEN, avisos e novos cenários do frontend; RTC-009 a RTC-013 validados. |
| 2026-11-27 | 0.2.0 | Critérios da primeira fatia Node/React e build integrado ao backend. |

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&animation=twinkling)
