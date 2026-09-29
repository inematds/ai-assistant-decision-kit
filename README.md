# AI Assistant Decision Kit

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

Material de **terceiro**, baixado em 2026-08-24 para estudo. Ajuda a decidir **qual modelo de assistente de IA pessoal adotar** — ou a não trocar de plataforma à toa — em vez de reconstruir o mesmo assistente cada vez que sai um produto novo.

- **Autor:** Mark Kashef
- **Origem:** [`earlyaidopters/gumroad-resources`](https://github.com/earlyaidopters/gumroad-resources/tree/main/resources/the-ai-assistant-decision-kit)
- **Produto:** https://markkashef.gumroad.com/l/ai-assistant-decision-kit (CAD$ 0+)
- **Vídeo:** https://youtu.be/aBdMey9nqcM
- **Mapa interativo:** https://ai-assistant-house-map.markkashef.chatgpt.site/
- **Licença:** MIT — ver `kit/LICENSE.md` (resumo em português: `traducao/LICENSE-NOTA.md`)

> **Regra deste repositório:** o conteúdo de `kit/`, `origem/` e `zips/` é cópia fiel do upstream e fica **intacto**. Nossas adições (este README e toda a pasta `traducao/`) vivem fora dessas pastas. Ver `CLAUDE.md`.


## 📖 Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/ai-assistant-decision-kit/guia/**

---

## Estrutura completa

```
README.md                      este arquivo
CLAUDE.md                      regras do projeto para agentes
kit/                           pacote completo, descompactado (upstream, intacto)
  START-HERE.md                por onde começar (em inglês)
  WEBSITE.md                   instruções do mapa interativo
  prompts/PASTE-INTO-ANY-AI.md   o caminho sem instalar nada: cola em qualquer IA
  website/OPEN-THE-AI-ASSISTANT-MAP.html   redirect para o mapa online
  ai-assistant-system-advisor/   a skill instalável (SKILL.md + references/ + agents/)
  LICENSE.md · WEBSITE.md
origem/                        metadados da página Gumroad (upstream, intacto)
  README-origem.md             descrição original do produto
  content.md                   cópia da página de vendas
  meta.json                    metadados brutos (preço, arquivos, permalink)
zips/                          os dois .zip originais, intactos
traducao/                      NOSSA tradução completa em pt-BR (fora do upstream)
  README.md                    índice das traduções + glossário adotado
  START-HERE.md · WEBSITE.md · LICENSE-NOTA.md
  prompts/ · website/ · origem/
  ai-assistant-system-advisor/   skill inteira traduzida (SKILL.md, agents/, references/, providers/)
```

## Os dois arquivos baixados

| zip | conteúdo |
|---|---|
| `AI-Assistant-Decision-Kit.zip` (42 KB) | o kit completo — é o que está extraído em `kit/` |
| `AI-Assistant-System-Advisor-Skill.zip` (35 KB) | só a skill |

**Os dois trazem a mesma skill** — conferido com `diff -rq`, byte a byte idêntica. Por isso extraímos só o kit completo; os dois zips originais continuam preservados em `zips/`.

## Como usar

### 1. Sem instalar nada

Copie `kit/prompts/PASTE-INTO-ANY-AI.md` inteiro (ou a versão em português em `traducao/prompts/PASTE-INTO-ANY-AI.md`) e cole no Claude, ChatGPT ou Codex. A entrevista de decisão roda na conversa.

### 2. Como skill instalável

A pasta `kit/ai-assistant-system-advisor/` está no formato Agent Skill (frontmatter com `name` e `description`). Para instalar:

```bash
ln -s ~/projetos/ai-assistant-decision-kit/kit/ai-assistant-system-advisor \
      ~/.claude/skills/ai-assistant-system-advisor        # Claude Code
# Codex: ~/.codex/skills/ai-assistant-system-advisor
```

Depois peça: *"Use the AI Assistant System Advisor to help me decide which setup fits my real work."*

**Estado: NÃO instalada** — instalar é decisão do usuário. Instale sempre o **original em inglês**, não a tradução (a tradução é para leitura).

### 3. Mapa interativo

Abra https://ai-assistant-house-map.markkashef.chatgpt.site/ (ou o HTML de redirect em `kit/website/`). O arquivo local tem só 1,3 KB — é um redirect, não a página; o conteúdo real depende de internet. O mapa cobre os cinco assistentes destacados, cortes de arquitetura, quadro de tiers arrastável e mapa combinado de capacidades. Pesquisa travada em 21/08/2026 (`kit/WEBSITE.md`).

## O que a skill faz

Um consultor de sistemas orientado a evidência que **entrevista antes de recomendar** e trabalha em quatro modos:

| modo | pergunta que responde |
|---|---|
| Auditoria completa de decisão | "Qual caminho é melhor para mim?" (padrão quando se pergunta qual assistente escolher) |
| Auditoria de troca | "Vale a pena sair do meu setup atual para o X?" |
| Mergulho no produto | "Como funciona por dentro o assistente X?" |
| Blueprint de sistema próprio | "Como seria uma arquitetura DIY para meus requisitos?" |

### Método (cinco etapas, um arquivo por etapa em `references/`)

1. **Entrevista adaptativa** (`interview-engine.md`) — até 2 rodadas, máx. 3 perguntas por rodada; usa `AskUserQuestion` no Claude Code, `request_user_input` no Codex ou conversa normal. Se o usuário não aponta uma falha recorrente real, "ficar onde está" vira a hipótese principal.
2. **Pesquisa** (`research-protocol.md`) — registra data/hora, URLs abertas, releases e commits inspecionados; sem navegação, usa os dossiês datados e avisa que fatos voláteis precisam reverificação.
3. **Modelo de decisão** (`decision-model.md`) — escolhe o *caminho operacional* antes da marca: ficar onde está → assistente gerenciado → runtime open-source → sistema próprio (DIY). Compara separadamente padrões de fábrica vs. teto alcançável, sobre 10 camadas comuns (modelo/roteamento, runtime, arquivos, ferramentas/conectores, memória, skills, rotinas/triggers, interfaces, permissões/fronteira de confiança, manutenção/backup).
4. **Dossiês** (`references/providers/`) — lê apenas os relevantes ao modo; todos os seis na auditoria completa.
5. **Pacote de decisão** (`output-contract.md`) — 11 itens obrigatórios, entre eles: veredito direto nomeando o caminho antes do produto, diagnóstico do que falha hoje, tabela de aderência ponderada com notas de evidência, runner-up e motivos das exclusões, inventário do que se mantém/perde/reconstrói, **teste reversível de 30–60 min** e **piloto de sete dias** com critérios de sucesso e saída.

Filosofia central: anti-hype. Trocar por novidade de rede social não é motivo; feature reproduzível barata no setup atual é candidato a teste, não razão para migrar; nenhum movimento unidirecional sem ensaio prévio.

## Dossiês de provedores

Pesquisa travada em **23/08/2026** — features, preços, limites e disponibilidade mudam rápido; a skill reverifica fontes de primeira parte quando há navegação disponível.

| dossiê | tipo | foco |
|---|---|---|
| `grok-bot.md` | gerenciado | bot da xAI/X, integração com ecossistema X |
| `hermes-agent.md` | open-source | harness exposto (loop, memória curada, skills, subagentes, cron), multi-modelo; repo canônico NousResearch/hermes-agent, release v0.20.5 / v2026.8.19 |
| `claude-cowork.md` | gerenciado | ambiente Anthropic de trabalho colaborativo |
| `chatgpt-work.md` | gerenciado | oferta OpenAI para trabalho/conectores corporativos |
| `openclaw.md` | open-source | runtime open-source self-hosted |
| `owned-diy.md` | rota DIY | arquitetura própria model-agnostic |

## Tradução em português

Toda a documentação foi traduzida para pt-BR em **[`traducao/`](traducao/README.md)**, espelhando a estrutura do kit (mesmos nomes de arquivo). Lá estão o índice completo, o glossário adotado (harness, lock de pesquisa, pacote de decisão…) e as exceções documentadas: `meta.json`/`content.md` (dados brutos de plataforma) e o texto legal da licença permanecem sem tradução.

## Licença

MIT © 2026 Mark Kashef — guia, prompt e skill. Texto oficial em inglês: `kit/LICENSE.md`. Resumo não-oficial: `traducao/LICENSE-NOTA.md`.
