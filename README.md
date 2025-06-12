# 📊 Savana Tech – Projeto de Dados em Databricks

Este projeto implementa uma pipeline de ingestão, tratamento e análise de dados utilizando a arquitetura em camadas (Medalhão) com o ambiente Databricks, integrando fontes de dados **MySQL** e **MongoDB**.

---

## 🧱 Arquitetura Medalhão

- **Bronze**: Dados brutos extraídos diretamente das fontes (MySQL e MongoDB).
- **Silver**: Dados tratados, normalizados e prontos para consumo analítico.
- **Gold**: Métricas consolidadas aplicando regras de negócio com SQL.

---

## 📁 Estrutura de Catálogo e Schemas

Todos os dados são organizados no catálogo:

```
adb_cliente_savana_prd
```

E os schemas seguem a estrutura:

```
adb_cliente_savana_prd.elenir_bronze
adb_cliente_savana_prd.elenir_silver
adb_cliente_savana_prd.elenir_gold
```

> Substitua `elenir` pelo identificador de cada usuário no projeto.

---

## 🔗 Fontes de Dados

- **MySQL** → Tabela `clientes`
- **MongoDB** → Coleção `transacoes`

---

## ⚙️ Fluxo de Processamento

### 🥉 Bronze
- Ingestão diária via JDBC (MySQL) e Mongo Connector.
- Tabelas:
  - `bronze.clientes`
  - `bronze.transacoes`

### 🥈 Silver
- Padronização de campos: remoção de metacaracteres, limpeza de texto e tratamento de nulos.
- Extração de campos internos de `_id`.
- Tabela:
  - `silver.transacoes_tratadas`

### 🥇 Gold
- Métricas derivadas (ex: total de transações por mês, última transação por cliente, volume por cidade).
- Construídas exclusivamente com **SQL**.

---

## 📌 Tecnologias Utilizadas

- **Databricks**
- **Apache Spark / PySpark**
- **Unity Catalog**
- **MySQL**
- **MongoDB**
- **Delta Lake**

---

## 📎 Como Executar

1. Solicite acesso ao catálogo `adb_cliente_savana_prd` e Unity Catalog.
2. Inicie seu cluster Single Node.
3. Execute os notebooks na ordem:
   - `bronze_ingestao_clientes_transacoes`
   - `silver_tratamento_transacoes`
   - `gold_metricas_transacoes`

---

## 🧪 Scripts Úteis

### Criação de Schemas
```python
spark.sql("USE CATALOG adb_cliente_savana_prd")
spark.sql("CREATE SCHEMA IF NOT EXISTS elenir_bronze")
spark.sql("CREATE SCHEMA IF NOT EXISTS elenir_silver")
spark.sql("CREATE SCHEMA IF NOT EXISTS elenir_gold")
```

---

## 📥 Contato

Projeto desenvolvido com base no desafio da Savana Tech e BlueShift.
