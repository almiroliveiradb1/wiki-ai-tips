# Guia de Testes Automatizados com IA

Guia de Testes Automatizados com Inteligência Artificial
A geração de testes com IA funciona como uma alavanca: ela amplifica a direção que você já escolheu. Sem diretrizes claras, a IA produzirá volume (centenas de testes redundantes); com a estratégia certa, ela entregará uma suíte de alta qualidade e baixa manutenção.
Abaixo está o passo a passo para estruturar seu projeto e extrair o valor real da IA no dia zero.
## Passo 1: Configurar a Infraestrutura no Dia Zero
Antes de interagir com qualquer LLM, o projeto deve possuir o ambiente mínimo de testes configurado e funcional.
Defina a Stack: Escolha e instale o framework de testes padrão (ex: JUnit, PyTest, Jest).
Crie um Teste "Hello World": Implemente um único teste simples que passe com sucesso no pipeline de CI/CD.
Objetivo: Estabelecer a referência técnica (convenções, imports e sintaxe) que a IA usará como exemplo.
## Passo 2: Estabelecer o Contrato Operacional
O framework configurado serve como o "contrato" do que a IA pode e não pode fazer. Delimite as fronteiras invisíveis do código:
Estilo de Escrita: Defina se o projeto adota BDD (Behavior-Driven Development) ou a estrutura tradicional AAA (Arrange, Act, Assert).
Mocks vs. Integração: Deixe claro se a IA deve mocar dependências externas (bancos de dados, APIs) ou se existem containers (como Testcontainers) disponíveis.
## Passo 3: Definir a Granularidade e a Estratégia Contextual
O nível de detalhe deve ser proporcional ao risco do negócio e ao custo de manutenção do software.
```
+-------------------------------------------------------------+
| Risco do Domínio (Ex: Bancário / Saúde)                     |
| --> Alta Rigidez | Alta Granularidade (Mais testes unitários)|
+-------------------------------------------------------------+
| Risco Controlado (Ex: MVP / CRUD Simples)                  |
| --> Abordagem Enxuta | Foco em Fluxos Críticos (Integração) |
+-------------------------------------------------------------+
```



Evite o excesso: Não peça para a IA testar getters, setters ou frameworks puros.
Foque no valor: Direcione o esforço para regras de negócio complexas, cálculos e fluxos de exceção.
## Passo 4: Mitigar o Risco de Falsa Segurança
Volume não é sinônimo de cobertura. Uma IA pode gerar dois mil testes de front-end que apenas validam se um botão renderiza, ignorando se o comportamento do clique funciona sob estresse.
Critério de Aceitação: Avalie o teste gerado pela relevância do cenário, não pela quantidade de linhas de código.
Revisão Humana: Trate o código gerado pela IA como o código de um desenvolvedor júnior; ele exige validação antes de ser integrado.
## Passo 5: Criar Instruções Claras (Prompts Estruturados)
Nunca utilize comandos genéricos como "Crie testes para esta classe". Em vez disso, forneça contexto, restrições e critérios explicitamente através de uma estrutura padronizada:
Template de Prompt para IA:
Contexto: "Esta classe implementa a regra de cálculo de juros do produto X."
Contrato: "Utilize o framework Y, seguindo o padrão AAA. Moke as chamadas da API de terceiros."
Granularidade: "Gere 3 cenários principais: fluxo de sucesso, entrada com valor negativo e timeout da API."
Critério: "Não gere testes para validações de tipagem já cobertas pelo compilador."
Seguindo esse fluxo, a automação com IA deixa de ser uma geradora de código descartável e passa a ser uma ferramenta estratégica de qualidade.

Explicação com Exemplos de realização de testes integrados
## 1. Fluxos de Navegação com IA - Por que precisam de instruções precisas
### ❌ Problema (sem instruções claras)
Solicitação vaga: "Faça um teste de cliente"
O agente repetirá:
## Passo 1: Abrir navegador
## Passo 2: Fazer login
## Passo 3: Ir até clientes
## Passo 4: Criar cliente
## Passo 5: Fazer login novamente ⚠️
## Passo 6: Ir até clientes novamente ⚠️
## Passo 7: Alterar cliente
### ✅ Solução (com instruções precisas)
Instrução clara:
"1. Você já está autenticado
2. Navegue para a tela de clientes
3. Crie um novo cliente com dados XYZ
4. Verifique se foi criado"
## 2. Reuso de Sessão e Cookies
Exemplo Prático: Fluxo de Compra
Cenário: Um teste precisa validar criar pedido + alterar pedido
FLUXO SEM REUSO (ineficiente):
```
┌─────────────────────────────┐
│ Teste 1: Criar Pedido       │
├─────────────────────────────┤
│ ✓ Login                     │
│ ✓ Navegar para Pedidos      │
│ ✓ Criar pedido              │
└─────────────────────────────┘
```

