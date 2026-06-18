# Claude Code CLI — Guia Completo de Comandos

Documentação detalhada de todos os comandos disponíveis na Claude Code CLI com exemplos práticos.

---

## 1. Instalação e Setup

### Instalar Claude Code CLI

```bash
# Via npm
npm install -g @anthropic-ai/claude-code

# Via pip (alternativa)
pip install claude-code
```

### Verificar versão instalada

```bash
claude-code --version
# Saída: claude-code v1.x.x

claude-code -v
# Saída: v1.x.x
```

### Obter ajuda geral

```bash
claude-code --help
# ou
claude-code -h
# Mostra todos os comandos disponíveis com suas descrições
```

---

## 2. Comandos Principais

### 2.1 `claude-code init`

Inicializa um novo projeto Claude Code no diretório atual.

```bash
# Inicializar com configurações padrão
claude-code init

# Com flags customizadas
claude-code init --name "meu-projeto" --type typescript

# Interativo (recomendado para iniciantes)
claude-code init --interactive
```

**O que ele cria:**
- `.claudecode/config.json` - Configurações do projeto
- `.claudecode/prompts/` - Diretório de prompts customizados
- `claude.json` - Manifest do projeto

---

### 2.2 `claude-code run`

Executa scripts ou tarefas com assistência do Claude.

```bash
# Executar script simples
claude-code run "script.js"

# Executar com contexto customizado
claude-code run "script.py" --context "Use Python 3.11"

# Executar com variáveis de ambiente
claude-code run "script.sh" --env="NODE_ENV=production"

# Executar de forma assíncrona
claude-code run "long-task.js" --async

# Executar com timeout
claude-code run "task.js" --timeout 300
```

**Exemplos práticos:**

```bash
# Executar build do projeto
claude-code run "npm run build"

# Executar testes
claude-code run "npm test" --env="TEST_ENV=true"

# Executar script com debug
claude-code run "debug-script.js" --verbose
```

---

### 2.3 `claude-code build`

Compila ou constrói o projeto com otimizações inteligentes.

```bash
# Build padrão
claude-code build

# Build com modo de desenvolvimento
claude-code build --dev

# Build com modo de produção
claude-code build --prod

# Build específico de um arquivo
claude-code build ./src/main.ts

# Build com verbose
claude-code build --verbose

# Build sem cache
claude-code build --no-cache
```

**Exemplos:**

```bash
# Build TypeScript para JavaScript
claude-code build --target es2020

# Build com otimizações
claude-code build --prod --minify

# Build com source maps
claude-code build --dev --source-maps
```

---

### 2.4 `claude-code deploy`

Realiza deploy da aplicação para diferentes plataformas.

```bash
# Deploy padrão
claude-code deploy

# Deploy para plataforma específica
claude-code deploy --platform vercel

# Deploy com configurações customizadas
claude-code deploy --platform aws --region us-east-1

# Deploy com variáveis de ambiente
claude-code deploy --env-file .env.production

# Deploy em staging (teste)
claude-code deploy --staging

# Deploy com aprovação
claude-code deploy --require-approval
```

**Exemplos por plataforma:**

```bash
# Vercel
claude-code deploy --platform vercel --project-id abc123

# AWS Lambda
claude-code deploy --platform aws-lambda --function-name my-function

# Docker
claude-code deploy --platform docker --registry docker.io

# Heroku
claude-code deploy --platform heroku --app my-app
```

---

### 2.5 `claude-code generate`

Gera código, arquivos ou estruturas baseado em descrição em linguagem natural.

```bash
# Gerar componente React
claude-code generate "componente React de botão com temas"

# Gerar API endpoint
claude-code generate "api endpoint GET /users com validação"

# Gerar teste unitário
claude-code generate --test "função de autenticação"

# Gerar estrutura de projeto
claude-code generate --project "projeto Next.js com autenticação"

# Gerar com file específico
claude-code generate "função em TypeScript" --output utils/helper.ts

# Gerar com contexto
claude-code generate "modelo de dados" --context "banco de dados PostgreSQL"
```

**Exemplos práticos:**

```bash
# Componente React
claude-code generate "componente React com hooks para gerenciar formulário de login"

# Função utilitária
claude-code generate "função JavaScript para validar email e telefone"

# Classe Python
claude-code generate "classe Python para conectar ao MongoDB com retry"

# Schema GraphQL
claude-code generate "schema GraphQL para usuários e posts"
```

