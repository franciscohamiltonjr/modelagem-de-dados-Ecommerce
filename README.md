# 🛒 Projeto de E-commerce – Plataforma de Vendas Online

## 📘 Descrição do Projeto

Este projeto tem como objetivo modelar e implementar um **sistema de e-commerce completo** voltado para **venda de produtos online**, permitindo a integração entre **clientes, fornecedores, controle de estoque, pedidos, pagamentos e entregas**.

A aplicação foi estruturada para funcionar como um **marketplace**, onde múltiplos vendedores podem comercializar produtos dentro de uma única plataforma, mantendo rastreabilidade total do processo de compra e venda.

---

## 🚀 Funcionalidades Principais

- Cadastro de clientes (Pessoa Física e Jurídica)
- Cadastro e gerenciamento de produtos e fornecedores
- Controle de estoque e notificações de reposição
- Registro e acompanhamento de pedidos
- Processamento de pagamentos (PIX, cartão, boleto)
- Rastreamento de entrega com código e status
- Suporte a múltiplas formas de pagamento por cliente
- Cancelamento e devolução de pedidos

---

## 🧩 Modelagem do Sistema

### **Entidades Principais**
- **Produto**
- **Cliente (PF e PJ)**
- **Fornecedor**
- **Estoque**
- **Pedido**
- **Item_Pedido**
- **Pagamento**
- **Entrega**

---

## 🧱 Estrutura do Banco de Dados (DER)

```mermaid
erDiagram

    CLIENTE ||--o{ ENDERECO : possui
    CLIENTE ||--o{ PEDIDO : realiza
    CLIENTE ||--o{ PAGAMENTO : efetua
    FORNECEDOR ||--o{ PRODUTO : fornece
    PRODUTO ||--|| ESTOQUE : controla
    PEDIDO ||--o{ ITEM_PEDIDO : contem
    ITEM_PEDIDO }o--|| PRODUTO : refere
    PEDIDO ||--|| PAGAMENTO : possui
    PEDIDO ||--|| ENTREGA : gera

    CLIENTE {
        int id_cliente
        string nome_razao_social
        string tipo_cliente
        string cpf_cnpj
        string email
        string telefone
    }

    ENDERECO {
        int id_endereco
        int id_cliente
        string cep
        string logradouro
        string numero
        string cidade
        string estado
        string tipo_endereco
    }

    FORNECEDOR {
        int id_fornecedor
        string razao_social
        string cnpj
        string email
        string telefone
    }

    PRODUTO {
        int id_produto
        string nome
        string descricao
        decimal preco
        string categoria
        int id_fornecedor
        int id_estoque
        string status
    }

    ESTOQUE {
        int id_estoque
        int id_produto
        int quantidade_atual
        int quantidade_minima
        date data_ultima_atualizacao
    }

    PEDIDO {
        int id_pedido
        int id_cliente
        int id_endereco
        int id_pagamento
        int id_entrega
        date data_pedido
        decimal valor_total
        string status
    }

    ITEM_PEDIDO {
        int id_item
        int id_pedido
        int id_produto
        int quantidade
        decimal preco_unitario
    }

    PAGAMENTO {
        int id_pagamento
        int id_cliente
        string tipo
        string status
        decimal valor
        date data_pagamento
    }

    ENTREGA {
        int id_entrega
        int id_pedido
        string transportadora
        string codigo_rastreio
        string status_entrega
        date data_envio
        date data_entrega_prevista
        date data_entrega_real
    }