↓ Sessão perdida ❌
```
┌─────────────────────────────┐
│ Teste 2: Alterar Pedido     │
├─────────────────────────────┤
│ ✓ Login (repetido)          │ ⚠️ Desperdício
│ ✓ Navegar para Pedidos      │ ⚠️ Desperdício
│ ✓ Alterar pedido            │
└─────────────────────────────┘
```

COM REUSO (eficiente):
```
┌─────────────────────────────────┐
│ Teste 1: Criar Pedido           │
├─────────────────────────────────┤
│ ✓ Login                         │
│ ✓ Navegar para Pedidos          │
│ ✓ Criar pedido                  │
│ 🔒 Sessão + Cookies preservados │
└─────────────────────────────────┘
```

↓ Sessão mantida ✓
```
┌─────────────────────────────────┐
│ Teste 2: Alterar Pedido         │
├─────────────────────────────────┤
│ ✓ Usar cookie existente         │ ✅ Rápido
│ ✓ Ir direto para Pedidos        │ ✅ Eficiente
│ ✓ Alterar pedido                │
└─────────────────────────────────┘
```

## 3. Headless vs Headed
Exemplo Visual
```
╔════════════════════════════════════════════════════════╗
║                    HEADLESS (sem interface)            ║
╠════════════════════════════════════════════════════════╣
│  Terminal rodando teste                                │
│  playwright-cli open https://app.com                   │
│  playwright-cli type "#email" "usuario@email.com"      │
│  playwright-cli press "Enter"                          │
│  ✓ Rápido, sem poluição visual, usa menos RAM         │
║                                                        ║
║ Uso: CI/CD, suítes longas, ambiente servidor          ║
╚════════════════════════════════════════════════════════╝
╔════════════════════════════════════════════════════════╗
║                   HEADED (com interface)               ║
╠════════════════════════════════════════════════════════╣
│ ┌─────────────────────────────────────────────────┐   │
│ │ Chrome (automação)                              │   │
│ │ ┌────────────────────────────────────────────┐  │   │
│ │ │ Login                                      │  │   │
│ │ │ Email: usuario@email.com ← Digitação      │  │   │
│ │ │ Senha: ****                               │  │   │
│ │ │ [Login]                                    │  │   │
│ │ └────────────────────────────────────────────┘  │   │
│ │                                                  │   │
│ │ ✓ Visualização em tempo real                    │   │
│ │ ✓ Fácil de depurar                             │   │
│ └─────────────────────────────────────────────────┘   │
│                                                        │
│ Uso: Debug, desenvolvimento, confirmar comportamento │
╚════════════════════════════════════════════════════════╝
```

## 4. Playwright como Base
Exemplo: Script Tradicional vs Abordagem com Fluxo
// ❌ Script gravado (frágil)
const { chromium } = require('playwright');
(async () => {
const browser = await chromium.launch();
const page = await browser.newPage();

await page.goto('https://app.com/login');
await page.click('input[id="email"]');
await page.type('input[id="email"]', 'user@mail.com');
// Se o ID mudar, o teste quebra ❌
await page.click('button:has-text("Login")');

await browser.close();
})();
// ✅ Abordagem orientada a fluxo (resiliente)
// Descrição: "Validar login de usuário"
// O agente entende a TAREFA, não apenas o script
FLUXO: Autenticar Usuário
```
├─ Ir para tela de login
├─ Inserir credenciais
├─ Confirmar autenticação
└─ Validar redirecionamento para dashboard
```

## 5. Playwright CLI vs MCP
Comparação Prática
```
┌──────────────────────────────────────────────────────┐
│ PLAYWRIGHT + MCP (Pesado mas Rico)                   │
├──────────────────────────────────────────────────────┤
│ • Carrega: descrições, tools, metadados              │
│ • Contexto consumido ANTES do teste                  │
│ • Custo: ~5000 tokens só de inicialização            │
│ • Benefício: Rich features, visibilidade completa   │
│ • Uso ideal: Testes complexos com múltiplos fluxos  │
│                                                      │
│ Exemplo de contexto carregado:                       │
│ {                                                    │
│   "mcp_server": "playwright",                        │
│   "tools": [100+ funções disponíveis],              │
│   "capabilities": {...},                            │
│   "metadata": {...}                                 │
│ }                                                    │
└──────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────┐
│ PLAYWRIGHT CLI + SKILL (Leve e Prático)              │
├──────────────────────────────────────────────────────┤
│ • Carrega: Skill apenas quando necessário            │
│ • Contexto consumido DURANTE execução                │
│ • Custo: ~1000 tokens (bem mais barato)             │
│ • Benefício: Simples, direto, sem overhead          │
│ • Uso ideal: Testes simples, CI/CD, suítes longas  │
│                                                      │
│ Exemplo de comando:                                 │
│ $ playwright-cli open https://app.com               │
│ $ playwright-cli type "#email" "user@mail.com"      │
│ $ playwright-cli press "Enter"                      │
│ $ playwright-cli wait-for-element "h1:Dashboard"    │
└──────────────────────────────────────────────────────┘
```

