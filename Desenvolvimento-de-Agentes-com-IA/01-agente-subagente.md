## ✅ 1. O que é um agente e um subagente

* Um **agente** é o sistema principal que executa uma tarefa (ex: um assistente que gera código).
* Um **subagente** é um “mini agente” que:
  * roda dentro do agente principal
  * faz uma tarefa específica
  * e depois devolve o resultado

👉 Pense assim:

* Agente principal = “chefe”
* Subagentes = “especialistas”

***

## ✅ 2. Por que usar subagentes?

À medida que um agente cresce, ele fica:

* grande
* complexo
* difícil de testar
* caro (mais tokens)
* lento (mais contexto)

Então, a solução é **quebrar o agente em partes menores**, delegando tarefas para subagentes.

***

## ✅ 3. Analogia (muito importante)

O texto compara com:

### 💻 Desenvolvimento de software

* Um sistema monolítico → vira microserviços
* Uma classe enorme → vira várias classes menores

👉 Mesma ideia:

> Dividir algo grande em partes menores e especializadas

***

# 🔧 Exemplos práticos

## 🧪 Exemplo 1: Assistente que planeja uma feature

### Sem subagente:

O agente faz tudo sozinho:

1. Pesquisa sobre o problema
2. Analisa soluções
3. Cria plano
4. Gera código

👉 Problemas:

* Muito contexto
* Mais custo
* Difícil testar

***

### ✅ Com subagente:

**Agente principal (coordenador):**

* gerencia tudo

**Subagente de pesquisa:**

* busca informações na web
* resume os dados

👉 Fluxo:

```
Usuário → Agente principal
        → Subagente de pesquisa
        → Resultado resumido
        → Agente principal decide e responde
```

✅ Vantagem:

* o histórico da pesquisa NÃO polui o contexto principal

***

## ⚡ Exemplo 2: Uso de diferentes modelos (economia)

Você pode usar modelos diferentes:

* Subagente: modelo barato (ex: pesquisa simples)
* Agente principal: modelo mais poderoso

👉 Resultado:

* economia de tokens 💰
* mais eficiência

***

## ⚡ Exemplo 3: Execução paralela

Se você tem 2 tarefas:

* Pesquisa técnica
* Pesquisa de mercado

👉 Com subagentes:

* os dois rodam ao mesmo tempo

✅ Resultado:

* resposta mais rápida

***

## 🧪 Exemplo 4: Testes

Sem subagente:

* difícil testar partes isoladas

Com subagente:

* você testa só o subagente de pesquisa

👉 Exemplo:

* medir qualidade de respostas
* medir consumo de tokens
* comparar modelos

***

## 🔁 Exemplo 5: Reuso

Imagine vários agentes:

* agente de suporte
* agente de planejamento
* agente de análise

Todos precisam de pesquisa.

👉 Solução:

* cria **1 subagente de pesquisa**
* reutiliza em todos

***

# ⚠️ Quando NÃO usar subagentes

O texto também alerta 🚨

Nem sempre vale a pena.

## ❌ Casos onde NÃO usar:

* agente pequeno e simples
* pouca complexidade
* sem ganho real

## ❌ Problemas possíveis:

* mais latência
* maior custo de tokens
* pior qualidade (dependendo do modelo usado)

***

# 💡 Regra importante do texto

👉 **O subagente precisa se justificar**

Não faça isso:

> “vou pegar 2 linhas e virar um subagente”

Faça isso:

1. Crie o agente primeiro
2. Teste
3. Veja gargalos
4. Só depois divida

***

# 📌 Resumo final

### ✔️ Subagentes servem para:

* dividir complexidade
* melhorar testes
* economizar contexto
* permitir paralelismo
* reutilizar lógica

### ❗ Mas:

* não use sem necessidade
* sempre avalie custo vs benefício

infografico ![alt text](Agentes_e_Subagentes_na_IA.png)