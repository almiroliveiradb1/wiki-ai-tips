# 🧠 Prompts de IA para PRD, SPEC, ADR e Implementação

Prompts otimizados (prontos para copiar e colar) para usar IA na criação de PRD, SPEC, ADR e IMPLEMENTAÇÃO — pensados para gerar respostas consistentes, completas e reutilizáveis no seu fluxo.

> 👉 Todos seguem um padrão profissional usado em times de produto + engenharia.

---

## 🧩 Prompt Base (recomendado usar sempre)

Antes de cada tipo, você pode usar esse wrapper:

```
Você é um especialista sênior em engenharia de software e arquitetura de sistemas.

Gere uma resposta clara, estruturada e prática, evitando explicações genéricas.
Se faltar informação, faça suposições razoáveis e explicite-as.

Use linguagem profissional e formatação em Markdown.
```

---

## 📄 1. Prompt para PRD

### ✅ Prompt principal

```
Você é um Product Manager experiente.

Crie um PRD (Product Requirements Document) completo para a seguinte ideia:

IDEIA:
[descreva aqui]

Inclua as seguintes seções:

1. Contexto e problema
2. Objetivo do produto
3. Personas e usuários
4. Jornada do usuário
5. Requisitos funcionais (com bullets claros)
6. Requisitos não funcionais (performance, segurança, escala, etc.)
7. Métricas de sucesso (KPIs)
8. Escopo (in-scope / out-of-scope)
9. Riscos e suposições

Regras:
- Seja específico e prático
- Evite generalizações
- Estruture como documento profissional
- Se necessário, proponha melhorias na ideia original
```

### 🔥 Prompt avançado (refinamento)

```
Revise esse PRD e:

1. Identifique lacunas ou ambiguidades
2. Sugira melhorias nos requisitos
3. Adicione edge cases não considerados
4. Avalie clareza e mensurabilidade das métricas

Retorne versão melhorada + lista de melhorias
```

---

## 📐 2. Prompt para SPEC

### ✅ Prompt principal

```
Você é um arquiteto de software sênior.

Com base no PRD abaixo, crie um documento técnico (SPEC):

PRD:
[cole aqui]

Inclua:

1. Resumo técnico da solução
2. Arquitetura (componentes e comunicação)
3. Diagrama textual da arquitetura
4. Definição de APIs (endpoints + payloads)
5. Modelo de dados (schemas)
6. Fluxos principais (step-by-step)
7. Edge cases
8. Estratégia de escalabilidade
9. Considerações de segurança
10. Plano de testes

Regras:
- Use linguagem técnica
- Seja detalhado, mas direto
- Faça suposições quando necessário e liste-as
- Evite soluções triviais; pense como sistema real
```

### 🔥 Prompt para aprofundar

```
Revise este SPEC e:

1. Identifique gargalos de performance
2. Avalie riscos de escala
3. Sugira melhorias arquiteturais
4. Aponte inconsistências entre PRD e SPEC

Explique de forma objetiva e acionável
```

---

## 📘 3. Prompt para ADR

### ✅ Prompt principal

```
Você é um arquiteto de software.

Com base no contexto abaixo, gere um ADR (Architecture Decision Record):

CONTEXTO:
[descreva situação ou decisão]

Use o formato:

# Título

## Contexto
Explique o problema e cenário

## Decisão
Descreva claramente o que foi escolhido

## Alternativas consideradas
Liste opções com prós e contras

## Consequências
- Positivas
- Negativas

## Status
(Proposto, Aceito, Deprecado)

Regras:
- Seja objetivo
- Foque em trade-offs
- Evite texto desnecessário
```

### 🔥 Prompt para decisões complexas

```
Compare as seguintes opções técnicas:

[opção A]
[opção B]
[opção C]

Considere:
- Performance
- Escalabilidade
- Custo
- Complexidade
- Manutenção

Recomende uma decisão final e gere um ADR completo
```

---

## ⚙️ 4. Prompt para Implementação

### ✅ Prompt principal (planejamento + código)

```
Você é um engenheiro de software sênior.

Com base no SPEC abaixo, gere:

1. Quebra em tarefas (task breakdown)
2. Ordem de implementação
3. Código inicial (boilerplate)
4. Exemplos de implementação das partes críticas
5. Testes unitários
6. Possíveis bugs e como evitar

SPEC:
[cole aqui]

Regras:
- Use boas práticas modernas
- Código limpo e organizado
- Explique decisões importantes
```

### 🔥 Prompt para geração incremental

```
Implemente apenas a seguinte parte:

[descrição da tarefa]

Regras:
- Código completo e funcional
- Inclua validações
- Inclua testes
- Não explique demais, foque no código
```

---

## 🤖 Prompts para Automação Completa (Pipeline)

### 🚀 Prompt ALL-IN-ONE

```
Você é um time completo (PM + Tech Lead + Engenheiro).

A partir da ideia abaixo:

[IDEIA]

Gere:

1. PRD
2. SPEC
3. Lista de ADRs necessários (com 1 ADR completo)
4. Plano de implementação
5. Estrutura de pastas do projeto

Organize em seções bem definidas.
```

---

## 🔍 Prompts para Revisão

### ✅ Auditoria geral

```
Revise todos os artefatos (PRD, SPEC, ADR, código) e:

1. Identifique inconsistências
2. Detecte riscos técnicos
3. Sugira simplificações
4. Aponte overengineering

Classifique severidade: alta, média, baixa
```

---

## 🧩 Prompts para Produtividade Real

### 🧷 Gerar tarefas para Jira/DevOps

```
Converta o SPEC em tarefas de desenvolvimento:

Para cada tarefa inclua:
- Título
- Descrição
- Critérios de aceite
- Estimativa (S, M, L)

Formato pronto para Jira
```

### 🔄 Converter PRD → backlog

```
Transforme esse PRD em backlog priorizado:

- Épicos
- User stories
- Critérios de aceite

Ordene por valor de negócio
```

---

## 🧱 Dica de Ouro (uso real)

Crie uma estrutura de pastas para reutilizar seus prompts:

```
/ai/prompts/
  prd.md
  spec.md
  adr.md
  impl.md
```

> 👉 Reutilize sempre — **consistência = qualidade**

---

## ✅ Resumo

Você agora tem:

- ✅ Prompt de criação
- ✅ Prompt de revisão
- ✅ Prompt de aprofundamento
- ✅ Pipeline completo com IA
- ✅ Prompt para tarefas reais

---

> **Próximos passos:** adapte esses prompts para seu stack (Java, Node, .NET, etc.), integre com GitHub Copilot / Azure DevOps ou crie um CLI interno para gerar tudo automaticamente.
