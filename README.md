# 📊 Modelagem de Casos de Uso — Sistema de Controle Financeiro

> Atividade acadêmica desenvolvida para a disciplina de **Análise e Desenvolvimento de Sistemas (ADS)**.  
> Modelagem UML completa de um sistema de controle financeiro simplificado.

---

## 📁 Estrutura do Repositório

```
📦 modelagem-casos-de-uso/
├── 📄 README.md
└── 📄 ATIVIDADE_MODELAGEM_DE_CASOS_DE_USO.pdf
```

---

## 📌 Sobre o Projeto

Este trabalho apresenta a modelagem UML de um **Sistema de Controle Financeiro Simplificado**, cobrindo três entregas principais:

| Entrega | Descrição |
|---|---|
| Diagrama de Contexto | Visão externa do sistema (caixa-preta), atores e interações |
| Diagrama de Casos de Uso | Relações de `<<include>>`, `<<extend>>` e generalização de atores |
| Especificação Descritiva | Detalhamento completo do caso de uso *Registrar Despesa* |

---

## 👥 Atores do Sistema

- **Usuário** — ator principal, realiza operações básicas do sistema
- **Gerente Financeiro** — especialização do Usuário (herança/generalização), com permissões adicionais
- **Sistema Bancário** — ator externo que fornece dados de transações

---

## 🔄 Casos de Uso Modelados

| Caso de Uso | Tipo | Ator(es) |
|---|---|---|
| Autenticar | Base | Usuário |
| Registrar Receita | Base | Usuário |
| Registrar Despesa | Base | Usuário |
| Validar Saldo Disponível | `<<include>>` de Registrar Despesa | Sistema |
| Categorizar Lançamento | `<<include>>` de Registrar Despesa | Sistema |
| Consultar Extrato | Base | Usuário |
| Gerenciar Contas | Base | Gerente Financeiro |
| Gerar Relatório Financeiro | Base | Gerente Financeiro |
| Exportar Relatório | `<<extend>>` de Gerar Relatório | Gerente Financeiro |

---

## 📋 Especificação: Registrar Despesa

**Pré-condições:**
- Usuário autenticado no sistema
- Pelo menos uma conta cadastrada

**Requisitos atendidos:** `RF-03` `RF-05` `RF-07`

**Fluxo Principal:**
1. Usuário seleciona "Registrar Despesa"
2. Sistema exibe formulário (conta, data, valor, categoria, descrição)
3. Usuário preenche e confirma
4. Sistema executa `Validar Saldo Disponível` *(include)*
5. Sistema executa `Categorizar Lançamento` *(include)*
6. Sistema salva o lançamento e atualiza o saldo
7. Sistema exibe mensagem de sucesso

**Fluxos Alternativos e de Exceção:**

| Código | Situação | Comportamento |
|---|---|---|
| A1 | Usuário cancela antes de confirmar | Sistema descarta e retorna ao menu |
| E1 | Saldo insuficiente | Exibe aviso e retorna ao formulário |
| E2 | Erro ao salvar | Exibe erro e solicita nova tentativa |

---

## 🛠️ Conceitos UML Aplicados

- **Diagrama de Contexto** — visão estática de alto nível (caixa-preta)
- **Diagrama de Casos de Uso** — visão funcional do sistema
- **`<<include>>`** — comportamento obrigatório, sempre executado
- **`<<extend>>`** — comportamento opcional, executado sob condição
- **Generalização de atores** — herança entre Usuário e Gerente Financeiro

---

## 🎓 Informações Acadêmicas

- **Curso:** Tecnologia em Análise e Desenvolvimento de Sistemas
- **Disciplina:** Engenharia de Software / Análise de Sistemas
- **Atividade:** Modelagem de Casos de Uso

---

*Desenvolvido como atividade acadêmica — ADS*
