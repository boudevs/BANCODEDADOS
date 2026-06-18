## Modelo de Dados

Cinco tabelas: `endereco`, `cliente`, `pizza`, `pedido`, `item_pedido`.

Três views: `vw_pedidos_completos`, `vw_itens_pedido`, `vw_pizzas_mais_vendidas`.

Três functions: `fn_valor_total_pedido`, `fn_total_pedidos_cliente`, `fn_pizza_mais_pedida_cliente`.

Três procedures: `sp_inserir_pedido`, `sp_inserir_item_pedido`, `sp_cancelar_pedido`.

## Regras de Negócio

1. Um cliente só pode ser removido se não possuir pedidos vinculados
2. Uma pizza só pode ser removida se não houver itens de pedido referenciando-a
3. A quantidade de itens deve ser maior que zero (validado na procedure)
4. O preço unitário do item é registrado no momento do pedido, independente de alterações futuras no cardápio
5. Ao cancelar um pedido, todos os seus itens são removidos automaticamente em cascata

## Como Executar

### Pré-requisitos

- Java 17+
- Maven 3.8+
- PostgreSQL 15+ rodando localmente

### 1. Configurar o banco

```sql
CREATE DATABASE pizzaria;
```

Execute os scripts na ordem:

```bash
psql -U postgres -d pizzaria -f sql/01_ddl.sql
psql -U postgres -d pizzaria -f sql/02_views_functions_procedures.sql
psql -U postgres -d pizzaria -f sql/03_seed.sql
```

### 2. Configurar a conexão

Edite o arquivo `src/main/java/pizzaria/ConexaoBD.java` com suas credenciais:

```java
private static final String URL     = "jdbc:postgresql://localhost:5432/pizzaria";
private static final String USUARIO = "postgres";
private static final String SENHA   = "sua_senha";
```

### 3. Compilar e executar

```bash
mvn package
java -jar target/pizzaria-1.0.0.jar
```

Ou pelo Eclipse: botão direito em `Main.java` → **Run As → Java Application**

## Funcionalidades do Sistema

1. **Gerenciar Pizzas** → listar, buscar, cadastrar, atualizar, remover
2. **Gerenciar Clientes** → listar, buscar, cadastrar, atualizar, remover
3. **Pedidos** → novo pedido, adicionar itens, ver itens, cancelar
4. **Relatórios** → todos os pedidos, pizzas mais vendidas, pizza favorita
0. **Sair**
