# Figma Local com Claude Code (MCP)


Aqui está um documento completo, organizado e prático , incluindo passo a passo + explicações + dicas reais de uso:
### 📘 Guia: Figma Local + Claude Code (MCP) — Instalação e Uso
### 🧩 Visão geral
O Figma pode ser integrado ao Claude Code via MCP (Model Context Protocol) em dois modos:
| Modo | Capacidades | Uso ideal |
|------|-------------|-----------|
| Local | Apenas leitura | Consultar design |
| Remoto (plugin) | Leitura + escrita | Criar e editar design |
➡️ No modo local, o Figma funciona como uma fonte de contexto.
➡️ No modo remoto, o AI atua como um “usuário completo” dentro do Figma.
### ⚙️ Pré-requisitos
Antes de começar:
- ✅ Figma Desktop instalado (Mac ou Windows)
- ✅ Claude Code instalado
- ✅ Conta no Figma
⚠️ Importante:
Figma local não funciona no Linux
O app desktop precisa estar aberto o tempo todo
### 🪜 PASSO A PASSO — Instalar Figma Local no Claude Code
### 1. Instalar o Figma Desktop
Baixe o Figma Desktop
Instale normalmente
Faça login
👉 Esse passo é obrigatório para o MCP local funcionar.
2. Ativar o servidor local no Figma
Dentro do Figma Desktop:
Abra qualquer arquivo
Ative o Dev Mode
No painel direito, habilite:

```
Enable Desktop Server
```


✅ Isso faz o Figma criar um servidor local:

```
http://localhost:3845
```


➡️ Esse endpoint será usado pelo Claude Code
3. Configurar o MCP local no Claude Code
Abra o arquivo de config do Claude Code (settings.json) e adicione:

```
{
  "mcpServers": {
    "figma-local": {
      "type": "http",
      "url": "http://localhost:3845"
    }
  }
}
```


✅ Características dessa configuração:
Não precisa autenticação
Usa HTTP local
Conecta direto ao Figma Desktop
4. Desabilitar o plugin do Figma (se existir)
Se você instalou o plugin oficial:
Rode no Claude Code:

```
/mcp
```


Localize o MCP do Figma (plugin)
Execute:

```
disable
```


⚠️ Motivo:
O Claude Code prioriza o plugin remoto — pode ignorar o local.
5. Reiniciar Claude Code
Sempre reinicie para garantir que:
O MCP local foi carregado
Não há conflito com plugin
6. Verificar se está funcionando
Digite:

```
/mcp
```


Você deve ver:
### ✅ figma-local ativo
### ✅ tools disponíveis
### 🧠 Como usar na prática
### ✅ Exemplo 1 — Ler dados do Figma
Você pode pedir:

```
Descreva os componentes dessa tela do Figma
```


O Claude irá:
Consultar o Figma local
Trazer hierarchy, estilos, spacing
### ✅ Exemplo 2 — Inspecionar UI

```
Quais cores e tipografia estão sendo usadas?
```


### ✅ Exemplo 3 — Gerar código

```
Gere um componente React baseado nesse layout
```


➡️ Aqui o MCP local fornece o design, e o Claude gera o código.
### ⚠️ Limitações do Figma Local
### ❌ Não cria elementos no Figma
### ❌ Não altera design
### ✅ Apenas leitura (contexto)
➡️ Isso é esperado:
O modo local é um “assistente observador”.
### 🚀 Dicas importantes (muito úteis)
### 💡 1. Use local para performance
Menos tokens
Mais rápido
Melhor para análise
### 💡 2. Desative quando não usar

```
/mcp → disable figma
```


### ✅ Economiza contexto
### ✅ Evita consumo desnecessário
### 💡 3. Combine local + remoto estrategicamente
Fluxo ideal:
Use local → entender design
Use remoto → modificar
### 💡 4. Prefira escopo de projeto
Evite instalar global:
✔ Melhor organização
✔ Menos poluição
✔ Controle por projeto
### 💡 5. Skills fazem diferença
Sem plugin:
Você precisa instalar skills manualmente
Com plugin:
Já vem tudo pronto
➡️ Skills ajudam o agente a entender como usar o Figma
### 💡 6. Sempre mantenha o Figma aberto
Se o app fechar:
### 🚫 MCP local para de funcionar
### 🆚 Comparação rápida
| Característica | Local | Plugin (remoto) |
|----------------|-------|-----------------|
| Leitura | ✅ | ✅ |
| Escrita | ❌ | ✅ |
| Precisa Figma aberto | ✅ | ❌ |
| Autenticação | ❌ | ✅ |
| Nº de tools | Poucas | Muitas (~19) |
[MCP figma | Txt]
### ✅ Conclusão
O Figma Local via MCP é ideal para:
Inspecionar design
Gerar código baseado no layout
Reduzir uso de tokens
Já o Plugin remoto é melhor para:
Criar telas
Automatizar design
Fazer edições diretamente



