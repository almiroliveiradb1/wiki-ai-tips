O **O **Headroom** (disponível no repositório `headroomlabs-ai/headroom`) é uma camada de compressão de contexto de código aberto (*open-source*) projetada para agentes de IA e assistentes de programação (como Claude Code, Cursor, Aider, entre outros).

A sua principal função é intercetar tudo o que o agente de IA lê — incluindo logs extensos, outputs de ferramentas, ficheiros JSON, código, resultados de pesquisa e histórico de conversação — e **comprimir esses dados entre 60% e 95% antes de chegarem ao LLM**. Isto permite reduzir drasticamente o consumo e o custo de *tokens* de entrada (input) sem comprometer a precisão das respostas.

### Como funciona?

O Headroom atua de forma local e reversível:

1. **ContentRouter:** Identifica o tipo de conteúdo (se é código, prosa, JSON, etc.) e escolhe o melhor algoritmo de compressão.
2. **Compressão Inteligente:** Compacta estruturas repetitivas, dados ruidosos em logs ou tabelas JSON gigantes.
3. **CCR (Context Compression & Retrieval):** Guarda os dados originais localmente. Se o modelo de IA precisar do conteúdo exato de um trecho que foi comprimido, ele pode chamar automaticamente a ferramenta `headroom_retrieve` para obter os dados originais.

---

### Exemplo de Uso

Imagine que está a usar um agente de IA para depurar (*debug*) uma falha num pipeline de Integração Contínua (CI) e o output do erro gera um log gigante com 400 linhas de texto repetitivo.

Normalmente, o agente enviaria todas as 400 linhas para o Claude, gastando milhares de tokens. Com o Headroom ativo, o log é analisado localmente, as redundâncias são removidas e apenas as 15 linhas cruciais (com os avisos e erros reais) são enviadas ao modelo. O Claude recebe a informação essencial, resolve o bug da mesma forma, mas consome apenas uma fração dos tokens originais.

---

### Como instalar e usar no Claude (Claude Code)

O Headroom oferece uma funcionalidade chamada `headroom wrap`, que permite envolver e monitorizar assistentes de IA CLI de forma direta e sem alterar o código deles.

#### Passo 1: Instalação

Pode instalar o Headroom via `pip` no seu ambiente Python (certifique-se de incluir a extensão completa para suporte aos agentes):

```bash
pip install "headroom-ai[all]"

```

*(Alternativamente, se preferir usar diretamente o repositório, pode cloná-lo via `git clone https://github.com/headroomlabs-ai/headroom` e seguir as instruções internas).*

#### Passo 2: Executar com o Claude

Para iniciar o **Claude Code** (ou a ferramenta CLI do Claude) sob a otimização de contexto do Headroom, basta usar o comando `wrap`:

```bash
headroom wrap claude

```

A partir desse momento, o Headroom criará um proxy local automático. Sempre que o Claude fizer uma chamada de API, o Headroom intercetará o tráfego, comprimirá os dados pesados (como outputs de terminal ou logs) e entregará uma versão otimizada ao modelo da Anthropic.

Se o seu assistente de IA suportar o protocolo **MCP (Model Context Protocol)**, o Headroom também pode ser configurado como um servidor MCP, fornecendo as ferramentas `headroom_compress`, `headroom_retrieve` e `headroom_stats` diretamente para o ecossistema do Claude.

---

[Este vídeo sobre o Headroom](https://www.youtube.com/watch?v=03vi4ApFIZE) demonstra uma instalação prática passo a passo, detalha o pipeline de compressão e mostra o Headroom a intercetar em tempo real o tráfego do Claude Code para reduzir drasticamente os tokens consumidos.** (disponível no repositório `headroomlabs-ai/headroom`) é uma camada de compressão de contexto de código aberto (*open-source*) projetada para agentes de IA e assistentes de programação (como Claude Code, Cursor, Aider, entre outros).

A sua principal função é intercetar tudo o que o agente de IA lê — incluindo logs extensos, outputs de ferramentas, ficheiros JSON, código, resultados de pesquisa e histórico de conversação — e **comprimir esses dados entre 60% e 95% antes de chegarem ao LLM**. Isto permite reduzir drasticamente o consumo e o custo de *tokens* de entrada (input) sem comprometer a precisão das respostas.

### Como funciona?

O Headroom atua de forma local e reversível:

1. **ContentRouter:** Identifica o tipo de conteúdo (se é código, prosa, JSON, etc.) e escolhe o melhor algoritmo de compressão.
2. **Compressão Inteligente:** Compacta estruturas repetitivas, dados ruidosos em logs ou tabelas JSON gigantes.
3. **CCR (Context Compression & Retrieval):** Guarda os dados originais localmente. Se o modelo de IA precisar do conteúdo exato de um trecho que foi comprimido, ele pode chamar automaticamente a ferramenta `headroom_retrieve` para obter os dados originais.

---

### Exemplo de Uso

Imagine que está a usar um agente de IA para depurar (*debug*) uma falha num pipeline de Integração Contínua (CI) e o output do erro gera um log gigante com 400 linhas de texto repetitivo.

Normalmente, o agente enviaria todas as 400 linhas para o Claude, gastando milhares de tokens. Com o Headroom ativo, o log é analisado localmente, as redundâncias são removidas e apenas as 15 linhas cruciais (com os avisos e erros reais) são enviadas ao modelo. O Claude recebe a informação essencial, resolve o bug da mesma forma, mas consome apenas uma fração dos tokens originais.

---

### Como instalar e usar no Claude (Claude Code)

O Headroom oferece uma funcionalidade chamada `headroom wrap`, que permite envolver e monitorizar assistentes de IA CLI de forma direta e sem alterar o código deles.

#### Passo 1: Instalação

Pode instalar o Headroom via `pip` no seu ambiente Python (certifique-se de incluir a extensão completa para suporte aos agentes):

```bash
pip install "headroom-ai[all]"

```

*(Alternativamente, se preferir usar diretamente o repositório, pode cloná-lo via `git clone https://github.com/headroomlabs-ai/headroom` e seguir as instruções internas).*

#### Passo 2: Executar com o Claude

Para iniciar o **Claude Code** (ou a ferramenta CLI do Claude) sob a otimização de contexto do Headroom, basta usar o comando `wrap`:

```bash
headroom wrap claude

```

A partir desse momento, o Headroom criará um proxy local automático. Sempre que o Claude fizer uma chamada de API, o Headroom intercetará o tráfego, comprimirá os dados pesados (como outputs de terminal ou logs) e entregará uma versão otimizada ao modelo da Anthropic.

Se o seu assistente de IA suportar o protocolo **MCP (Model Context Protocol)**, o Headroom também pode ser configurado como um servidor MCP, fornecendo as ferramentas `headroom_compress`, `headroom_retrieve` e `headroom_stats` diretamente para o ecossistema do Claude.

---

[Este vídeo sobre o Headroom](https://www.youtube.com/watch?v=03vi4ApFIZE) demonstra uma instalação prática passo a passo, detalha o pipeline de compressão e mostra o Headroom a intercetar em tempo real o tráfego do Claude Code para reduzir drasticamente os tokens consumidos.