# Harness Engineering

Harness Engineering é a disciplina de criar limites, ferramentas e condições de execução para que um modelo de IA opere dentro de um ambiente controlado. Em vez de tentar "melhorar a inteligência" do modelo, essa prática foca em dar forma operacional ao comportamento esperado, minimizando alucinações e aumentando a aderência entre o que o usuário pede e o que a máquina produz.

> **Princípio central:** `Agente = Modelo + Harness`
>
> "Harness" engloba tudo ao redor do LLM: infraestrutura, contexto, restrições e ferramentas de apoio.

---

## Por que o Harness é necessário?

Modelos de IA são sistemas **probabilísticos** — não garantem 100% de obediência e podem desviar do objetivo se deixados totalmente livres. O Harness troca a improvisação da IA por controle sistêmico.

**Exemplo sem Harness:**
```
Usuário: "Crie um endpoint REST para usuários."
IA: Cria o endpoint usando um padrão diferente do projeto, sem autenticação,
    com nomes de variáveis inconsistentes e sem testes.
```

**Exemplo com Harness:**
```
[CLAUDE.md define: padrão REST com JWT, snake_case, cobertura mínima 80%]

Usuário: "Crie um endpoint REST para usuários."
IA: Cria o endpoint seguindo o padrão do projeto, com middleware JWT,
    nomenclatura snake_case e suite de testes incluída.
```

---

## Mecanismos de Controle do Harness

### 1. Guias — Feedforward

Antecipam e orientam as ações da IA **antes** que ela gere código. Diminuem a ambiguidade na primeira tentativa.

**Exemplos de feedforward:**
- Arquivos de configuração (`CLAUDE.md`, `AGENTS.md`) com convenções do projeto
- Especificações arquiteturais detalhadas antes de implementar
- Skills operacionais que descrevem o fluxo esperado

```markdown
<!-- CLAUDE.md -->
## Convenções de Código
- Sempre use TypeScript strict mode
- Funções assíncronas devem usar async/await, nunca .then()
- Cada módulo novo precisa de um arquivo `.spec.ts` correspondente
```

---

### 2. Sensores — Feedback

Observam o comportamento da IA **depois** que ela atua, criando um loop de auto-correção sem intervenção humana.

**Exemplos de feedback:**
- Mensagens de erro customizadas que instruem a IA a corrigir a própria falha
- Hooks pós-execução que rodam linters e retornam o resultado ao agente
- Testes automatizados que bloqueiam o avanço se falharem

```bash
# Hook pós-edição que retorna feedback direto ao agente
#!/bin/bash
npx eslint "$FILE" --format=compact 2>&1
# A saída do lint vira contexto para o agente corrigir automaticamente
```

---

### 3. Controles Computacionais vs. Inferenciais

| Tipo | Como funciona | Exemplos |
|------|---------------|----------|
| **Computacional** | Validadores rápidos, determinísticos, executados por CPU | Linters, type checkers, testes unitários |
| **Inferencial** | O próprio LLM atua como "juiz" avaliando qualidade semântica | Code review por agente, avaliação de arquitetura |

**Exemplo de controle inferencial:**
```markdown
<!-- Rubrica para o agente avaliador -->
Avalie o código gerado nos seguintes critérios (1-5):
- Segue as convenções do CLAUDE.md?
- Tem cobertura de testes adequada?
- Introduz dívida técnica?
Se qualquer critério < 3, rejeite e explique o motivo.
```

---

### 4. Mediação de Acesso — Sandboxing e Permissões

O Harness separa o "cérebro" (modelo lógico) do "corpo" (ambiente de atuação), definindo estritamente quais recursos a IA pode acessar.

**Exemplos de sandboxing:**
```jsonc
// .claude/settings.json
{
  "permissions": {
    "allow": [
      "Bash(npm run test)",
      "Bash(npm run lint)",
      "Read(**)"
    ],
    "deny": [
      "Bash(git push)",
      "Bash(rm -rf*)"
    ]
  }
}
```

