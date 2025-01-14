# Banco de Dados - Sistema de Estoque

Este repositório contém a estrutura do banco de dados para o sistema de gerenciamento de estoque. Ele foi projetado para atender às necessidades de cadastramento, controle e movimentação de produtos, com suporte a categorias e histórico de movimentações.

## Estrutura do Banco de Dados

O banco de dados é composto por três tabelas principais:

1. **categorias**: Gerencia as categorias dos produtos.
2. **produtos**: Armazena as informações sobre os produtos.
3. **movimentacoes**: Registra as movimentações (entrada e saída) de estoque.

### Script de Criação das Tabelas

```sql
CREATE TABLE categorias (
    id_categoria INT AUTO_INCREMENT PRIMARY KEY,
    nome_categoria VARCHAR(100) NOT NULL,
    descricao TEXT
);

CREATE TABLE produtos (
    id_produto INT AUTO_INCREMENT PRIMARY KEY,
    nome_produto VARCHAR(150) NOT NULL,
    id_categoria INT,
    preco DECIMAL(10, 2) NOT NULL,
    quantidade_estoque INT DEFAULT 0,
    FOREIGN KEY (id_categoria) REFERENCES categorias (id_categoria)
);

CREATE TABLE movimentacoes (
    id_movimentacao INT AUTO_INCREMENT PRIMARY KEY,
    id_produto INT,
    tipo_movimentacao ENUM('entrada', 'saida') NOT NULL,
    quantidade INT NOT NULL,
    data_movimentacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_produto) REFERENCES produtos (id_produto)
);
