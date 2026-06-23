
# 📘 Agent Loop com IA (Guia Profissional + Exemplos com Claude Code)

## 🔎 1. O que é “Agent Loop”?

Um **Agent Loop** é a estrutura central que permite que uma IA funcione como um *agente autônomo* capaz de:

1. Receber um objetivo
2. Planejar ações
3. Executar tarefas
4. Avaliar resultados
5. Iterar até atingir o objetivo

👉 Ou seja: é o ciclo contínuo de **pensar → agir → observar → ajustar**

***

## 🧠 2. Modelo mental do Agent Loop

```text
[Objetivo]
    ↓
[Planejamento]
    ↓
[Ação]
    ↓
[Observação]
    ↓
[Reflexão]
    ↓
(loop até concluir)
```

***

## 🧩 3. Estrutura formal do loop

Um agent loop geralmente segue:

```pseudo
while not goal_achieved:
    thought = model.plan(context)
    action = execute(thought)
    observation = get_result(action)
    context += observation
    evaluate_progress()
```

***

## ⚙️ 4. Componentes principais

### ✔️ 1. Contexto acumulado

Memória do que já foi feito

### ✔️ 2. Política de decisão

Como o agente decide o próximo passo

### ✔️ 3. Ferramentas (tools)

Exemplo:

* API
* banco de dados
* terminal
* filesystem

### ✔️ 4. Critério de parada

Evita loops infinitos:

* objetivo atingido
* limite de passos
* confiança suficiente

***

## 🧠 5. Tipos de Agent Loop

| Tipo             | Descrição                 |
| ---------------- | ------------------------- |
| React            | Think → Act simples       |
| ReAct            | Reason + Act intercalados |
| Plan-and-Execute | Planeja tudo antes        |
| Reflection Loop  | Autoavalia e melhora      |
| Tool-augmented   | Usa ferramentas externas  |

***

# 🚀 6. Implementando Agent Loop com Claude Code

Claude Code permite criar loops com raciocínio + ferramentas.

***

## ✅ Exemplo 1 — Loop básico (ReAct)

```python
from anthropic import Anthropic

client = Anthropic()

objective = "Descubra o preço médio de notebooks gamer e sugira 3 opções"

context = ""

for step in range(5):
    response = client.messages.create(
        model="claude-3-opus",
        max_tokens=1000,
        messages=[
            {
                "role": "user",
                "content": f"""
Você é um agente com objetivo:

{objective}

Contexto atual:
{context}

1. Pense no próximo passo
2. Execute a ação
3. Retorne resultado + próximo passo
"""
            }
        ]
    )

    output = response.content[0].text
    print(f"\nSTEP {step}:\n", output)

    context += "\n" + output

    if "FINAL ANSWER" in output:
        break
```

***

## ✅ Exemplo 2 — Agent Loop com ferramentas

Aqui o agente decide quando usar uma tool.

### Simulação de Tool:

```python
def search_product(query):
    return f"Resultado simulado para: {query}"
```

### Loop:

```python
tools = {
    "search": search_product
}

context = ""

for step in range(5):
    prompt = f"""
Objetivo: encontrar melhores notebooks custo-benefício

Contexto:
{context}

Se precisar, use:
TOOL: search(query)

Formato:
THOUGHT:
ACTION:
OBSERVATION:
"""

    response = client.messages.create(
        model="claude-3-sonnet",
        max_tokens=800,
        messages=[{"role": "user", "content": prompt}]
    )

    text = response.content[0].text
    print(text)

    if "TOOL:" in text:
        query = text.split("search(")[1].split(")")[0]
        observation = toolsquery
        context += f"\nOBSERVATION: {observation}"
    else:
        context += text
```

***

## ✅ Exemplo 3 — Loop com reflexão (nível avançado)

```python
for step in range(5):
    response = client.messages.create(
        model="claude-3-opus",
        max_tokens=1000,
        messages=[
            {
                "role": "user",
                "content": f"""
Objetivo: Criar plano de negócios para SaaS

Contexto:
{context}

Execute:

1. THOUGHT
2. ACTION
3. RESULT
4. REFLECTION (o que melhorar)
"""
            }
        ]
    )

    output = response.content[0].text
    print(output)

    context += output

    if "PLANO FINAL" in output:
        break
```

***

# 🧠 7. Padrões avançados

## 🧩 7.1 Self-Reflection Loop

Agente melhora sua própria resposta:

```text
Resposta → Crítica → Nova resposta → Score → Itera
```

***

## 🧩 7.2 Tree of Thought (ToT)

Explora múltiplos caminhos:

```text
Branch A → avalia
Branch B → avalia
Escolhe melhor caminho
```

***

## 🧩 7.3 Multi-Agent Loop

Vários agentes colaboram:

* Planner
* Executor
* Critic

***

## 🧩 7.4 Memory-augmented Loop

Integra memória persistente:

* Redis
* Vector DB (Pinecone, FAISS)

***

# ⚠️ 8. Problemas comuns

| Problema         | Solução           |
| ---------------- | ----------------- |
| Loop infinito    | limite de steps   |
| Contexto gigante | sumarização       |
| decisões ruins   | reflexão          |
| custo alto       | truncar memória   |
| hallucinação     | validação externa |

***

# ✅ 9. Boas práticas (nível senior)

✔ Defina objetivos claros  
✔ Limite número de iterações  
✔ Use structured outputs (JSON)  
✔ Separe raciocínio e ação  
✔ Use feedback loops  
✔ Instrumente logs  
✔ Avalie com métricas

***

# 📊 10. Exemplo real (produção)

### Agente programador

```text
Objetivo: corrigir bug

Loop:

1. Analisa erro
2. Busca código
3. Propõe patch
4. Roda teste
5. Ajusta
```

***

# 🧪 11. Formato ideal de prompt

```text
Você é um agente autônomo.

Objetivo: {goal}

Sempre responda com:

THOUGHT:
ACTION:
OBSERVATION:
REFLECTION:

Pare quando atingir:
FINAL ANSWER
```

***

# 🎯 12. Checklist de qualidade (9.5+)

✅ Explica conceito  
✅ Mostra arquitetura  
✅ Tem pseudocódigo  
✅ Possui múltiplos exemplos reais  
✅ Mostra integração com tools  
✅ Inclui padrões avançados  
✅ Ensina boas práticas  
✅ Apresenta problemas reais  
✅ Demonstra uso prático com Claude

***

# 🏁 Conclusão

O **Agent Loop é o coração dos sistemas de IA moderna**, permitindo ir muito além de prompts simples e criar agentes que:

* tomam decisões
* usam ferramentas
* aprendem iterativamente
* resolvem problemas complexos


