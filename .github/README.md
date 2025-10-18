# GitHub Actions Workflows

Este diretório contém os workflows de CI/CD para o projeto backend-core.

## 📋 Workflows Disponíveis

### 1. **CI Pipeline** (`ci.yml`)
Executado em: Push e Pull Requests para `main` e `develop`

**Funcionalidades:**
- ✅ Checkout do código
- ✅ Setup Java 21 (Temurin)
- ✅ Setup PostgreSQL 15.5
- ✅ Build com Maven
- ✅ Execução de testes
- ✅ Empacotamento da aplicação
- ✅ Upload de artefatos
- ✅ Geração de relatórios de teste

### 2. **CD Pipeline** (`cd.yml`)
Executado em: Push para `main` e criação de tags

**Funcionalidades:**
- 🚀 Build e deploy automático
- 🐳 Criação de imagem Docker
- 📦 Push para Docker Hub
- 🏷️ Release no GitHub com artefatos

**Secrets necessários:**
- `DOCKER_USERNAME`: Usuário do Docker Hub
- `DOCKER_PASSWORD`: Senha do Docker Hub

### 3. **Pull Request Checks** (`pr-checks.yml`)
Executado em: Pull Requests

**Funcionalidades:**
- 🔍 Verificação de qualidade de código
- 🔒 Scan de segurança (OWASP Dependency Check)
- 📊 Cobertura de testes (Jacoco + Codecov)
- 🏷️ Auto-labeling de PRs

### 4. **CodeQL Analysis** (`codeql.yml`)
Executado em: Push, Pull Requests e semanalmente (segundas às 6h)

**Funcionalidades:**
- 🛡️ Análise de segurança estática
- 🔎 Detecção de vulnerabilidades
- 📈 Relatórios de segurança

### 5. **Dependency Review** (`dependency-review.yml`)
Executado em: Pull Requests

**Funcionalidades:**
- 📦 Revisão de dependências
- ⚠️ Detecção de vulnerabilidades em dependências
- 🚫 Bloqueio de licenças GPL-2.0 e GPL-3.0
- 💬 Comentários automáticos em PRs

## 🤖 Dependabot

Configurado para atualizar automaticamente:
- 📦 Dependências Maven (semanalmente)
- 🔧 GitHub Actions (semanalmente)
- 🐳 Imagens Docker (semanalmente)

## 🏷️ Auto-labeling

O sistema de auto-labeling adiciona labels automaticamente baseado nos arquivos modificados:

| Label | Arquivos |
|-------|----------|
| `customer` | `src/**/customer/**/*` |
| `schedules` | `src/**/schedules/**/*` |
| `database` | `src/main/resources/db/migration/**/*` |
| `config` | `*.properties`, `*.yml` |
| `security` | `**/security/**/*` |
| `tests` | `src/test/**/*` |
| `dependencies` | `pom.xml` |
| `docker` | `Dockerfile`, `docker-compose.yml` |
| `ci/cd` | `.github/workflows/**/*` |
| `documentation` | `**/*.md` |

## 🚀 Como Usar

### Para desenvolvedores:

1. **Criar uma branch:**
   ```bash
   git checkout -b feature/minha-feature
   ```

2. **Fazer commit e push:**
   ```bash
   git add .
   git commit -m "feat: adiciona nova funcionalidade"
   git push origin feature/minha-feature
   ```

3. **Abrir Pull Request:**
   - Os workflows `pr-checks.yml` e `dependency-review.yml` serão executados automaticamente
   - Aguarde a aprovação dos checks

4. **Após merge para main:**
   - O workflow `ci.yml` será executado
   - O workflow `cd.yml` fará o deploy automaticamente

### Para releases:

1. **Criar uma tag:**
   ```bash
   git tag -a v1.0.0 -m "Release v1.0.0"
   git push origin v1.0.0
   ```

2. **O workflow `cd.yml` criará:**
   - Release no GitHub
   - Upload dos JARs
   - Notas de release automáticas

## 📝 Secrets Necessários

Configure os seguintes secrets no GitHub:

| Secret | Descrição |
|--------|-----------|
| `DOCKER_USERNAME` | Usuário do Docker Hub |
| `DOCKER_PASSWORD` | Senha do Docker Hub |
| `CODECOV_TOKEN` | Token do Codecov (opcional) |

## 🔧 Manutenção

- Os workflows são executados automaticamente
- Dependabot cria PRs semanais para atualizações
- CodeQL executa scans semanais de segurança
- Todos os workflows usam cache do Maven para melhor performance
