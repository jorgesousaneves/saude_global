# 📊 Monitoramento Global de Saúde Pública (COVID-19)

> **Análise da evolução temporal e impacto geográfico da pandemia, com foco em métricas de incidência e volume.**

![Status](https://img.shields.io/badge/Status-Concluído-success)
![Stack](https://img.shields.io/badge/Stack-Unity%20Catalog%20|%20PySpark%20|%20PowerBI-blue)

## 🖼️ Visão Geral do Dashboard
<img width="1919" height="1079" alt="Image" src="https://github.com/user-attachments/assets/9a07f000-d6fa-4a57-a45a-0d26b715ee03" />
---

## 💼 O Desafio de Negócio

O objetivo deste projeto foi criar um modelo de dados confiável e escalável capaz de analisar o impacto da COVID-19 em diversas regiões geográficas e ao longo do tempo. O desafio de Engenharia de Dados residiu em:
1.  Tratar grandes volumes de dados de notificação diária com alta variabilidade.
2.  Garantir a Qualidade de Dados (DQ) em métricas críticas (Casos e População).
3.  Calcular métricas proporcionais de alta complexidade (Taxa de Incidência).

---

## 🛠️ A Solução Técnica (Arquitetura Medalhão)

Construí um pipeline End-to-End em ambiente Lakehouse, garantindo governança de dados através do **Unity Catalog** (`saude_global`) e performance com o **Apache Spark**.

### Arquitetura do Pipeline

| Camada | Função Principal | Foco Técnico |
| :--- | :--- | :--- |
| **Bronze** | **Ingestão (Raw)** | Leitura da fonte (OWID) e persistência imediata. |
| **Silver** | **Tratamento e DQ** | Limpeza pesada, padronização de datas, remoção de nulos/negativos, e cálculo da **Taxa de Incidência**. |
| **Gold** | **Modelagem** | Criação do Modelo Estrela (Fact: `fact_daily_metrics`; Dims: `dim_country`, `dim_date`). |

### 💡 Insights & Conclusões (Dashboard)

O painel de BI reflete a narrativa completa da pandemia:

1.  **Evolução Temporal:** O gráfico de linhas exibe claramente as ondas e picos de contágio ao longo dos anos (2020 a 2024).
2.  **Impacto Proporcional:** O ranking por **Taxa de Incidência (Casos por 100k hab.)** revela o impacto real do vírus em relação à população de cada país, destacando regiões que enfrentaram maiores desafios proporcionais.
3.  **Contraste:** A separação visual entre Volume Absoluto (Casos) e Taxa (Incidência) garante que a análise não seja distorcida apenas pelo tamanho populacional.

---

## 💻 Tech Stack

* **Cloud & Processing:** Databricks / Apache Spark (PySpark).
* **Storage:** Delta Lake (Unity Catalog).
* **Languages:** Python, SQL, DAX.
* **Visualization:** Microsoft Power BI.# saude_global