---

### 5. Unidades Menores e Verificáveis

O Harness impede processos invisíveis e exige que o trabalho seja fragmentado em **marcos verificáveis objetivamente** — cada etapa passa por um gate de qualidade antes de avançar.

**Exemplo de task atômica:**
```markdown
<!-- tasks.md -->
## Task 1.3 — Criar modelo User
- [ ] Definir interface TypeScript em `src/models/user.ts`
- [ ] Implementar validação Zod em `src/schemas/user.schema.ts`
- [ ] Escrever testes em `src/models/user.spec.ts`

**Gate de qualidade:** `npm run test -- user` deve passar com 100% antes de avançar.
```

---

## Camadas do Harness

```
┌─────────────────────────────────────────────────┐
│              User Harness (customizado)          │
│  CLAUDE.md · Skills · Hooks · MCP Servers        │
│  Scripts de validação · Rubricas de negócio      │
├─────────────────────────────────────────────────┤
│         General-purpose Harness (embutido)       │
│  Cursor · GitHub Copilot · Claude Code           │
│  Persistência de contexto · Segurança base       │
├─────────────────────────────────────────────────┤
│                    LLM (Modelo)                  │
└─────────────────────────────────────────────────┘
```

- **General-purpose Harness:** já vem embutido em IDEs e assistentes modernos — provê persistência de contexto e infraestrutura de segurança base.
- **User Harness:** camada customizada criada pelo desenvolvedor, acoplando processos de validação de negócio, scripts e convenções específicas do projeto.

---

## CLAUDE.md — Guia de Comportamento do Agente

O `CLAUDE.md` orienta o agente, mas **não deve** ser o depósito total do estado do projeto. Ele funciona como um **índice** (Progressive Disclosure), apontando para as fontes certas sob demanda.

**O que colocar no CLAUDE.md:**
```markdown
# Projeto X

## Stack
- Backend: Node.js + TypeScript + Fastify
- Banco: PostgreSQL com Prisma ORM
- Testes: Vitest

## Convenções
Ver [CONVENTIONS.md](.specs/codebase/CONVENTIONS.md)

## Estado atual do projeto
Ver [STATE.md](.specs/project/STATE.md) antes de qualquer implementação.

## Como rodar
npm run dev      # servidor local
npm run test     # suite de testes
npm run lint     # verificação de estilo
```

**O que NÃO colocar:**
- Histórico completo de decisões arquiteturais (use ADRs separados)
- Regras de negócio detalhadas de cada módulo (use docs específicos)
- Lista de bugs e bloqueios (use STATE.md)

---

## CLAUDE.md vs AGENTS.md

No contexto de Harness Engineering, os dois arquivos são **funcionalmente equivalentes** — diferem apenas na preferência de nomenclatura por IDE ou framework:

| Aspecto | CLAUDE.md | AGENTS.md |
|---------|-----------|-----------|
| Usado por | Claude Code, Cursor | OpenAI Agents, outros |
| Função | Guia de feedforward | Guia de feedforward |
| Limitações | Não suporta complexidade total | Não suporta complexidade total |
| Papel ideal | Índice → aponta para docs | Índice → aponta para docs |

> Não importa o nome — ambos representam a mesma prática: um artefato estático para dar direção inicial ao modelo e integrá-lo ao ambiente controlado.

---

## Estrutura de Arquivos do Harness

A estrutura evolui conforme o projeto cresce de **Greenfield** (novo) para **Brownfield** (maduro):

