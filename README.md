# 🌍 Global Health Monitor: COVID-19 & Data Modeling

![Status](https://img.shields.io/badge/Status-Concluído-success)
![Stack](https://img.shields.io/badge/Stack-Databricks%20|%20Star%20Schema%20|%20PowerBI-blue)

> **"Números absolutos mentem. Como comparar o impacto da pandemia na Índia vs. Islândia?"**

Este projeto de **BI & Analytics Engineering** resolve um problema clássico de saúde pública: a comparabilidade de dados. O objetivo foi transformar dados brutos e sujos em métricas padronizadas (Taxa de Incidência), utilizando uma modelagem dimensional robusta no Databricks.

O diferencial técnico é a implementação de um **Star Schema (Modelo Estrela)** físico na camada Gold, otimizando a performance do Power BI ao entregar Fatos e Dimensões prontos.

---

## 🖼️ Visão do Analista (Dashboard)

O painel foca na **Taxa de Incidência (Casos por 100k hab.)**, permitindo comparar a severidade da pandemia independentemente do tamanho da população.

<img width="1919" height="1079" alt="Dashboard COVID-19" src="https://github.com/user-attachments/assets/9a07f000-d6fa-4a57-a45a-0d26b715ee03" />

---

## 🧠 O Problema Analítico (Por que Engenharia?)

1.  **Dados Sujos:** Bases públicas de saúde frequentemente contêm erros, como dias com "casos negativos" (correções de base).
2.  **Escala:** Comparar o volume absoluto de casos do Brasil com o de Portugal gera distorções.
3.  **Performance:** Calcular agregações complexas em milhões de linhas dentro da ferramenta de visualização (Power BI) degrada a experiência do usuário.

---

## 🛠️ A Solução: Dimensional Modeling no Lakehouse

Em vez de apenas "limpar dados", atuei como Arquiteto de BI construindo o modelo final dentro do Databricks (**Shift Left**).

### 1. Tratamento e Métricas (Silver)
* **Data Quality:** Regra de negócio para tratar valores negativos (`daily_new_cases < 0`), garantindo a integridade analítica.
* **Métrica de Negócio:** Cálculo da *Incidence Rate* (`(Casos / População) * 100.000`), normalizando os dados para análise geográfica justa.
* [Ver código Silver](silver.ipynb)

### 2. Modelagem Estrela (Gold)
Aqui está o diferencial. Transformei a tabela única (flat table) em um modelo relacional otimizado para OLAP:
* **Fato (`fact_daily_metrics`):** Contém apenas as chaves (`iso_code`, `date_key`) e as métricas numéricas.
* **Dimensões (`dim_country`, `dim_date`):** Tabelas auxiliares para filtros e categorização (Continente, Dia da Semana, Mês).
* **Performance:** Uso de `ZORDER BY (iso_code, date_key)` na Fato para garantir filtros instantâneos.
* [Ver código Gold](gold.ipynb)

---

## 💻 Tech Stack

* **Arquitetura:** Medallion (Bronze/Silver/Gold) com Star Schema.
* **Processamento:** PySpark & SparkSQL.
* **Governança:** Unity Catalog.
* **Visualização:** Power BI (conectado ao Modelo Dimensional).
