# 🛡️ Detecção de Fraude em Cartões de Crédito: Uma Abordagem Estatística

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Estatística](https://img.shields.io/badge/Background-Estatística-blueviolet?style=flat)
![Sklearn](https://img.shields.io/badge/Lib-Scikit--Learn-orange?style=flat&logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Concluído-green?style=flat)

> **Contexto Acadêmico:** Este projeto foi desenvolvido aplicando o rigor metodológico do **Bacharelado em Estatística**, focando não apenas na predição, mas na inferência, prevenção de vieses e interpretabilidade de modelos em cenários de eventos raros.

---

## 🎯 O Problema de Negócio
Fraudes em cartões de crédito são eventos de **cauda longa** (apenas 0.17% das transações neste dataset são fraudes).
* **O Desafio:** Um modelo que classifica *tudo* como "não-fraude" teria 99.8% de acurácia, mas falharia completamente em proteger o banco.
* **O Objetivo:** Maximizar a detecção de fraudes (Recall) sem gerar um número excessivo de alarmes falsos (Precision), otimizando o retorno financeiro.

---

## 🧠 Diferenciais Técnicos e Metodologia
Diferente de abordagens padrão, este projeto utiliza técnicas avançadas para garantir robustez estatística:

### 1. Prevenção de Data Leakage (Vazamento de Dados)
Utilização de **Scikit-Learn Pipelines**.
* **O erro comum:** Normalizar os dados (StandardScaler) antes de dividir treino/teste. Isso "contamina" o treino com informações da média/desvio do teste.
* **Nossa abordagem:** O Pipeline ajusta (`fit`) a normalização *apenas* nos dados de treino e aplica (`transform`) no teste, simulando um cenário real de produção.

### 2. Otimização de Threshold (Ponto de Corte)
A decisão de fraude não segue o padrão arbitrário de $P(x) > 0.5$.
* Utilizamos a **Curva Precision-Recall** para encontrar matematicamente o limiar que maximiza o **F1-Score**.
* **Resultado:** O modelo ajustado detecta mais fraudes com maior segurança do que o modelo padrão.

### 3. Análise Exploratória (EDA) Focada
Investigação visual das distribuições das componentes principais (PCA) para entender a separabilidade das classes.

---

## 📊 Principais Insights (EDA)

A análise univariada e bivariada revelou que certas variáveis transformadas (PCA) são discriminantes fortíssimos para fraude.

### Correlação e Distribuição
As variáveis `V17`, `V14` e `V12` apresentaram comportamento distinto:
* **Transações Normais:** Distribuição centrada em zero.
* **Fraudes:** Distribuição deslocada para a esquerda (valores negativos extremos) e com maior variância.

*(Espaço reservado: Cole aqui o print dos seus Boxplots gerados pelo código)*

---

## 📈 Resultados do Modelo

O modelo final (**Random Forest com Pesos Balanceados**) obteve performance superior após a calibração do threshold.

| Métrica | Performance (Threshold Otimizado) | Interpretação |
| :--- | :--- | :--- |
| **ROC - AUC** | **0.97** | Alta capacidade de separação entre classes. |
| **Recall** | **Alto** | O modelo captura a grande maioria das fraudes reais. |
| **F1-Score** | **Maximizado** | Melhor equilíbrio harmônico entre precisão e sensibilidade. |

### Interpretabilidade (XAI)
Utilizando **SHAP Values**, confirmamos que o modelo não é uma "caixa preta". As variáveis que mais impactam a decisão do modelo (V17, V14) são as mesmas identificadas na análise exploratória estatística.


---

## 🛠️ Tecnologias
* **Linguagem:** Python
* **Manipulação:** Pandas, NumPy
* **Machine Learning:** Scikit-Learn (Pipeline, RandomForest, Metrics)
* **Estatística Visual:** Seaborn, Matplotlib
* **Explainable AI:** SHAP

---

## 🚀 Como Executar

1. Clone o repositório:
   ```bash
   git clone [https://github.com/igorcarvah/deteccao-fraude-bancaria.git](https://github.com/igorcarvah/deteccao-fraude-bancaria.git)