## 6. Desativação de MCPs Desnecessários
Exemplo de Economia de Tokens
ATIVADO:
```
┌────────────────┐
│ MCP Playwright │ → +2000 tokens
├────────────────┤
│ MCP Figma      │ → +1500 tokens
├────────────────┤
│ MCP Asana      │ → +1800 tokens
├────────────────┤
│ MCP Slack      │ → +1200 tokens
└────────────────┘
```

Total: +6500 tokens POR CONVERSA
DESATIVADO (apenas necessários):
```
┌────────────────┐
│ MCP Playwright │ → +2000 tokens
└────────────────┘
  Total: +2000 tokens POR CONVERSA
```

Economia: 4500 tokens = ~30% de redução
## 7. Skills como Camada Operacional
Exemplo de Skill
# skill-playwright-cli.md
## Comandos Disponíveis
### Abrir página
playwright-cli open <URL>
Exemplo: playwright-cli open https://app.com
### Digitar em campo
playwright-cli type <selector> <texto>
Exemplo: playwright-cli type "#email" "user@mail.com"
### Pressionar tecla
playwright-cli press <key>
Exemplo: playwright-cli press "Enter"
### Esperar elemento
playwright-cli wait-for-element <selector> [timeout]
Exemplo: playwright-cli wait-for-element "h1:Dashboard" 5000
### Validar elemento visível
playwright-cli assert-visible <selector>
Exemplo: playwright-cli assert-visible ".success-message"
Como o agente usa:
"Instruções claras do que fazer"
↓
Agente consulta skill
↓
Encontra comando apropriado
↓
Executa com baixo overhead
## 8. Instalação e Uso do Playwright CLI
Passo a Passo
# ✓ Passo 1: Instalar Playwright CLI correto
npm install @playwright/cli@latest
# ✓ Passo 2: Verificar ajuda
npx playwright-cli help
# ✓ Passo 3: Instalar skill (opcional)
playwright-cli-install-skill
# ✓ Passo 4: Usar em teste
playwright-cli open https://seu-app.com
playwright-cli type "#login" "usuario"
playwright-cli press "Enter"
playwright-cli wait-for-element ".dashboard" 5000
❌ Erros Comuns:
# Errado: confundir com Playwright tradicional
npm install playwright  # ← Isso é diferente!
# Errado: usar comandos do Playwright tradicional
npx playwright test     # ← Não funciona com CLI
# Correto:
npm install @playwright/cli@latest
npx playwright-cli open ...  # ← Comando certo
## 9. Sessões no Playwright CLI
Exemplo: Fluxo com Sessão Persistente
# Passo 1: Criar nova sessão
playwright-cli session create "minha_sessao"
# Saída: ID da sessão criada
# Passo 2: Executar ações NA SESSÃO
playwright-cli open https://app.com --session minha_sessao
playwright-cli type "#email" "user@mail.com"
playwright-cli press "Enter"
playwright-cli wait-for-element ".dashboard"
# Agora cookies e autenticação estão SALVOS
# A sessão permanece ativa
# Passo 3: Reusar MESMA sessão depois
playwright-cli open https://app.com/clientes --session minha_sessao
# ✓ Já está logado! Não precisa fazer login novamente
# Passo 4: Fechar quando terminar
playwright-cli session delete "minha_sessao"
Resumo Visual do Fluxo Completo
```
┌─────────────────────────────────────────────────────┐
│ 1. PLANEJAMENTO: Instruções claras do que fazer     │
├─────────────────────────────────────────────────────┤
│ 2. SETUP: Criar sessão reutilizável                 │
├─────────────────────────────────────────────────────┤
│ 3. EXECUÇÃO: Playwright CLI (leve) ou MCP (rico)   │
│    ├─ Headless no CI/CD                             │
│    └─ Headed para debug                             │
├─────────────────────────────────────────────────────┤
│ 4. SKILL: Guia operacional para o agente            │
├─────────────────────────────────────────────────────┤
│ 5. REUTILIZAÇÃO: Manter sessão entre fluxos         │
├─────────────────────────────────────────────────────┤
│ 6. RESULTADO: Testes rápidos, eficientes, baratos  │
└─────────────────────────────────────────────────────┘
```


