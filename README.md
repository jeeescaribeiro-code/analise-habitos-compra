#  Pesquisa de Mercado: Viabilidade de um Aplicativo de Comparação de Preços

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-red?logo=scikit-learn&logoColor=white)
![Looker Studio](https://img.shields.io/badge/Looker_Studio-Dashboard-4285F4?logo=google&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)

> Projeto desenvolvido como trabalho acadêmico e para o mini-curso de Análise de  Dados da PrograMaria, com aplicação de análise estatística e machine learning para investigar hábitos de consumo e validar a viabilidade de uma startup de comparação de preços em supermercados. A partir de uma pesquisa com 98 respondentes e 39 variáveis, o projeto explora padrões de comportamento do consumidor, segmentação de perfis e modelos preditivos para apoiar decisões de negócio orientadas por dados.

##  Sobre o Projeto

Este projeto analisa uma pesquisa com **98 consumidores** para responder três perguntas centrais de negócio:
1. O que mais importa para o consumidor na hora de escolher um supermercado?
2. Quem usaria um app de comparação de preços, e quem pagaria pelo plano premium?
3. Quanto os usuários estariam dispostos a pagar?

Os dados foram coletados via survey online com 39 variáveis, cobrindo perfil demográfico, hábitos de compra, percepção de valor e disposição a pagar. A análise combina estatística descritiva, clusterização e modelos de machine learning supervisionados para gerar insights acionáveis.

---

##  Dashboard Looker Studio

🔗 **[Acesse o dashboard interativo aqui]([https://lookerstudio.google.com/](https://datastudio.google.com/reporting/51204db5-3124-4231-a538-d33e5749bf47))**

O dashboard possui 3 páginas:
- **Página 1 — Perfil:** distribuição demográfica e hábitos de compra
- **Página 2 — Prioridades & App:** rankings de fatores, funcionalidades e monetização
- **Página 3 — Segmentos:** clusters, barreiras e mapa de interesse × exigência

---

## Estrutura do Repositório

```
analise-habitos-compra/
│
├── projetoProgramaria_final.ipynb   # Notebook principal — análise completa
├── habitos_de_compra.xlsx           # Dados brutos da pesquisa
├── habitos_compra_tratado.csv       # Dados tratados — fonte do dashboard Looker
│
├── dashboard/
│   └── looker_instrucoes.md         # Guia de configuração do Looker Studio
│
├── requirements.txt                 # Dependências do projeto
└── README.md                        # Este arquivo
```

---

##  Metodologia

### 5 partes do notebook

| Parte | Conteúdo | Técnicas |
|-------|----------|----------|
| 1 — Fundação | Carregamento, limpeza, tratamento de nulos | Pandas, `fillna`, renomeação |
| 2 — Exploratória | Filtros, agrupamentos, estatísticas por grupo | `groupby`, `value_counts`, outliers IQR |
| 3 — Insights | Rankings, correlação, cruzamentos, testes | Heatmap, T-test, ANOVA, Chi², V de Cramér |
| 4 — Segmentação | Clusterização + personas automáticas | KMeans, StandardScaler, radar chart |
| 5 — Machine Learning | 3 modelos preditivos + simulador | Random Forest, SMOTE, cross-validation |

### Modelos de Machine Learning

| Modelo | Pergunta | Algoritmo | Resultado |
|--------|----------|-----------|-----------|
| Classificação 1 | Vai usar o app? | Random Forest + SMOTE | F1 ≈ 0.88 |
| Classificação 2 | Vai pagar pelo premium? | Random Forest | F1 ≈ 0.55 |
| Regressão | Quanto pagaria? | Random Forest Regressor | MAE ≈ R$ 6,00 |

> **Por que SMOTE?** A base tem desbalanceamento severo na variável alvo (86 não usam app × 12 usam). O SMOTE gera amostras sintéticas da classe minoritária, permitindo que o modelo aprenda padrões que seriam ignorados com os dados originais.

---

## Principais Insights

**O consumidor prioriza preço acima de tudo.** A média de importância de `FATOR_PRECO` foi 4.29/5 — o maior entre todos os fatores de escolha do supermercado. No app, a funcionalidade mais desejada foi comparação de preços em tempo real (4.11/5).

**O mercado de apps comparadores está praticamente inexplorado.** Apenas 12% dos respondentes já usam algum app similar, o que representa uma janela de oportunidade grande. Ainda assim, metade (50%) pagaria pelo plano premium — o que valida a hipótese de monetização.

**Quem tem dificuldade em comparar preços é o melhor alvo.** Esse grupo apresenta maior score de interesse no app e maior propensão a adoção. A dor é real e o produto resolve diretamente.

**A lógica de uso é diferente da lógica de pagamento.** Usuários mais jovens e de menor renda são os mais engajados nas funcionalidades gratuitas. Já a conversão para o premium é mais forte em usuários de maior renda — que buscam conveniência, não economia de centavos.

**Três segmentos de usuários identificados:**
- 🔵 **Exploradores Digitais (43.9%)** — alta exigência, alto interesse no app, alvo primário
- 🟤 **Caçadores de Preço (38.8%)** — foco em custo, usariam o app para economizar
- 🟣 **Desengajados (17.3%)** — baixo interesse, precisam de onboarding forte

**Canais prioritários para aquisição:** WhatsApp e Instagram lideram. Programa de indicação tem alto potencial dado o perfil da base.

---

##  Como Rodar o Projeto

### 1. Clone o repositório

```bash
git clone https://github.com/SEU_USUARIO/analise-habitos-compra.git
cd analise-habitos-compra
```

### 2. Instale as dependências

```bash
pip install -r requirements.txt
```

### 3. Abra o notebook

```bash
jupyter notebook projetoProgramaria_final.ipynb
```

> **Google Colab:** você também pode abrir direto no Colab. Faça o upload do arquivo `.xlsx` para o Google Drive e ajuste o caminho de carregamento na célula de setup.

### 4. Exporte os dados tratados

Execute todas as células até o final do notebook — a última célula exporta automaticamente o arquivo `habitos_compra_tratado.csv`, que é a fonte de dados do dashboard Looker.

---

##  Tecnologias Utilizadas

- **Python 3.10+**
- **Pandas** — manipulação e limpeza de dados
- **NumPy** — operações numéricas
- **Matplotlib / Seaborn** — visualização de dados
- **Scikit-learn** — KMeans, Random Forest, métricas
- **Imbalanced-learn** — SMOTE para balanceamento de classes
- **SciPy** — testes estatísticos (T-test, ANOVA, Chi-quadrado)
- **Looker Studio** — dashboard interativo

---

## ⚠️ Limitações

- **Tamanho da amostra:** 98 respondentes é suficiente para análise exploratória e prova de conceito, mas pequeno para modelos de ML robustos. Com mais dados, os modelos de classificação e regressão ganhariam estabilidade e generalização.
- **Viés de amostragem:** 72% dos respondentes são do sexo feminino, o que pode não representar a população geral de consumidores.
- **Dados de survey:** respostas em escala Likert carregam subjetividade. A transformação para escala numérica (1–3–5) é uma aproximação.

---

## 👩‍💻 Autora

**Jéssica Rodrigues**
Projeto acadêmico desenvolvido na Universidade Federal de Uberlândia

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Jéssica_Rodrigues-0077B5?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jessica-ribeiro-lr/)