---

### 2.6 `claude-code refactor`

Refatora código existente melhorando qualidade, performance e legibilidade.

```bash
# Refatorar arquivo
claude-code refactor ./src/app.js

# Refatorar pasta inteira
claude-code refactor ./src --recursive

# Refatorar com foco específico
claude-code refactor ./src --focus "performance"

# Refatorar com padrão específico
claude-code refactor ./src --pattern "component-design"

# Refatorar sem modificar original
claude-code refactor ./src --dry-run

# Refatorar com validação automática
claude-code refactor ./src --validate
```

**Exemplos:**

```bash
# Melhorar performance
claude-code refactor ./src/utils.js --focus "performance"

# Aplicar TypeScript
claude-code refactor ./src --pattern "typescript-migration"

# Melhorar legibilidade
claude-code refactor ./src/components --focus "readability"

# Atualizar padrões obsoletos
claude-code refactor ./src --pattern "modern-js"
```

---

### 2.7 `claude-code test`

Executa, gera ou gerencia testes automatizados.

```bash
# Executar todos os testes
claude-code test

# Executar teste específico
claude-code test ./tests/user.test.js

# Executar com coverage
claude-code test --coverage

# Gerar testes automaticamente
claude-code test --generate "src/utils.js"

# Executar com framework específico
claude-code test --framework jest

# Executar em watch mode
claude-code test --watch

# Executar com timeout
claude-code test --timeout 30000
```

**Exemplos:**

```bash
# Gerar testes para uma função
claude-code test --generate "src/calculateDiscount.js" --framework jest

# Executar com coverage detalhado
claude-code test --coverage --report html

# Executar testes de integração
claude-code test ./tests/integration --timeout 60000

# Watch mode durante desenvolvimento
claude-code test --watch --verbose
```

---

### 2.8 `claude-code analyze`

Analisa código, projeto ou arquivos para identificar problemas e sugestões.

```bash
# Analisar arquivo
claude-code analyze ./src/app.js

# Analisar projeto inteiro
claude-code analyze ./

# Análise de segurança
claude-code analyze ./src --security

# Análise de performance
claude-code analyze ./src --performance

# Análise de qualidade
claude-code analyze ./src --quality

# Gerar relatório
claude-code analyze ./src --report

# Com nível de detalhe
claude-code analyze ./src --detail=high
```

**Exemplos:**

```bash
# Verificar segurança do código
claude-code analyze ./src --security --report

# Performance analysis
claude-code analyze ./src/queries.js --performance --detail=high

# Análise completa
claude-code analyze ./ --security --performance --quality --report

# Verificar dependências problemáticas
claude-code analyze ./package.json --security
```

---

### 2.9 `claude-code debug`

Auxilia na depuração de código com assistência inteligente.

```bash
# Debug de arquivo
claude-code debug ./src/app.js

# Debug interativo
claude-code debug ./src/app.js --interactive

# Debug com breakpoint
claude-code debug ./src/app.js --breakpoint=25

# Debug com contexto de erro
claude-code debug ./src/app.js --error="TypeError: undefined"

# Debug de teste falhando
claude-code debug --test "./tests/user.test.js"

# Debug com stack trace
claude-code debug --stack-trace "path/to/error.log"
```

**Exemplos:**

```bash
# Debug interativo (recomendado)
claude-code debug ./src/auth.js --interactive

# Debug de erro específico
claude-code debug ./src/api.js --error="Cannot read property 'id' of undefined"

# Debug com breakpoint
claude-code debug ./src/app.js --breakpoint=45 --verbose

# Investigar teste falhando
claude-code debug --test "./tests/validation.test.js" --interactive
```

---

### 2.10 `claude-code lint`

Valida e melhora a qualidade do código.

```bash
# Lint de arquivo
claude-code lint ./src/app.js

# Lint de pasta
claude-code lint ./src --recursive

# Lint com fix automático
claude-code lint ./src --fix

# Lint com regras específicas
claude-code lint ./src --rules=security,performance

# Lint com formato de saída
claude-code lint ./src --format json

# Lint com ignore de arquivos
claude-code lint ./src --ignore "*.min.js"
```

