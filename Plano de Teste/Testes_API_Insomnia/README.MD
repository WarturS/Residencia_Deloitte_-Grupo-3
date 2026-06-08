# Esteira de Automação de Testes de API - ParaBank

Este repositório documenta a suíte de testes e a esteira de automação desenvolvida para a API REST do sistema bancário ParaBank, como parte das entregas de Quality Assurance (QA).

A estrutura foi desenvolvida no Insomnia e contempla 16 requisições automatizadas. O escopo cobre validações de segurança, regras de negócio, fluxos de sucesso e a documentação de vulnerabilidades críticas do back-end.

## Arquitetura e Tecnologias

* Ferramenta de Automação: Insomnia Desktop
* Formato de Arquivo: Insomnia Export (JSON)
* Validação e Asserções: JavaScript (Chai)
* Gerenciamento de Dados: Autenticação dinâmica via pre-request e after-response scripts

## Cobertura da Suíte de Testes

A coleção está estruturada nos seguintes módulos lógicos:

1. Login (Gerenciamento de Sessão):
   - POST Login Autenticador: Captura dinâmica de IDs de sessão e variáveis globais.
   - GET Login Carregar Accounts: Validação de estado pós-autenticação.

2. Accounts Overview:
   - GET Accounts Overview (Positivo): Retorno de contas ativas.
   - GET Accounts Overview (Negativo): Tratamento de erro para cliente inexistente.

3. Open New Account:
   - POST Open New Account (Checking): Criação de conta corrente.
   - POST Open New Account (Savings): Criação de conta poupança.
   - POST Open New Account (Tipo Vazio): Rejeição de payload malformado.

4. Transfer Funds:
   - POST Transfer Funds (Positivo): Movimentação com saldo válido.
   - POST Transfer Funds (Negativo): Conta de origem inválida.
   - POST Transfer Funds (Bug Error 500): Envio de parâmetro de valor vazio para forçar e documentar quebra de infraestrutura.

5. Request Loan:
   - POST Request Loan (Positivo): Empréstimo com entrada coerente.
   - POST Request Loan (Negativo): Valor solicitado zerado.
   - POST Request Loan (Bug Inconsistência): Entrada maior que o valor total para documentar falha na regra de crédito.

6. Transactions:
   - GET Transactions por Conta: Extrato detalhado.
   - GET Transactions por Mês e Tipo: Filtros de transação.
   - GET Transactions (Negativo): Conta inexistente.

7. Customer Details:
   - GET Customer (Positivo): Consulta de cadastro.
   - GET Customer (Negativo): Isolamento de dados entre clientes.

## Instruções de Importação e Execução

### 1. Importação da Collection
1. Baixe o arquivo `Parabank_api_tests_Insomnia.json` presente neste repositório.
2. Abra o Insomnia Desktop.
3. Clique em **Create** (ou no ícone de "+") e selecione **Import**.
4. Escolha a opção de importar arquivo (File), selecione o json baixado e confirme a importação.

### 2. Configuração do Ambiente Dinâmico (Passo Obrigatório)
A versão atual da collection automatiza o preenchimento de variáveis de ambiente para contornar os resets do banco de dados da API.
1. No canto superior esquerdo do Insomnia, altere o seletor de ambiente de "No Environment" para **"Base Environment"**.
2. Abra a pasta **"0. Login"**.
3. **Primeiro**, execute a requisição `POST Login Autenticador`.
4. **Em seguida**, execute a requisição `GET Login Carregar Accounts`.
> *Nota: Os scripts contidos nessas duas requisições capturarão as variáveis necessárias (customer_id, account_id, to_account_id) da resposta da API e atualizarão o seu ambiente automaticamente, garantindo que o resto da coleção funcione sem falhas.*

### 3. Execução dos Cenários e Validação
1. **Execução Manual**: Você pode abrir cada requisição individualmente, clicar em `Send` e verificar a aba `Tests` na resposta para analisar as asserções.
2. **Execução Automatizada (Runner)**: No Insomnia, clique no menu de opções da pasta raiz (ou utilize a aba "Runner") e selecione "Run".
3. O Insomnia executará os cenários sequencialmente, validando os contratos e regras de negócio de acordo com os scripts de asserção configurados.

## Documentação de Bugs 

A collection possui scripts elaborados para expor inconsistências do back-end. Testes que apresentam o status de falha (FAIL) no painel de execução são evidências de vulnerabilidades documentadas:

* Falha de Infraestrutura (Transferência): Uma transferência com parâmetro de valor ausente resulta em um 500 Internal Server Error no servidor, sem o devido tratamento de exceção (400 Bad Request).
* Inconsistência Financeira (Empréstimo): A API aprova o crédito mesmo quando o valor da entrada informada é superior ao montante total do empréstimo. O script detecta a flag "approved: true" e acusa a falha na lógica de negócio.
* Falha de Validação (Nova Conta): A API cria indevidamente uma conta corrente (CHECKING) e retorna 200 OK quando o parâmetro de tipo de conta é omitido, ao invés de barrar a criação com um erro 400 Bad Request.
