# Atividade — Modelagem de Casos de Uso
## Sistema de Controle Financeiro Simplificado

---

## 1. Diagrama de Contexto

**Sistema de Controle Financeiro Simplificado — Interações Externas**

> O sistema aparece aqui como um bloco único (Caixa Preta). Nenhum processo interno é mostrado, apenas quem interage com ele e o que troca nessas interações. O Gerente Financeiro é uma especialização do Usuário: ele herda as mesmas interações e acrescenta as suas próprias.

### Atores

| Ator | Tipo | Interações |
|------|------|-----------|
| Usuário | Ator principal | Informa credenciais de acesso; Registra receitas e despesas; Consulta extrato financeiro; Gerencia contas e categorias |
| Gerente Financeiro | Especialização do Usuário (generalização) | Herda interações do Usuário + Solicita relatório financeiro |
| Sistema Bancário | Ator externo | Fornece dados de transações bancárias |

---

## 2. Diagrama de Casos de Uso

**Relações de include, extend e generalização de atores**

### Atores

- **Usuário** — ator principal
- **Gerente Financeiro** — generalização do Usuário
- **Sistema Bancário** — ator externo

### Casos de Uso

| Caso de Uso | Relações |
|-------------|----------|
| Autenticar | — |
| Registrar Receita | `<<include>>` Validar Saldo Disponível |
| Registrar Despesa | `<<include>>` Validar Saldo Disponível; `<<include>>` Categorizar Lançamento |
| Validar Saldo Disponível | Incluído por outros casos de uso |
| Categorizar Lançamento | Incluído por outros casos de uso |
| Consultar Extrato | — |
| Gerenciar Contas | — |
| Gerar Relatório Financeiro | `<<extend>>` Exportar Relatório |
| Exportar Relatório | Estende Gerar Relatório Financeiro |

> **Legenda:** `<<include>>` = sempre executado | `<<extend>>` = execução opcional

---

## 3. Especificação Descritiva do Caso de Uso

**Caso selecionado: Registrar Despesa**

| Campo | Descrição |
|-------|-----------|
| **Nome** | Registrar Despesa |
| **O que faz** | O usuário informa conta, data, valor, categoria e descrição de uma despesa. O sistema valida o saldo disponível, vincula a categoria e salva no extrato. |
| **Atores** | Usuário (ator principal) |
| **Casos de Uso ligados** | Autenticar; Validar Saldo Disponível `<<include>>`; Categorizar Lançamento `<<include>>` |
| **Antes de começar** | O usuário precisa estar logado (UC Autenticar já executado). Tem que existir pelo menos uma conta cadastrada. |
| **Requisitos atendidos** | RF-03, RF-05, RF-07 |

### Fluxo Principal

| # | Ator | Sistema |
|---|------|---------|
| P1 | Seleciona "Registrar Despesa" no menu. | — |
| P2 | — | Exibe o formulário com os campos: conta, data, valor, categoria e descrição. |
| P3 | Preenche os campos e confirma. `[A1]` | — |
| P4 | — | Executa UC Validar Saldo Disponível, checa se o saldo da conta cobre a despesa. `[E1]` |
| P5 | — | Executa UC Categorizar Lançamento, vincula a despesa à categoria informada. |
| P6 | — | Salva o lançamento no extrato e atualiza o saldo. `[E2]` |
| P7 | — | Mostra a mensagem: "Despesa registrada com sucesso". |
| P8 | — | Encerra a operação. |

### Fluxo Alternativo

**[A1] Usuário cancela antes de confirmar**

- A1.1. Clica em "Cancelar".
- A1.2. Sistema descarta o que foi digitado e volta ao menu.

### Fluxos de Exceção

**[E1] Saldo insuficiente**

- E1.1. Sistema avisa: "Saldo insuficiente para registrar esta despesa."
- E1.2. Retorna ao P2.

**[E2] Erro ao salvar**

- E2.1. Mensagem de erro e pede para tentar de novo.
- E2.2. Retorna ao P3.

### Resultado Esperado

A despesa fica gravada, o saldo diminui. Ou tudo é cancelado sem mudar nada. Ou dá erro e o sistema pede para tentar de novo.