**Exemplos:**

```bash
# Executar lint com correções automáticas
claude-code lint ./src --fix

# Verificar apenas segurança
claude-code lint ./src --rules security --report

# Gerar relatório JSON
claude-code lint ./src --format json --output report.json

# Lint com padrões customizados
claude-code lint ./src --config .claudelint.json
```

---

### 2.11 `claude-code document`

Gera documentação automática para código.

```bash
# Documentar arquivo
claude-code document ./src/utils.js

# Documentar pasta
claude-code document ./src --recursive

# Documentar em formato Markdown
claude-code document ./src --format markdown

# Documentar com exemplos
claude-code document ./src --include-examples

# Documentar API
claude-code document ./src/api --api-style rest

# Gerar README
claude-code document ./ --generate-readme
```

**Exemplos:**

```bash
# Documentar função com exemplos
claude-code document ./src/utils.js --include-examples --format markdown

# Gerar documentação de API
claude-code document ./src/routes --api-style rest --output docs/api.md

# Documentar projeto completo
claude-code document ./ --format markdown --output docs/ --recursive

# Gerar README automático
claude-code document ./ --generate-readme --include-setup
```

---

### 2.12 `claude-code migrate`

Auxilia na migração de código entre versões, linguagens ou frameworks.

```bash
# Migrar para TypeScript
claude-code migrate ./src --to typescript

# Migrar framework
claude-code migrate ./src --from react --to vue

# Migrar versão
claude-code migrate ./src --from node-12 --to node-20

# Migrar com validação
claude-code migrate ./src --to typescript --validate

# Migração seca (sem modificar)
claude-code migrate ./src --to typescript --dry-run

# Gerar relatório de migração
claude-code migrate ./src --to typescript --report
```

**Exemplos:**

```bash
# Migrar projeto para TypeScript
claude-code migrate ./src --to typescript --validate

# Atualizar React 16 para React 18
claude-code migrate ./src --from react-16 --to react-18

# Migrar Express para Fastify
claude-code migrate ./src --from express --to fastify --report

# Migração Java 8 para Java 21
claude-code migrate ./src --from java-8 --to java-21 --dry-run
```

---

### 2.13 `claude-code prompt`

Gerencia prompts customizados para tarefas recorrentes.

```bash
# Criar novo prompt
claude-code prompt create "meu-prompt"

# Usar prompt customizado
claude-code prompt use "meu-prompt"

# Listar prompts disponíveis
claude-code prompt list

# Editar prompt
claude-code prompt edit "meu-prompt"

# Deletar prompt
claude-code prompt delete "meu-prompt"

# Exportar prompts
claude-code prompt export --output prompts.json

# Importar prompts
claude-code prompt import --file prompts.json
```

**Exemplos:**

```bash
# Criar prompt para code review
claude-code prompt create "code-review" --description "Revisar código em TypeScript"

# Usar prompt para analisar arquivo
claude-code prompt use "code-review" --file ./src/app.ts

# Exportar todos os prompts
claude-code prompt export --output my-prompts.json

# Listar prompts com detalhes
claude-code prompt list --verbose
```

---

### 2.14 `claude-code config`

Gerencia configurações da CLI.

```bash
# Ver configurações atuais
claude-code config get

# Ver uma configuração específica
claude-code config get api-key

# Definir configuração
claude-code config set api-key "sk-..."

# Definir variáveis de ambiente
claude-code config set-env NODE_ENV production

# Resetar para padrão
claude-code config reset

# Ver arquivo de config
claude-code config show

# Validar configuração
claude-code config validate
```

**Exemplos:**

```bash
# Configurar chave de API
claude-code config set api-key "sk-proj-..."

# Definir modelo padrão
claude-code config set default-model claude-3-5-sonnet

# Variáveis de ambiente
claude-code config set-env API_URL "https://api.example.com"

# Resetar todas as configs
claude-code config reset --confirm
```

---

### 2.15 `claude-code auth`

Gerencia autenticação e credenciais.

```bash
# Login
claude-code auth login

# Login com token
claude-code auth login --token "token-aqui"

# Verificar status de autenticação
claude-code auth status

# Logout
claude-code auth logout

# Refresh token
claude-code auth refresh

# Validar credenciais
claude-code auth validate
```

