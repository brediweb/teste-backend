# Teste Backend - API PHP para Cadastro de Produtos

## Descrição do Projeto

Desenvolva uma API REST em PHP para gerenciamento de produtos com relacionamento a categorias. O projeto deve implementar um CRUD completo seguindo os contratos de API especificados neste documento.

## Estrutura do Banco de Dados

### Tabela Categorias (Já existente)

```sql
CREATE TABLE `categorias` (
    `id` INT(11) NOT NULL AUTO_INCREMENT,
    `titulo` VARCHAR(190) NOT NULL,
    PRIMARY KEY (`id`)
) ENGINE=InnoDB;

INSERT INTO `categorias` (`id`, `titulo`) VALUES (4, 'Alimentos');
INSERT INTO `categorias` (`id`, `titulo`) VALUES (5, 'Informática');
INSERT INTO `categorias` (`id`, `titulo`) VALUES (2, 'Eletrodomésticos');
INSERT INTO `categorias` (`id`, `titulo`) VALUES (3, 'Celulares');
```

### Tabela Produtos (A ser criada)

```sql
CREATE TABLE `produtos` (
    `id` INT(11) NOT NULL AUTO_INCREMENT,
    `categoria_id` INT(11) NOT NULL,
    `nome` VARCHAR(255) NOT NULL,
    `preco` DECIMAL(10,2) NOT NULL,
    PRIMARY KEY (`id`),
    FOREIGN KEY (`categoria_id`) REFERENCES `categorias`(`id`) ON DELETE RESTRICT
) ENGINE=InnoDB;
```

## Requisitos Funcionais

### 1. Tela de Cadastro de Produtos

- Listar todos os produtos
- Criar novo produto
- Editar produto existente
- Excluir produto

### 2. Funcionalidades da API

- CRUD completo para produtos
- Relacionamento com categorias
- Validação de dados
- Tratamento de erros

## Contrato das APIs

Todas as APIs devem retornar respostas no seguinte formato padrão:

```json
{
  "error": false,
  "messages": ["Sucesso"],
  "results": []
}
```

### Estrutura de Resposta

- **error**: Boolean indicando se houve erro
- **messages**: Array com mensagens de feedback
- **results**: Array com os dados retornados

## Endpoints Obrigatórios

### 1. Listar Produtos

- **Método**: GET
- **URL**: `/api/produtos`
- **Resposta de Sucesso**:

```json
{
  "error": false,
  "messages": ["Produtos listados com sucesso"],
  "results": [
    {
      "id": 1,
      "categoria_id": 4,
      "nome": "Arroz Integral",
      "preco": "15.99",
      "categoria": {
        "id": 4,
        "titulo": "Alimentos"
      }
    }
  ]
}
```

### 2. Buscar Produto por ID

- **Método**: GET
- **URL**: `/api/produtos/{id}`
- **Resposta de Sucesso**:

```json
{
  "error": false,
  "messages": ["Produto encontrado"],
  "results": {
    "id": 1,
    "categoria_id": 4,
    "nome": "Arroz Integral",
    "preco": "15.99",
    "categoria": {
      "id": 4,
      "titulo": "Alimentos"
    }
  }
}
```

### 3. Criar Produto

- **Método**: POST
- **URL**: `/api/produtos`
- **Body**:

```json
{
  "categoria_id": 4,
  "nome": "Feijão Preto",
  "preco": 8.5
}
```

- **Resposta de Sucesso**:

```json
{
  "error": false,
  "messages": ["Produto criado com sucesso"],
  "results": {
    "id": 2,
    "categoria_id": 4,
    "nome": "Feijão Preto",
    "preco": "8.50"
  }
}
```

### 4. Atualizar Produto

- **Método**: PUT
- **URL**: `/api/produtos/{id}`
- **Body**:

```json
{
  "categoria_id": 5,
  "nome": "Notebook Dell",
  "preco": 2500.0
}
```

- **Resposta de Sucesso**:

```json
{
  "error": false,
  "messages": ["Produto atualizado com sucesso"],
  "results": {
    "id": 1,
    "categoria_id": 5,
    "nome": "Notebook Dell",
    "preco": "2500.00"
  }
}
```

### 5. Excluir Produto

- **Método**: DELETE
- **URL**: `/api/produtos/{id}`
- **Resposta de Sucesso**:

```json
{
  "error": false,
  "messages": ["Produto excluído com sucesso"],
  "results": []
}
```

### 6. Listar Categorias

- **Método**: GET
- **URL**: `/api/categorias`
- **Resposta de Sucesso**:

```json
{
  "error": false,
  "messages": ["Categorias listadas com sucesso"],
  "results": [
    {
      "id": 4,
      "titulo": "Alimentos"
    },
    {
      "id": 5,
      "titulo": "Informática"
    }
  ]
}
```

## Tratamento de Erros

### Produto Não Encontrado

```json
{
  "error": true,
  "messages": ["Produto não encontrado"],
  "results": []
}
```

### Erro de Validação

```json
{
  "error": true,
  "messages": [
    "O campo nome é obrigatório",
    "O campo preço deve ser um número válido"
  ],
  "results": []
}
```

### Categoria Inválida

```json
{
  "error": true,
  "messages": ["Categoria não encontrada"],
  "results": []
}
```

### Erro Interno do Servidor

```json
{
  "error": true,
  "messages": ["Erro interno do servidor"],
  "results": []
}
```

## Entrega

### Arquivos Esperados

1. **api/**: Código fonte da API
2. **database/**: Scripts SQL das tabelas
4. **README.md**: Instruções de instalação e uso
5. **frontend/**: Tela de cadastro (opcional)

### Instruções de Instalação

Inclua no README.md:

- Requisitos do sistema
- Configuração do banco de dados
- Como executar o projeto

## Tecnologias Sugeridas

- **PHP**: Versão 7.4 ou superior
- **MySQL**: Para banco de dados
- **Composer**: Gerenciador de dependências (opcional)

## Bônus (Opcional)

- Implementar filtros de busca
- Criar documentação da API
- Adicionar logs de requisições

Boa sorte com o desenvolvimento! 🚀
