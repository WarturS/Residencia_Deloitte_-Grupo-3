
# Plano de Testes – ParaBank
👨‍🎓Integrantes da equipe: 

- Wenderson Artur da Silva (líder)
- Jefferson Ribeiro dos Santos
- Caio Henrique Santana do Nascimento
- Fellipe Henrique Nogueira Fernandes Caluête
- Matheus Rufino Tavares dos Santos
- Pedro Lucas Santos de Araujo

## Nome do Sistema
ParaBank

## Descrição do Sistema

- O ParaBank é um sistema bancário online de demonstração
que simula o funcionamento de um banco real. Ele permite
realizar operações como consulta de contas, transferências,
pagamentos e empréstimos. É usado para aprendizado,
testes e validação de sistemas bancários, sem envolver
dinheiro real.

## Funcionalidades em Escopo
Liste as funcionalidades que serão consideradas neste plano de testes.

- Accounts Overview
- Open New Account
- Transfer Funds
- Request Loan

---

## Critérios de Aceite

### Accounts Overview

**Front-end**
- Permite Visualizar todas as contas associadas ao usuário autenticado.
- Permite identificar cada conta de forma única dentro do conjunto apresentado.
- Permite compreender o saldo e o valor disponivel de cada conta exibida. 
- Permite ter uma visão consolidada da posição financeira do usuário 
- Permite acessar os detalhes de uma conta selecionada, mantendo o contexto do sistema.

**API / Back-end**
- Permite consultar todas as contas associadas a um cliente a partir de um identificador válido 
- Retorna dados de contas de forma isolada por cliente,sem mistura de informações.
- Retorna respostas consistentes e previsíveis, nesmo quando não existem contas associadas.
- Não  expõe dados de contas não pertencentes ao cliente informado.
- 
### Open New Account

**Front-end**
- Permite iniciar a aberta de uma nova conta para um usuário autenticado.
- Exige a definição do tipo de conta e de uma conta de origem para o depósito inicial. 
- Não permite prosseguir sem as informações mínimas necessárias 
- Comunica ao Usuário o resultado da tentativa de abertura de conta .
- Mantém o acesso contínuo ás demais funcionalidades após da operação.
---
**API / Back-end**
- Permite criar uma nova conta vinculada a um cliente existente .
- Exige cliente , tipo de conta e conta de origem válidos para processar a criação 
- Não cria contas quando  informações obrigatórias estão ausentes ou inválidas. 
- Em caso de sucesso , a nova conta passa a fazer parte do conjunto de contas do cliente .
- Em caso de erro, não gera efeitos colaterais parciais  sobre contas existentes.
---

### Transfer Funds

**Front-end**
- Permite transferir valores entre contas pertencentes ao usuário autenticado 
- Exige valor , conta de origem e conta de destino para realizar a operação. 
- Não permite a execução de transferência sem informações essenciais.
- Comunica o resultado da tentativa de transferência ao usuário .
- Mantém o contexto de navegação do sistema após a operação.
--- 

**API / Back-end**
- Permite registrar uma transação de transferência entre contas válidas. 
- Garante que as contas envolvidas pertencem ao mesmo cliente .
- Registra a transferência de forma atômica,  sem estados intermediários inconsistentes .
- Em caso de erro, não altera saldos nem cria transações parciais .
- Retorna reposta coerente com o resultado da operação.
---

### Request Loan

**Front-end**
- Permite ao usuario solicitar um empréstimo associado à sua conta.
- Exige valor de empréstimo, valor de entrada e conta de origem.
- Não permite a submissão da solicitação sem as informações necessárias.
- Apresenta ao usuário o resultado da solicitação dentro do próprio fluxo.
- Mantém o uso continuo do sistema após a solicitação.

**API / Back-end**
- Permite registrar solicitações de empréstimo para clientes exigentes.
- exige cliente, valores e conta de origem válidos.
- Retorna de forma clara o resultado da solicitação (processada ou não).
- Em caso de sucesso, gera um empréstimo vinculado ao cliente e à conta.
- Em caso de erro, não provoca alterações parciais em dados financeiros.

---

## Funcionalidades Fora de Escopo
- Histórico de Pagamentos
- Editar Conta
- Investimento

---

## Estratégia de Testes

### Objetivo dos testes:
- Desenvolver e manter um sistema robusto, garantindo a execução de testes tanto na interface quanto no backend, com foco na identificação e documentação de falhas. Gerar relatórios claros sobre bugs encontrados, acompanhar os resultados dos testes e assegurar a entrega de resultados positivos, contribuindo para a melhoria contínua da qualidade do software.
### Tipos ou níveis de teste serão considerados:
- teste de componentes, teste de integração e testes de sistema , nível de teste (caixa preta)
### Ferramentas podem ser utilizadas:
- Trello , Playwrigth, Insomnia, TestRail

---

## Premissas e Riscos

### Premissas
- O Usuário devidamente cadastrado , conseguirá realizar pagamentos,transferência, empréstimos e criação de novas contas.
- O ambiente ParaBank estará disponível durante todo o  período de testes (23/04 a 04/06).
- Todos os 6 integrantes participarão ativamente de cada sprint conforme planejado.
- As funcionalidades fora de escopo (Histórico de Pagamentos, Editar Conta, Investimento) não serão testadas em nenhuma sprint. 

### Riscos
- O ambiente de testes pode apresentar indisponibilidade ou comportamento inconsistente em determinados períodos, comprometendo a execução das sprints.
- Problemas na instalação ou configuração das ferramentas podem atrasar o início dos testes automatizados e de API.

## Gerenciamento do Projeto

### Metodologia
Método ágil - Scrum

### Organização em Sprints

####  Quantas sprints compõem o projeto : 
- 04 Sprint
#### A duração estimada de cada sprint : 
- 01 Semana
 
#### Sprint 01 :

Criar os cenários e Casos de testes das seguintes funcionalidades: 
- Accounts Overview,
- Open New Account,
- Transfer Rounds,
- Request Loan
- Adicionar os cenários e casos de testes no TestRail

#### Sprint 02 : 

Realizar Teste de Interface em Accounts Overview: 
- Testar carregamento  das dashboards: saldo, lista de contas, histórico
- Validar responsividade: desktop, mobile
- Validar interface visual: alinhamento, espaçamento, cores, fontes, ícones
	  
Realizar Teste de Interface em Open New Account:
- Validar formulário>: campos obrigatórios
- Validar mensagens: sucesso, erro, campos inválidos

Realizar Teste de Interface em Trasnfer Founds: 
- Validar fluxo de transferência: conta origem, conta destino, valor, confirmação
- Validar comportamento visual: mensagens, feedback visual
- Validar erros : saldo insuficiente, valor negativo, campos vazios
- Teste de responsividade

Realizar Teste de Interface em Request Loan: 
- Validar formulário de empréstimo: valores, entrada, envio
- Validar UX/UI: clareza das informações, organização visual
- Validar erros: valor negativo, campos vazios

#### Sprint 03 : 
- Realizar teste de API 
#### Sprint 04 : 
- Realizar testes dentro do TestRail
- Realizar casos de evidência para cada caso de teste.
### Cronograma
- Data de início do projeto : 23/04
- Data prevista de encerramento: 04/06

