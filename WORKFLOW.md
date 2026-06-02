# WORKFLOW.md — Transcrição Documental

**Versão:** v1.0 — 2026-06-02
**Status:** ativo
**Responsável:** Victor Leonardo Arimatea Queiroz — Diretor de Transformação Digital
**Repositório:** workflow-transcricao-documental (W01)

---

## Seção 1 — Identificação

| Campo | Valor |
|---|---|
| Nome do processo | Transcrição Documental para Markdown |
| ID | W01 |
| Versão | v1.0 |
| Status | ativo |
| Data de criação | 2026-06-02 |
| Responsável | DTD/SETIS/SES-DF |
| Skill associada | [skill-transcricao-documental (S05)](https://github.com/victorarimatea/skill-transcricao-documental) |
| Repositório de saída | [governanca-ses-df (D01)](https://github.com/victorarimatea/governanca-ses-df) |

---

## Seção 2 — Missão e contexto organizacional

### Missão

Transformar documentos regulatórios oficiais — leis, portarias, resoluções e
referências internacionais — em arquivos Markdown estruturados, fiéis ao original,
auditáveis, pesquisáveis e reutilizáveis, constituindo a camada documental primária
do ecossistema de governança digital da DTD/SETIS/SES-DF.

### Por que este processo existe

A DTD/SETIS/SES-DF opera em um ambiente regulatório denso e em constante evolução.
Decisões técnicas, análises de conformidade, desenvolvimento de instrumentos como
IACs e PoCs, e o trabalho de transformação digital em saúde dependem de acesso rápido
e confiável ao texto integral de normas vigentes.

PDFs regulatórios são o formato oficial de publicação — mas são opacos para ferramentas
de IA, difíceis de comparar entre si, e não permitem indexação semântica. A transcrição
para Markdown estruturado resolve esse problema: o texto passa a ser consultável,
comparável, versionável e consumível por qualquer camada do ecossistema.

### Objetivos estratégicos atendidos

- Construção da camada documental primária do ecossistema (`governanca-ses-df`)
- Habilitação de análises de conformidade automatizadas (workflows de IAC)
- Redução de tempo de acesso ao texto normativo em análises e produções da DTD
- Preservação de memória normativa com rastreabilidade de versões

### Quem pode acionar este workflow

- O Diretor de Transformação Digital (DTD)
- Qualquer instância do Claude com acesso ao ecossistema, ao ser solicitada
- Workflows de nível superior que consomem este como subprocesso (ex: workflow-iac-conformidade)

---

## Seção 3 — Estado final esperado

Uma execução bem-sucedida deste workflow produz um arquivo `.md` que satisfaz
**todos** os critérios abaixo — este é o benchmark de qualidade verificável:

### 3.1 Estrutura obrigatória
- [ ] Front Matter YAML válido com todos os 13 campos preenchidos
- [ ] Ficha Técnica Documental em tabela Markdown com 12 linhas
- [ ] Seção "Observações da Conversão" presente e não vazia
- [ ] Seção "Conteúdo Integral Transcrito" com conteúdo substantivo (> 200 chars)
- [ ] Seção "Controle de Integridade" com status de conversão explícito

### 3.2 Fidelidade ao original
- [ ] Nenhum elemento estrutural jurídico ausente
- [ ] Nenhum artefato de extração presente no conteúdo
- [ ] Assinatura(s) presente(s) e corretamente formatadas
- [ ] Texto integral sem truncamento

### 3.3 Organização e rastreabilidade
- [ ] Cada marcador estrutural jurídico em parágrafo próprio
- [ ] `arquivo_original` corresponde ao nome exato do PDF fonte
- [ ] `fonte_externa` contém URL válida
- [ ] Arquivo salvo na subpasta correta do D01 com nomenclatura padrão

### 3.4 Registro
- [ ] Status atualizado no §9 do `WORKFLOW-ESPECIFICACAO.md` do D01
- [ ] Log de execução criado em `execucoes/` deste repositório (quando em sessão autenticada)

---

## Seção 4 — Etapas do processo

| # | Etapa | Executor | Tipo | Entrada | Saída |
|---|---|---|---|---|---|
| 0 | Leitura de contexto | S05 (IA) | Automatizada | Contexto da sessão | Identificação do documento, fase, necessidades especiais |
| 1 | Extração do PDF | S05 (IA) | Automatizada | Arquivo PDF | Texto bruto extraído |
| 2 | Limpeza e reflow | S05 (IA) | Automatizada | Texto bruto | Texto limpo sem artefatos |
| 3 | Estrutura jurídica | S05 (IA) | Automatizada | Texto limpo | Texto com marcadores estruturais |
| 4 | Montagem do Markdown | S05 (IA) | Automatizada | Texto estruturado | Arquivo .md com 5 seções |
| 5 | Auto-verificação | S05 (IA) | Automatizada | Arquivo .md | Status: PASSOU / ALERTA / FALHOU |
| 6 | Nomenclatura e salvamento | S05 (IA) | Automatizada | Arquivo verificado | Arquivo .md salvo na subpasta correta do D01 |
| 7 | Atualização do workflow | Humano ou IA | Semi-automática | Arquivo entregue | §9 do WORKFLOW-ESPECIFICACAO.md atualizado |
| 8 | Registro do log | S04 (IA) | Automatizada em sessão autenticada | Execução concluída | Log em `execucoes/` deste repositório |

**Etapas com intervenção humana obrigatória:**
- Fornecimento do arquivo PDF quando não disponível no ambiente da IA
- Revisão visual quando auto-verificação retorna ALERTA ou FALHOU
- Aprovação do log antes de commit em sessões autenticadas

---

## Seção 5 — Skills e subprocessos consumidos

| Recurso | Tipo | Papel neste workflow | Link |
|---|---|---|---|
| skill-transcricao-documental | S05 — Skill | Executa as Etapas 0–7 | [→](https://github.com/victorarimatea/skill-transcricao-documental) |
| skill-github-orquestracao | S04 — Skill | Executa o registro do log (Etapa 8) em sessões autenticadas | [→](https://github.com/victorarimatea/skill-github-orquestracao) |
| governanca-ses-df | D01 — Documento | Repositório de destino dos arquivos transcritos | [→](https://github.com/victorarimatea/governanca-ses-df) |

**Subprocessos consumidos por workflows de nível superior:**
Este workflow pode ser consumido como subprocesso por:
- `workflow-iac-conformidade` (planejado) — quando identificar gap normativo,
  aciona este workflow para transcrever o documento faltante antes de prosseguir

---

## Seção 6 — Histórico de problemas e soluções

Ver `WORKFLOW-ESPECIFICACAO.md` no repositório D01 (`governanca-ses-df`) para
o histórico completo de problemas P01–P08 identificados e resolvidos durante
o desenvolvimento deste pipeline.

→ [governanca-ses-df/WORKFLOW-ESPECIFICACAO.md](https://github.com/victorarimatea/governanca-ses-df/blob/main/WORKFLOW-ESPECIFICACAO.md)

**Problemas registrados:** P01 (assinaturas), P02 (artefatos DOU), P03 (cabeçalhos SINJ/BVS),
P04 (marcadores fundidos), P05 (quebras espúrias), P06 (municípios Portaria 3.233),
P07 (observações DOU), P08 (arquivo inutilizável).

---

## Seção 7 — Roadmap de automação

| Etapa | Status atual | Próxima evolução |
|---|---|---|
| 0–6 (extração ao salvamento) | ✅ Automatizada via S05 | Fila sequencial autônoma (condição: taxa PASSOU ≥ 95% em ≥ 10 docs) |
| 7 (atualização do workflow) | 🔄 Semi-automática | Automatizar atualização do §9 via S04 em sessões autenticadas |
| 8 (log de execução) | 🔄 Automática em sessões autenticadas | Extender para todas as sessões com mecanismo de commit diferido |
| Fila de documentos | 🔄 Manual | Automatizar leitura do §9 e processamento sequencial sem intervenção |

**Condições para progressão para fase sequencial autônoma:**
- Taxa de PASSOU ≥ 95% em ≥ 10 documentos consecutivos
- Nenhum problema P01–P08 reincidente
- Critérios do §3 cobertos por testes automatizados

---

## Seção 8 — Referências e dependências

### Documentos normativos que habilitam este workflow
- Resolução CFM nº 2.314/2022 — referenciada nos documentos transcritos
- LGPD (Lei 13.709/2018) — governa o tratamento dos dados dos documentos
- Marco Civil da Internet (Lei 12.965/2014) — base para acesso às fontes

### Repositórios do ecossistema referenciados
- M01 `ecossistema-sumario` — matrizes de nomenclatura e convenções
- S05 `skill-transcricao-documental` — skill de execução
- S04 `skill-github-orquestracao` — skill de registro no ecossistema
- D01 `governanca-ses-df` — repositório de destino e WORKFLOW-ESPECIFICACAO.md

### Fontes homologadas para extração
Portal Planalto.gov.br, DOU/Imprensa Nacional, SINJ-DF,
BVS Saúde Legis, portais internacionais (IMDRF, OECD, WHO, PAHO, EUR-Lex).