**Exemplos:**

```bash
# Login interativo
claude-code auth login

# Login com token direto
claude-code auth login --token "sk-proj-abc123..."

# Verificar se está autenticado
claude-code auth status

# Fazer logout
claude-code auth logout
```

---

## 3. Comandos com Flags Globais

Flags que funcionam com a maioria dos comandos:

### Flags Comuns

```bash
# Verbose/Debug mode
claude-code [comando] --verbose
claude-code [comando] -v

# Help para comando específico
claude-code [comando] --help
claude-code [comando] -h

# Versão
claude-code --version

# Output format
claude-code [comando] --format json
claude-code [comando] --format yaml

# Quiet mode (menos output)
claude-code [comando] --quiet

# Dry-run (simular sem executar)
claude-code [comando] --dry-run

# Timeout
claude-code [comando] --timeout 30

# Número de tentativas
claude-code [comando] --retry 3
```

---

## 4. Exemplos de Fluxos Comuns

### Exemplo 1: Iniciar um novo projeto

```bash
# 1. Inicializar projeto
claude-code init --name "meu-app" --type typescript

# 2. Gerar estrutura
claude-code generate --project "API REST com Express"

# 3. Build inicial
claude-code build

# 4. Gerar testes
claude-code test --generate "src/main.ts" --framework jest

# 5. Analisar código
claude-code analyze ./src --security --performance
```

### Exemplo 2: Refatorar código existente

```bash
# 1. Analisar situação atual
claude-code analyze ./src --quality --report

# 2. Refatorar
claude-code refactor ./src --focus "performance"

# 3. Gerar testes
claude-code test --generate "./src" --framework jest

# 4. Executar testes
claude-code test --coverage

# 5. Gerar documentação
claude-code document ./src --include-examples --output docs/
```

### Exemplo 3: Debugging de problema

```bash
# 1. Analisar arquivo problemático
claude-code analyze ./src/problematic.js --security --performance

# 2. Debug interativo
claude-code debug ./src/problematic.js --interactive

# 3. Lint com fix
claude-code lint ./src/problematic.js --fix

# 4. Verificar testes
claude-code test ./tests/problematic.test.js --verbose

# 5. Documentar solução
claude-code document ./src/problematic.js --include-examples
```

### Exemplo 4: Deploy para produção

```bash
# 1. Build para produção
claude-code build --prod --minify

# 2. Análise de segurança
claude-code analyze ./src --security

# 3. Testes completos
claude-code test --coverage

# 4. Deploy com aprovação
claude-code deploy --platform vercel --require-approval

# 5. Documentar mudanças
claude-code document ./ --format markdown
```

---

## 5. Troubleshooting

### Comando não reconhecido

```bash
# Verificar instalação
claude-code --version

# Reinstalar
npm install -g @anthropic-ai/claude-code@latest

# Verificar PATH
which claude-code  # macOS/Linux
where claude-code  # Windows
```

### Erro de autenticação

```bash
# Fazer login novamente
claude-code auth login

# Verificar credenciais
claude-code auth validate

# Renovar token
claude-code auth refresh
```

### Problema de performance

```bash
# Executar com verbose para diagnosticar
claude-code [comando] --verbose

# Limpar cache
claude-code config set cache-enabled false

# Atualizar para versão mais recente
npm install -g @anthropic-ai/claude-code@latest
```

---

## 6. Dicas e Boas Práticas

1. **Use `--verbose` para debug** - Ajuda a entender o que está acontecendo
2. **Sempre faça `--dry-run` antes de operações destrutivas** - Simulando antes de executar
3. **Crie prompts customizados** - Para tarefas recorrentes, economize tempo
4. **Use `.claudecode/config.json`** - Para configurações do projeto
5. **Combine comandos** - `claude-code analyze` → `claude-code refactor` → `claude-code test`
6. **Mantenha o arquivo `.gitignore`** - Evite commitar `.claudecode/` se contiver dados sensíveis

---

## 7. Recursos Adicionais

- [Documentação Oficial Claude Code](https://claude.ai/docs)
- [Repository Claude Code CLI](https://github.com/anthropic-ai/claude-code)
- [Guia de Melhores Práticas](https://claudecodedev.com/best-practices)
- [Community Forum](https://forum.claudedev.com)

