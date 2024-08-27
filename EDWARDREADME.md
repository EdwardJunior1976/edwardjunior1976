luma-store-tests/
├── cypress/
│   ├── integration/
│   │   ├── luma_store_tests.spec.js
│   ├── fixtures/
│   ├── plugins/
│   ├── support/
├── cypress.json
├── package.json
└── README.md
describe('Luma Store - Teste Automatizado', () => {

    // Antes de cada teste, navegue para a página inicial
    beforeEach(() => {
        cy.visit('https://magento.softwaretestingboard.com/');
    });

    // Caso de uso 1: Verificar se a página carrega corretamente
    it('Deve carregar a página inicial', () => {
        cy.get('.logo').should('be.visible'); // Verifica se o logo está visível
    });

    // Caso de uso 2: Buscar por "shirt"
    it('Deve buscar por "shirt" e carregar os resultados corretamente', () => {
        cy.get('#search').type('shirt{enter}');
        cy.get('.search.results').should('be.visible');
        cy.contains('shirt').should('exist');
    });

    // Diferencial 1: Selecionar o último resultado de "shirt"
    it('Deve clicar no último resultado de "shirt"', () => {
        cy.get('#search').type('shirt{enter}');
        cy.wait(2000); // Aguardar requisição
        cy.get('.product-item').last().click();
        cy.url().should('include', '/shirt'); // Verifica se estamos na página do produto
    });

    // Caso de uso 3: Adicionar um produto ao carrinho
    it('Deve adicionar um produto ao carrinho', () => {
        cy.get('#search').type('shirt{enter}');
        cy.get('.product-item').first().click();
        cy.get('#product-addtocart-button').click();
        cy.get('.message-success').should('be.visible');
    });

    // Caso de uso 4: Realizar o checkout
    it('Deve realizar o checkout com sucesso', () => {
        // Supondo que já adicionou um produto ao carrinho
        cy.get('.showcart').click();
        cy.get('#top-cart-btn-checkout').click();
        // Preencher informações de checkout (exemplo)
        cy.get('#customer-email').type('teste@teste.com');
        cy.get('#billing-address').type('Rua Teste, 123');
        cy.get('#place-order-button').click();
        cy.get('.success-message').should('be.visible');
    });
});
{
  "baseUrl": "https://magento.softwaretestingboard.com/",
  "viewportWidth": 1280,
  "viewportHeight": 720,
  "reporter": "mochawesome"
}
{
  "name": "luma-store-tests",
  "version": "1.0.0",
  "scripts": {
    "test": "cypress run"
  },
  "dependencies": {
    "cypress": "^12.0.0",
    "mochawesome": "^6.2.2"
  }
}
# Luma Store - Testes Automatizados

Este projeto visa automatizar testes funcionais na loja virtual Luma Store utilizando Cypress.

## Tecnologias Utilizadas
- Cypress
- Mochawesome (relatórios)

## Como Instalar e Rodar os Testes

### Pré-requisitos
- Node.js e npm instalados

### Instalação
1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/luma-store-tests.git
npm install
npx cypress open
npm test

---

### Estrutura do Projeto em Selenium
Se você quiser usar Selenium em vez de Cypress, o projeto teria uma estrutura semelhante. Aqui está um exemplo de código usando Python com Selenium:

**Estrutura do Projeto:**
```bash
selenium-tests/
├── tests/
│   ├── luma_store_test.py
├── README.md
├── requirements.txt
└── .gitignore
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import unittest

class LumaStoreTests(unittest.TestCase):

    def setUp(self):
        self.driver = webdriver.Chrome()

    def test_homepage_load
