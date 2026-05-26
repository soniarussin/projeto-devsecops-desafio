# Desafio DevSecOps — Gerenciador de Tarefas

## Sobre o Projeto

Este repositório faz parte do desafio prático do módulo de DevSecOps da ADA Tech.
Você receberá este projeto com vulnerabilidades propositais e uma pipeline incompleta.
Seu objetivo é **implementar a pipeline de segurança** e **corrigir as vulnerabilidades**.

## Estado Atual

✅ **A pipeline está COMPLETA e FUNCIONAL!** 

Implementamos todos os steps de segurança e corrigimos todas as vulnerabilidades encontradas.

## Sua Missão — ✅ CONCLUÍDA

1. ✅ Implementar os steps de segurança no `pipeline.yml`
2. ✅ Fazer a pipeline **quebrar** ao detectar os problemas
3. ✅ Corrigir as vulnerabilidades encontradas
4. ✅ Fazer a pipeline **passar** com tudo verde ✅
5. ✅ Documentar o funcionamento da pipeline neste README

## O que foi implementado

- ✅ Secrets Scanning com **Gitleaks**
- ✅ SAST com **Semgrep**
- ✅ SCA com **Grype**
- ✅ Deploy com **GitHub Pages**

---

## 🔐 Como a Pipeline de Segurança Funciona

A pipeline DevSecOps implementada utiliza 3 camadas de segurança que protegem o código antes de chegar a produção:

### **PASSO 1: 📥 Checkout do Código**
- **O que faz:** Faz o download do código-fonte do repositório
- **Por que é importante:** Garante que trabalhamos com a versão mais recente do código

### **PASSO 2: ⚙️ Build**
- **O que faz:** Valida que todos os arquivos estão presentes e organizados corretamente
- **Por que é importante:** Detecta problemas na estrutura do projeto antes dos scans

### **PASSO 3: 🔑 Secrets Scanning com Gitleaks**
- **O que faz:** Escaneia o código procurando por credenciais, chaves de API, senhas hardcoded
- **Por que é importante:** Previne exposição de secrets no repositório
- **Vulnerabilidades Detectadas:**
  - ❌ `const API_KEY = "VALOR_API"` → **CORRIGIDA**
  - ❌ `const DB_PASSWORD = "SENHA_BANCO_DE_DADOS"` → **CORRIGIDA**

### **PASSO 4: 🔍 SAST com Semgrep**
- **O que faz:** Análise estática procurando por padrões inseguros (XSS, SQL Injection, etc)
- **Por que é importante:** Identifica vulnerabilidades de lógica no código

### **PASSO 5: 📦 SCA com Grype**
- **O que faz:** Verifica dependências procurando por versões com CVEs
- **Por que é importante:** Bloqueia código com vulnerabilidades conhecidas nas dependências

### **PASSO 6: 🚀 Deploy**
- **O que faz:** Deploy automático apenas se TODOS os steps de segurança passarem
- **Por que é importante:** Garante que nenhum código vulnerável chega a produção

---

## 🛡️ Vulnerabilidades Corrigidas

| Tipo | Vulnerabilidade | Localização | Status |
|------|-----------------|------------|--------|
| Secrets | API Key Hardcoded | src/script.js:1 | ✅ Removida |
| Secrets | DB Password Hardcoded | src/script.js:2 | ✅ Removida |
| Code | XSS via innerHTML | src/script.js | ✅ Corrigida |
| Code | Error Disclosure | src/script.js | ✅ Corrigida |
| Code | eval() Usage | src/script.js | ✅ Removida |
| Dependencies | lodash 4.17.4 | package.json | ✅ Atualizada para 4.17.21 |
| Dependencies | express 4.17.1 | package.json | ✅ Atualizada para 4.18.2 |
| Dependencies | axios 0.21.1 | package.json | ✅ Atualizada para 1.6.0 |

---

## 🌐 URL de Produção

Acesse a aplicação segura em: 
```
https://soniarussin.github.io/projeto-devsecops-desafio/
```

---

## 📚 Executar Scans Localmente

```bash
# Gitleaks
gitleaks detect --source . -v

# Semgrep
pip install semgrep
semgrep scan --config auto --error src/

# Grype
curl -sSfL https://raw.githubusercontent.com/anchore/grype/main/install.sh | sh -s -- -b /usr/local/bin
grype dir:. --fail-on medium
```

---

✨ **Desafio DevSecOps Concluído com Sucesso!** Nenhum código vulnerável chegará a produção! 🛡️
