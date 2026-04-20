**Imagem Dashboard Geral**

<img width="1910" height="1008" alt="image" src="https://github.com/user-attachments/assets/3eaada3d-af72-4709-8f68-9feca48f71f2" />


**Imagem perfil do CEO Agêntico**

<img width="1910" height="1008" alt="image" src="https://github.com/user-attachments/assets/6b1a0770-4069-49b1-9cec-a7c9ab8a7f3e" />



# 🐦 Canary Board FIDIC — AI Investment Management System

> Sistema autônomo de gestão de investimentos em ações brasileiras (B3) e criptoativos, orquestrado por agentes de IA via [Paperclip](https://paperclip.ing).

[![Paperclip](https://img.shields.io/badge/Powered%20by-Paperclip-6366f1?style=flat-square)](https://paperclip.ing)
[![OpenRouter](https://img.shields.io/badge/LLM-OpenRouter-ff6b35?style=flat-square)](https://openrouter.ai)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker)](https://docker.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## 🎯 O que é este projeto?

Este projeto implementa uma **empresa de gestão de investimentos autônoma** usando agentes de IA. O sistema:

1. 🔍 **Pesquisa automaticamente** ativos da B3 e criptoativos
2. 🧠 **Estrutura o conhecimento** em documentos organizados (organograma, RACI, teses de investimento)
3. 📊 **Gera recomendações** baseadas em análise de risco e retorno
4. 🤖 **Delega tarefas** entre agentes especializados (CEO → CTO → Analistas)

Foi construído como resposta ao desafio de [Luis Felipe Amaral](https://www.linkedin.com/in/luis-felipe-amaral/) (CEO/CIO da Drýs Capital) para construção de sistemas com AI agents.

---

## 🏗️ Arquitetura

```
Canary Board FIDIC
│
├── CEO Agent          → Estratégia, alocação de capital, delegação
├── CTO Agent          → Infraestrutura, organograma, documentação técnica
├── [em construção]
├── Analista B3        → Renda fixa, ações, FIIs
├── Analista Cripto    → BTC, ETH, DeFi, altcoins
├── Risk Manager       → Controle de risco, drawdown, correlação
└── Compliance         → Relatórios periódicos, conformidade
```

**Stack:**
- **Orquestração:** [Paperclip](https://paperclip.ing) — control plane para agentes de IA
- **LLM:** OpenRouter (multi-provider — Gemini, GPT-4o, DeepSeek)
- **Adapter:** OpenCode (local multi-provider agent)
- **Banco de dados:** PostgreSQL 17
- **Runtime:** Docker Compose

---

## ⚡ Como rodar

### Pré-requisitos

- Docker + Docker Compose
- Conta no [OpenRouter](https://openrouter.ai) com créditos ($5 é suficiente para centenas de execuções)
- Git

### 1. Clone o repositório

```bash
git clone git@github.com:Klint-prog/canary-board-fidic.git
cd canary-board-fidic
```

### 2. Configure as variáveis de ambiente

```bash
cp .env.example .env
nano .env
```

Preencha:
```ini
POSTGRES_PASSWORD=sua-senha-segura
BETTER_AUTH_SECRET=gere-com-openssl-rand-base64-32
OPENAI_API_KEY=sk-or-sua-chave-openrouter
```

### 3. Suba o sistema

```bash
docker compose -f paperclip.yml up -d
```

### 4. Configure o admin (primeira vez)

```bash
# Crie a configuração inicial
docker exec -it paperclip pnpm paperclipai onboard

# Gere o convite de admin
docker exec paperclip pnpm paperclipai auth bootstrap-ceo
```

Cole a URL gerada no browser. Acesse: **http://localhost:3100**

### 5. Configure os agentes

No painel do Paperclip:
- Vá em **CEO → Configuration**
- Adapter: `OpenCode (local)`
- Model: `google/gemini-2.0-flash-001`
- Salve e clique **Run Heartbeat**

---

## 🤖 O que os agentes fazem

### CEO
- Define a missão e estratégia da gestora
- Cria o organograma da empresa
- Delega tarefas para o CTO e analistas
- Aprova contratações e estratégias

### CTO
- Documenta a estrutura organizacional
- Cria matriz RACI de responsabilidades
- Prepara job descriptions para novos agentes
- Gerencia o workspace técnico

### Próximos agentes (roadmap)
- **Analista B3** → scraping de dados da B3, análise de fundamentos
- **Analista Cripto** → dados on-chain, sentimento de mercado
- **Risk Manager** → VaR, drawdown máximo, correlação entre ativos

---

## 📁 Estrutura do repositório

```
canary-board-fidic/
├── paperclip.yml      # Docker Compose com todos os serviços
├── .env.example       # Variáveis de ambiente (template)
├── .gitignore
└── README.md
```

---

## 🔒 Segurança

- Senhas e chaves de API ficam apenas no `.env` (nunca commitado)
- Modo `authenticated+private` — acesso restrito à rede local/VPN
- PostgreSQL isolado em rede Docker interna
- Dados persistidos em volumes Docker nomeados

---

## 💡 Ideia de produto

Um **CRM AI-native para gestores de investimentos** que:
- Integra dados da B3, CVM e exchanges de cripto em tempo real
- Usa agentes para gerar relatórios automáticos de carteira
- Alerta o gestor sobre oportunidades baseado no perfil de risco
- Documenta automaticamente todas as decisões de investimento para compliance

---

## 👤 Autor

**Jhonatas Mendes**
- GitHub: [@Klint-prog](https://github.com/Klint-prog)
- Projeto construído com profissionalismo, Docker Compose, e muita trabalho para implementar algo ainda unico 🔧

---

## 📄 Licença

MIT — use, modifique e distribua à vontade.
