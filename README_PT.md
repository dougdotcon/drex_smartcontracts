# DrexSmartContracts

Este repositório contém uma implementação simulada em Solidity do contrato inteligente da Moeda Digital do Banco Central (CBDC), o Drex. Baseado na arquitetura conceitual do Real Digital do Banco Central do Brasil, este projeto utiliza a biblioteca OpenZeppelin para fornecer um padrão ERC20 robusto, aprimorado com recursos críticos de conformidade regulatória.

**Aviso Legal:** Este código destina-se apenas a fins educacionais e ilustrativos. Não se trata de uma implementação oficial e não deve ser utilizado em ambiente de produção sem rigorosos testes de auditoria e conformidade legal.

## Principais Funcionalidades

*   **Cunhagem (Minting) e Queima (Burning):** Contas autorizadas podem gerar ou destruir tokens para gerenciar a oferta monetária.
*   **Controle de Acesso:** Segurança baseada em papéis (`MINTER_ROLE`, `BURNER_ROLE`, `PAUSER_ROLE`, `MOVER_ROLE`) garante protocolos rígidos de autorização.
*   **Congelamento de Transações:** O contrato suporta o congelamento de saldos específicos ou de contas inteiras para atender a requisitos regulatórios.
*   **Mecanismos de Pausa:** Papéis autorizados podem pausar e despausar globalmente todas as transferências de tokens durante incidentes de segurança.
*   **Conformidade Regulatória:** Sobrescreve as funções padrão ERC20 `transfer` e `transferFrom` para incluir verificações customizadas de status da conta e saldos congelados.

## Arquitetura

O contrato herda de vários módulos do OpenZeppelin:

*   `ERC20`: Funcionalidades padrão de token.
*   `ERC20Burnable`: Extensões para queima de tokens.
*   `AccessControl`: Gerenciamento granular de papéis.
*   `Pausable`: Mecanismos de parada de emergência.

## Instalação

Para executar este projeto localmente, são necessários Node.js e Hardhat.

bash
# Instalar dependências
npm install

# Compilar contratos
npx hardhat compile

# Executar testes
npx hardhat test


## Interface do Contrato

### Gerenciamento de Contas

*   `disableAccount(address account)`: Restringe um endereço de transferir tokens.
*   `enableAccount(address account)`: Reabilita um endereço previamente restrito.
*   `authorizedAccount(address account)`: Verifica se um endereço está atualmente apto a transacionar.

### Gerenciamento de Saldos

*   `increaseFrozenBalance(address account, uint256 amount)`: Bloqueia uma quantidade específica de tokens dentro de uma conta.
*   `decreaseFrozenBalance(address account, uint256 amount)`: Desbloqueia tokens previamente congelados.
*   `frozenBalanceOf(address account)`: Retorna a quantidade de tokens atualmente bloqueada para uma conta.

### Operações de Token

*   `mint(address to, uint256 amount)`: Cria novos tokens (requer papel Minter).
*   `burn(uint256 amount)`: Destói tokens do saldo do chamador (requer papel Burner).
*   `pause()`: Interrompe todas as transferências (requer papel Pauser).
*   `unpause()`: Retoma as transferências.

## Aviso de Segurança

**Não utilize este código para operações financeiras reais.** Trata-se de uma simulação. Implementações oficiais de CBDC exigem estrita adesão a leis bancárias e auditorias de segurança avançadas. Verifique sempre a lógica do contrato antes de implantar em redes principais (mainnet).