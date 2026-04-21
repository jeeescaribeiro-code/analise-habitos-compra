# Guia do Dashboard — Looker Studio

Dashboard: **Pesquisa de Mercado: Viabilidade de um Aplicativo de Comparação de Preços**
Autora: Jéssica Rodrigues | [LinkedIn](https://www.linkedin.com/in/jessica-ribeiro-lr/)

---

## Fonte de Dados

O dashboard usa o arquivo `habitos_compra_tratado.csv`, gerado automaticamente pela última célula do notebook.

**Como conectar ao Looker Studio:**

1. Faça upload do `habitos_compra_tratado.csv` para o Google Drive
2. No Looker Studio → clique em **Criar** → **Relatório**
3. Selecione **Google Drive** como conector → localize o arquivo CSV
4. Clique em **Adicionar** → o Looker detecta os campos automaticamente

**Campos disponíveis no CSV após o notebook:**

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `FAIXA_ETARIA` | Texto | Faixa etária do respondente |
| `GENERO` | Texto | Gênero |
| `FAIXA_SALARIAL` | Texto | Renda mensal |
| `FREQUENCIA_COMPRAS` | Texto | Com que frequência compra |
| `TIPO_COMPRA` | Texto | Presencial / Online / Ambos |
| `COMPARA_PRECOS` | Texto | Frequência de comparação |
| `FATOR_PRECO` … `FATOR_ESTACIONAMENTO` | Número | Importância dos fatores (1–5) |
| `FUNC_COMPARACAO` … `FUNC_HISTORICO` | Número | Interesse nas funções do app (1–5) |
| `USA_APP` | Texto | Já usa app de comparação? |
| `PAGARIA_PREMIUM` | Texto | Pagaria pelo plano premium? |
| `PRECO_PREMIUM` | Texto | Faixa de preço aceita |
| `ACEITA_ANUNCIOS` | Texto | Aceita anúncios no app? |
| `CANAL_*` | Número | Preferência por canal de comunicação |
| `BARREIRA_*` | Texto | Barreiras de adoção |
| `score_geral` | Número | Score combinado de exigência + interesse |
| `score_interesse_app` | Número | Score de interesse nas funcionalidades |
| `score_exigencia_mercado` | Número | Score de exigência na escolha do mercado |
| `grupo` | Número | Cluster (0, 1 ou 2) |
| `TARGET_USA_APP` | Número | 1 = usa app, 0 = não usa |
| `TARGET_PAGARIA` | Número | 1 = pagaria premium, 0 = não pagaria |

---

## Estrutura do Dashboard — 3 Páginas

---

### Página 1 — Perfil & Hábitos

**Filtros globais no topo:**
- Dropdown `FAIXA_ETARIA` (já configurado no dashboard atual)
- Tabela de controle por `GENERO` com contagem de respondentes

**Scorecards (linha superior):**

| Métrica | Campo | Tipo |
|---------|-------|------|
| Respondentes | `GENERO` → contagem | Scorecard |
| Usam app hoje | `TARGET_USA_APP` → soma | Scorecard |
| Pagariam premium | `TARGET_PAGARIA` → soma | Scorecard |
| Ticket médio previsto | — | Scorecard (valor fixo R$ 5,99) |

**Como configurar o scorecard "Usam app hoje":**
- Adicionar gráfico → Scorecard
- Métrica: `TARGET_USA_APP` → Soma
- Formato: Número inteiro

**Gráficos da Página 1:**

| Gráfico | Tipo no Looker | Dimensão | Métrica |
|---------|---------------|----------|---------|
| Distribuição por gênero | Gráfico de pizza | `GENERO` | Contagem de registros |
| Faixa etária | Gráfico de barras | `FAIXA_ETARIA` | Contagem de registros |
| Faixa salarial | Gráfico de barras horizontal | `FAIXA_SALARIAL` | Contagem de registros |
| Frequência de compras | Gráfico de barras horizontal | `FREQUENCIA_COMPRAS` | Contagem de registros |
| Hábito de compra | Gráfico de rosca | `TIPO_COMPRA` | Contagem de registros |
| Comparação de preço por gênero | Gráfico de barras empilhadas | `COMPARA_PRECOS` + `GENERO` | Contagem |

**Dica para ordenar a faixa etária corretamente:**
- No campo `FAIXA_ETARIA`, clique em "Ordenar" → escolha uma ordenação personalizada ou crie um campo calculado com ordem numérica.

---

### Página 2 — Prioridades & App

**Scorecards — O que importa no supermercado (escala 1–5):**

Para cada fator, crie um Scorecard com:
- Métrica: `FATOR_PRECO` → Média → 2 casas decimais

| Fator | Campo |
|-------|-------|
| Preço | `FATOR_PRECO` |
| Distância | `FATOR_DISTANCIA` |
| Promoções | `FATOR_PROMOCOES` |
| Variedade | `FATOR_VARIEDADE` |
| Estacionamento | `FATOR_ESTACIONAMENTO` |
| Atendimento | `FATOR_ATENDIMENTO` |

**Scorecards — Funcionalidades do app (escala 1–5):**

| Função | Campo |
|--------|-------|
| Comparação de preços | `FUNC_COMPARACAO` |
| Sugestão de compras | `FUNC_SUGESTAO` |
| Alertas de promoções | `FUNC_ALERTAS` |
| Histórico de compras | `FUNC_HISTORICO` |

**Gráficos da Página 2:**

| Gráfico | Tipo no Looker | Configuração |
|---------|---------------|--------------|
| Pessoas que usam app | Gráfico de rosca | Dimensão: `USA_APP`, Métrica: Contagem |
| Pessoas que pagariam premium | Gráfico de rosca | Dimensão: `PAGARIA_PREMIUM`, Métrica: Contagem |
| Faixa salarial × preço do app | Barras empilhadas 100% | Dimensão: `FAIXA_SALARIAL`, Detalhamento: `PRECO_PREMIUM` |

**Como criar o gráfico de faixa salarial × preço:**
1. Inserir → Gráfico de barras empilhadas
2. Dimensão: `FAIXA_SALARIAL`
3. Detalhamento: `PRECO_PREMIUM`
4. Métrica: Contagem de registros
5. Em "Estilo" → ativar "Barras 100%" para ver proporções

---

### Página 3 — Segmentos & Barreiras

**Gráficos de barreiras (donut):**

Crie um gráfico de rosca para cada barreira:

| Título | Campo |
|--------|-------|
| Confiança na informação | `BARREIRA_CONFIANCA` |
| Compra presencial | `BARREIRA_PRESENCIAL` |
| Pouco uso do aplicativo | `BARREIRA_USO` |
| Utilidade do aplicativo | `BARREIRA_UTILIDADE` |

**Gráfico de pizza — Segmentos (Clusters):**
- Tipo: Gráfico de pizza
- Dimensão: `grupo`
- Métrica: Contagem de registros
- Renomeie os rótulos no Looker: 0 = Explorador Digital, 1 = Caçador de Preço, 2 = Desengajado

**Mapa de segmentos — Interesse × Exigência (Scatter):**
- Tipo: Gráfico de dispersão
- Eixo X: `score_geral` (média)
- Eixo Y: `score_interesse_app` (média)
- Cor: `grupo`
- Tamanho da bolha: Contagem de registros

---

## Filtros Globais Recomendados

Adicione no topo de cada página os seguintes controles:

| Controle | Campo | Tipo |
|----------|-------|------|
| Faixa etária | `FAIXA_ETARIA` | Lista suspensa |
| Gênero | `GENERO` | Lista de verificação |
| Cluster | `grupo` | Lista suspensa |

**Como tornar um filtro global:**
- Clique no controle → botão direito → "Tornar filtro de página" ou "Tornar filtro de relatório"

---

## Paleta de Cores

Cores utilizadas no dashboard (tema azul da pesquisa):

| Elemento | Hex |
|----------|-----|
| Cor principal | `#4A90D9` |
| Cor secundária | `#7EC8E3` |
| Destaque | `#1A5276` |
| Fundo dos scorecards | `#EAF4FB` |
| Texto dos scorecards | `#1A5276` |