```text
.specs/
├── project/
│   ├── PROJECT.md        # Visão geral e objetivos do projeto
│   ├── ROADMAP.md        # Planejamento de features e marcos
│   └── STATE.md          # Memória persistente: decisões, bloqueios, lições
│
├── codebase/             # Para projetos existentes (Brownfield)
│   ├── STACK.md          # Tecnologias e versões utilizadas
│   ├── ARCHITECTURE.md   # Diagrama e decisões arquiteturais
│   ├── CONVENTIONS.md    # Padrões de código e nomenclatura
│   ├── STRUCTURE.md      # Mapa de pastas e responsabilidades
│   ├── TESTING.md        # Estratégia e padrões de teste
│   ├── INTEGRATIONS.md   # APIs e serviços externos
│   └── CONCERNS.md       # Dívidas técnicas e áreas de risco
│
├── features/             # Especificações por funcionalidade
│   └── [feature-name]/
│       ├── spec.md       # Requisitos e critérios de aceite
│       ├── context.md    # Decisões para resolver ambiguidades
│       ├── design.md     # Arquitetura e componentes da feature
│       └── tasks.md      # Tarefas atômicas e verificáveis
│
└── quick/                # Tarefas rápidas e correções de bugs
    └── NNN-slug/
        ├── TASK.md       # Descrição e critério da tarefa
        └── SUMMARY.md    # Resultado e decisões tomadas
```

**Exemplo de `features/auth/spec.md`:**
```markdown
# Feature: Autenticação JWT

## Critérios de aceite
- [ ] Login com email + senha retorna token JWT válido por 24h
- [ ] Token expirado retorna 401 com mensagem clara
- [ ] Refresh token renova sem re-login por até 7 dias
- [ ] Tentativas de brute-force bloqueadas após 5 falhas

## Fora do escopo
- Login social (OAuth) — planejado para v2
- 2FA — planejado para v2
```

---

## STATE.md — Memória Persistente do Agente

O `STATE.md` é o **artefato central de estado** do projeto. Garante continuidade entre sessões — qualquer agente novo consulta este arquivo para um "onboarding rápido" e sabe exatamente de onde continuar.

### Por que é necessário?

As sessões dos agentes são **efêmeras** — morrem ao final de cada execução. Qualquer informação mantida apenas no contexto temporário desaparece junto.

### O que o STATE.md registra:

```markdown
# STATE.md — Estado do Projeto X

## Última atualização: 2025-06-20

## ✅ Implementado e funcionando
- Autenticação JWT (login + refresh token)
- CRUD de usuários com validação Zod
- Pipeline CI/CD no GitHub Actions

## 🚧 Em progresso
- [ ] Feature: Upload de avatar (50% — falta integração S3)
- [ ] Testes de integração para módulo de pagamento

## ❌ Bloqueios
- SDK do gateway de pagamento sem suporte a TypeScript 5.x
  → Aguardando release 3.2.0 (previsto: 2025-07-01)

## 🧠 Decisões tomadas
- Escolhemos Fastify sobre Express por benchmarks de performance
- Prisma em vez de TypeORM por melhor suporte a migrações

## 💡 Ideias adiadas
- Cache com Redis (avaliar após MVP)
- Rate limiting por IP (próxima sprint)
```

### Como o STATE.md funciona como contrato:

```
Agente A implementa feature
        ↓
Marca como ✅ no STATE.md
        ↓
Agente B (avaliador) lê STATE.md
        ↓
Verifica se feature passa nos critérios definidos
        ↓
Aprova ou reporta falha de volta ao STATE.md
```

> O formato pode variar (Markdown ou SQLite), mas o princípio é invariável: prover um ponto de partida **persistente e confiável** para retomada do trabalho, impedindo perda de continuidade entre sessões.

---

## Resumo: O que faz um bom Harness?

| Componente | Função | Sem ele |
|------------|--------|---------|
| `CLAUDE.md` | Orienta comportamento inicial | IA improvisa padrões |
| `STATE.md` | Continuidade entre sessões | IA recomeça do zero |
| Hooks de feedback | Auto-correção sem humano | Erros acumulam silenciosamente |
| Testes como gate | Impede avanço com falhas | Dívida técnica invisível |
| Permissões restritas | Isola risco operacional | IA pode causar danos irreversíveis |
| Tasks atômicas | Trabalho verificável | Progresso ambíguo e incontrolável |
