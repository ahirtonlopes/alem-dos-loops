# Além dos Loops: o que aprendemos errando com produtos de IA Agêntica

Material da palestra de **Ahirton Lopes, PhD** no **IA Conference Brasil 2026** (São Paulo, 24/09/2026).

Todo mundo sabe escrever um loop de agente. O que separa um protótipo de um produto é o que fica em volta do loop: contexto, verificação, limites e o time. A palestra parte de um case **fictício e composto**, a Amplitude Seguros, com agentes regulando sinistros de automóvel num setor regulado, e passa por sete erros que custariam caro em produção, com números medidos e casos públicos.

## Método

O case é desenhado com o **AI Architecture Decision Canvas**, do AI Architecture Toolkit de Ahirton Lopes, inspirado no [Machine Learning Canvas](https://www.louisdorard.com/machine-learning-canvas) de Louis Dorard. São 11 caixas, de processo e dados até métricas de sucesso. Cada caixa vira perguntas em linguagem de negócio para o dono do processo, que também assina o que fica fora de escopo. Na palestra, cada erro é apresentado como uma caixa do canvas que ficou em branco.

## Conteúdo

| Arquivo | O que é |
|---|---|
| `Palestra_Ahirton_AlemDosLoops.pptx` | Slides da palestra |
| `Palestra_Ahirton_AlemDosLoops.pdf` | Os mesmos slides em PDF |
| `demo/demo_alem_dos_loops.ipynb` | Demo com Google ADK + Gemini, pronta pra rodar |
| `demo/demo_alem_dos_loops_EXECUTADO.ipynb` | A mesma demo com as saídas de uma execução real |

## A demo

Dois erros acontecendo e o código que os segura:

1. **A alçada estava só no prompt.** Um agente de pagamento aprova uma indenização de R$ 185 mil num carro de R$ 92 mil. A correção põe validação, alçada e aprovação humana na própria ferramenta, sem mudar a instrução do agente.
2. **O loop sem contrato.** Um agente de cobertura nega um sinistro sem cláusula que fundamente a decisão. A correção é um loop com contrato: orçamento de chamadas (`RunConfig(max_llm_calls=...)`), verificador externo, saída de emergência para um humano e trilha por volta.

### Como rodar

1. Gere uma API key gratuita em [Google AI Studio](https://aistudio.google.com/apikey).
2. **No Colab:** abra o notebook, crie o secret `GOOGLE_API_KEY` (ícone de chave na barra lateral) e libere o acesso do notebook.
   **Local:** `pip install google-genai google-adk jupyter`, rode `export GOOGLE_API_KEY=...` e abra o notebook.
3. Execute as células em ordem. A primeira chamada confirma que a chave e o modelo estão funcionando.

Para usar Vertex AI no seu projeto GCP, troque `USE_VERTEX_AI = True` e ajuste `VERTEX_PROJECT_ID`.

Os modelos não são determinísticos: numa execução isolada o agente pode se comportar melhor ou pior do que nas saídas salvas. É justamente por isso que os controles ficam no código, e não no prompt.

## Referências

**Agentes e loops**
- Yao et al., [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) (ICLR 2023)
- Geoffrey Huntley, [Ralph Wiggum as a "software engineer"](https://ghuntley.com/ralph/) (2025)
- METR, [Time Horizon 1.1](https://metr.org/blog/2026-1-29-time-horizon-1-1/) (jan/2026)
- Anthropic, [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) (dez/2024)

**Multiagente**
- Google Research, [Towards a science of scaling agent systems](https://research.google/blog/towards-a-science-of-scaling-agent-systems-when-and-why-agent-systems-work/) (jan/2026)
- Anthropic, [Building multi-agent systems: When and how to use them](https://claude.com/blog/building-multi-agent-systems-when-and-how-to-use-them) (jan/2026)
- Cognition, [Multi-Agents: What's Actually Working](https://cognition.com/blog/multi-agents-working) (abr/2026)

**Contexto e harness engineering**
- Anthropic, [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) (set/2025)
- LangChain, [Context Engineering for Agents](https://www.langchain.com/blog/context-engineering-for-agents) (jul/2025)
- Chroma, [Context Rot](https://www.trychroma.com/research/context-rot) (jul/2025)
- Martin e Roger, [Classifier Context Rot](https://arxiv.org/abs/2605.12366) (mai/2026)
- Mitchell Hashimoto, [My AI Adoption Journey](https://mitchellh.com/writing/my-ai-adoption-journey) (fev/2026)
- Anthropic, [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps) (mar/2026)
- LangChain, [Improving Deep Agents with harness engineering](https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering) (fev/2026)

**Casos públicos citados**
- Replit apaga banco de produção durante code freeze: [The Register](https://www.theregister.com/2025/07/22/replit_saastr_response/) (jul/2025)
- STJ investiga prompt injection em petições: [STJ](https://www.stj.jus.br/sites/portalp/Paginas/Comunicacao/Noticias/2026/20052026-Tentativas-de-uso-de-prompt-injection-no-STJ-serao-investigadas.aspx) (mai/2026)
- Agente perde instrução após compactar o contexto: [TechCrunch](https://techcrunch.com/2026/02/23/a-meta-ai-security-researcher-said-an-openclaw-agent-ran-amok-on-her-inbox/) (fev/2026)
- Nx "s1ngularity": [postmortem oficial](https://nx.dev/blog/s1ngularity-postmortem) (ago/2025) e [GitHub Security Lab sobre pwn requests](https://securitylab.github.com/resources/github-actions-preventing-pwn-requests/)

**Segurança e ferramentas**
- [OWASP GenAI Security Project](https://genai.owasp.org)
- [Google Agent Development Kit (ADK)](https://adk.dev)

## Contato

[LinkedIn](https://www.linkedin.com/in/ahirtonlopes) · [GitHub](https://github.com/ahirtonlopes) · [X](https://x.com/ahirtonlopes)
