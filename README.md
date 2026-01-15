# 🤖Agente Gemini QA com Playwright MCP

Este repositório contém as configurações e o contexto necessário para executar testes E2E avançados na aplicação web alvo, utilizando o Gemini Code Assist (Modo Agente) em conjunto com o Playwright Model Context Protocol (MCP).

O agente é configurado para realizar testes funcionais, de regressão (datas/variáveis) e de qualidade de interface (responsividade/a11y/XSS) automaticamente.

⚙️ Pré-requisitos
Para rodar o agente, você precisa ter instalado:

Node.js (versão LTS ou superior): Necessário para o Gemini CLI e Playwright MCP.

npm (Node Package Manager): Geralmente incluído com o Node.js.

Git: Para clonar este repositório.

Conta Google: Para autenticar o Gemini CLI.

Gemini Code Assist / Gemini CLI: A ferramenta de agente instalada globalmente.

🚀 1. Setup e Instalação
Siga os passos abaixo no seu terminal (CMD ou PowerShell) para preparar o ambiente.

Passo 1.1: Clonar o Repositório
Bash

# 1. Clone este repositório para sua máquina
```bash
cd gemini-agente-e2e
```
# 2. Acesse o diretório do projeto
```bash
cd gemini-agente-e2e
```
Passo 1.2: Instalar Ferramentas Essenciais
Instale o Gemini CLI (globalmente) e as dependências locais (Playwright MCP) definidas no package.json.

Bash

# Instala o Gemini CLI (se já não estiver instalado)
```bash
npm install -g @google/gemini-cli@latest
```
# Instala as dependências do Playwright MCP
```bash
npm install
```
# Instala os binários dos navegadores (Chromium, Firefox, WebKit)
```bash
npx playwright install
```
# Rode o Gemini para autenticação
```bash
Digite "Gemini" no seu cmd
```
Passo 1.3: Autenticação do Gemini
Na primeira vez que usar o gemini na sua máquina, você deve autenticar:

🛠️ 2. Configuração do Agente e do MCP
Para que o Gemini use o Playwright, ele precisa de um arquivo de configuração.

Passo 2.1: Criar o Arquivo de Configuração Global (settings.json)
Você precisa criar este arquivo no seu diretório de usuário para configurar o servidor MCP.

Localização no Windows: C:\Users\<SeuUsuário>\.gemini\settings.json

Conteúdo do settings.json:

Cole o seguinte código. Ele configura o Playwright MCP e remove o modo headless (--headless) para que você possa ver a execução:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": [
        "@playwright/mcp@latest"
        // O modo visível (non-headless) é o padrão sem o argumento --headless.
      ]
    }
  },
  "security": {
    "auth": {
      "selectedType": "oauth-personal"
    }
  }
}
```

Passo 2.2: Contexto do Agente (GEMINI.md)
O arquivo GEMINI.md na raiz deste projeto contém todo o contexto do teste complexo. O agente o lerá automaticamente para entender os seletores (como o seletor do botão "Inventário") e as regras de teste avançadas.

⏯️ 3. Execução do Teste E2E
Para executar o teste E2E complexo definido no GEMINI.md, siga esta rotina:

Etapa 3.1: Iniciar o Gemini CLI (ou Modo Agente na IDE)
Bash

# Inicia o Gemini CLI dentro da pasta do projeto
gemini
Etapa 3.2: Confirmar o Carregamento do MCP
Dentro do Gemini CLI, verifique o status do servidor:

/mcp
A saída deve ser: 🟢 playwright - Ready (XX tools)

Etapa 3.3: Iniciar o Teste
Peça ao agente para executar o teste de "Inventário", referenciando o arquivo de contexto:

Agente, execute o teste de fluxo completo de login e geração de Inventário conforme detalhado no meu GEMINI.md. Lembre-se, a visualização é OBRIGATÓRIA.
O agente apresentará o Plano de Ação (10 etapas funcionais + validações não-funcionais). Aprovar o primeiro passo (y) forçará a abertura do navegador e iniciará a execução visível.

🔒 Segurança (Arquivos Ignorados)
Os seguintes arquivos são ignorados pelo Git (via .gitignore) porque contêm dependências ou dados sensíveis:

node_modules/

.gemini/ (Contém seu settings.json privado e tokens)

Arquivos de resultados de teste e logs (/test-results, /playwright-report)
