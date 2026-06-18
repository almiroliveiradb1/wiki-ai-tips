# Skill de Planejamento Orientada a Contratos

Boa tarde! Se liga, esse resumo que você trouxe é a bíblia da maturidade no desenvolvimento de agentes.
Como seu instrutor, deixa eu te mandar a real: o maior erro de quem está começando a criar agentes de IA é achar que o prompt nativo (mode: planning) resolve tudo. Não resolve. Se você deixa o agente solto, ele vira um "gerador de lero-lero técnico" altamente inconsistente.
Para que esse plano vire código de produção sem alucinação, nós precisamos envelopar essa capacidade em uma Skill Orquestrada. Vamos detalhar como isso funciona na prática, com exemplos reais do mercado, e fechar com um gráfico para você fixar o fluxo mental na sua cabeça.
1. O Problema do Planejamento Nativo (The "Wild West" Prompting)
Quando você digita /plan em um agente genérico, ele olha para o código, acha tudo lindo e cospe um plano bonito, mas abstrato.
O que o agente nativo faz: "Vamos criar uma rota de autenticação segura usando JWT."
O que a Skill de Planejamento Exige: O contrato exato da API (POST /api/v1/auth/login), a estrutura do payload, o catálogo de erros (ERR_AUTH_INVALID_CREDENTIALS -> 401) e a matriz de permissões.
A skill retira a arbitrariedade do LLM. Ela força o modelo a seguir um framework rígido definido pelo seu time de engenharia.
2. Na Prática: O Pipeline de Execução da Skill
Se fôssemos traduzir esse resumo em um fluxo de execução de um agente especialista, ele seguiria rigorosamente estas 5 etapas:
Etapa 1: Carga de Contexto Obrigatória & Alinhamento RPI
O agente não pode "tirar ideias da cartola". Ele lê ativamente a pasta do projeto:
Plaintext

```
📂 docs/
  ├── 📂 rpi-decisions/ -> "Usar Next.js 14 App Router e Iron Session para JWT"
  ├── 📂 testing-guides/ -> "Mínimo de 80% de cobertura com Vitest"
  └── phase-01-summary.md -> O que já foi entregue antes
```



Etapa 2: Validação (Gating)
Aqui o agente atua como um revisor chato. Se o planejamento do projeto pede autenticação via JWT, mas ninguém definiu a chave secreta ou o tempo de expiração no guia de arquitetura, o agente para a execução e joga a bola para o dev:
⚠️ [BLOCKER] Detectada inconsistência: O requisito pede autenticação JWT, mas a matriz de autorização para a rota /dashboard não foi especificada nas decisões técnicas. Por favor, defina os escopos (roles) antes de prosseguir.

Etapa 3: Pesquisa Instrumental JIT (Just-In-Time)
Com o escopo fechado, ele faz uma busca cirúrgica (via Web ou Context7) para validar sintaxe ou breaking changes:
Exemplo: Pesquisar a assinatura exata da função de rota do Next.js 14 para garantir que o plano não use a sintaxe antiga do Next.js 12.
Etapa 4: Decomposição em Implementation Steps (Micro-Passos)
Em vez de um passo gigante "Implementar o Login", a skill quebra em fatias atômicas. Veja a estrutura interna de um passo:
Step 2.1: Implementação do Middleware de Autenticação JWT
Ação Técnica: Criar o arquivo src/middleware.ts, interceptar as rotas privadas e decodificar o token usando jose.
Testes: Criar caso de teste no Vitest garantindo que requisições sem token recebam status 401 Unauthorized.
Critério de Aceitação: O middleware deve bloquear acessos não autenticados e o payload decodificado deve ser injetado nos headers da requisição em menos de 50ms.
Etapa 5: Especificações Globais (O Contrato)
Fora dos passos, o documento consolida os anexos técnicos do domínio:
Matriz de Erros: Tabela com status HTTP, código interno e mensagem.
Modelagem: Esquema do banco de dados (Prisma/SQL).
3. Visualizando o Fluxo da Skill de Planejamento
Para consolidar o aprendizado, executei um script para gerar o gráfico desse workflow. Ele mostra visualmente como a skill atua como um funil de qualidade, transformando inputs brutos e caóticos em um guia de implementação blindado contra falhas.
Note como as fontes de contexto alimentam a validação antes de qualquer quebra de tarefas ocorrer.

```
# Vamos gerar o gráfico do fluxo de trabalho da Skill de Planejamento descrito no texto.import matplotlib.pyplot as pltimport networkx as nx
# Configurando o gráficoplt.figure(figsize=(12, 7))
G = nx.DiGraph()
# Nós (Etapas do Processo)nodes = {
    "Inputs": "Fontes de Contexto\n(Decisões RPI, Guia de Testes,\nFases Anteriores)",
    "Validacao": "Validação de Gaps\n(Confrontar Fontes\n& Tratar Conflitos)",
    "Pesquisa": "Pesquisa Instrumental\n(Validação de Stack/\nNext/Libs)",
    "Specs": "Especificações Globais\n(Contratos API, Modelagem,\nCatálogo de Erros)",
    "Steps": "Implementation Steps\n(Ações Técnicas, Testes,\nCritérios de Aceitação)",
    "Output": "Guia de Implementação\n(Sem Gaps / Pronto p/ Código)"}
# Adicionando nós e arestas para o fluxoedges = [
    ("Inputs", "Validacao"),
    ("Validacao", "Pesquisa"),
    ("Pesquisa", "Specs"),
    ("Specs", "Steps"),
    ("Steps", "Output")
]
G.add_edges_from(edges)
# Posicionamento dos nós em layout de fluxo (esquerda para a direita)pos = {
    "Inputs": (0, 1),
    "Validacao": (2, 1),
    "Pesquisa": (4, 1),
    "Specs": (6, 1.5),
    "Steps": (6, 0.5),
    "Output": (8.5, 1)
}
# Ajustando as arestas que bifurcam e se juntam no finalG.add_edge("Pesquisa", "Steps") # Conecta pesquisa a ambos se necessário, mas vamos manter o fluxo limpoG.remove_edge("Specs", "Steps")
G.add_edge("Validacao", "Specs")
G.add_edge("Specs", "Output")
G.add_edge("Steps", "Output")
# Ajustando posições finais para um design de árvore/funil limpopos = {
    "Inputs": (0, 1),
    "Validacao": (2, 1),
    "Pesquisa": (4, 1),
    "Specs": (6, 1.4),
    "Steps": (6, 0.6),
    "Output": (8.5, 1)
}
# Desenhando os nósnx.draw_networkx_nodes(G, pos, node_size=3500, node_color="#1E293B", edgecolors="#38BDF8", linewidths=2)
# Desenhando as arestasnx.draw_networkx_edges(G, pos, edgelist=G.edges(), width=2, arrowsize=20, arrowstyle="->", edge_color="#64748B")
# Labels dos nóslabels = {k: v for k, v in nodes.items()}
nx.draw_networkx_labels(G, pos, labels, font_size=9, font_color="white", font_family="sans-serif", font_weight="bold")
plt.title("Workflow Arquitetural da Skill de Planejamento", fontsize=14, fontweight="bold", pad=20, color="#0F172A")
plt.axis("off")
plt.tight_layout()
# Salvando imagemplt.savefig("workflow_planning_skill.png", dpi=300, bbox_inches='tight')
plt.close()
INFO: O gráfico foi gerado com sucesso e estruturado para refletir o funil de engenharia.
O Workflow Visual da Skill
Aqui está o mapa mental e arquitetural de como sua Skill deve operar:
💡 Resumo para o seu Board de Arquitetura:
"Se a IA inventa, o erro é do blueprint."
O objetivo dessa skill é garantir que o agente de implementação vire apenas um executor de luxo. Ele não toma decisões de design no meio do código; ele segue o documento gerado por essa skill. Se o documento for perfeito, o código será impecável.
Ficou clara a diferença entre dar um prompt de planejamento e criar uma Skill de Planejamento Orientada a Contratos? Aceito palpites e complementos sobre assunto, vamos nos ajudar!
```


