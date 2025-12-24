
# 🌡️ Análise de Temperatura no Rio de Janeiro (RJ)

Este projeto realiza uma  **análise exploratória de dados climáticos** , focada na  **temperatura média no Rio de Janeiro** , utilizando  **Python** , **Pandas** e  **Matplotlib** .

O objetivo é analisar o comportamento da temperatura ao longo do tempo, identificar  **padrões sazonais** ,  **anos mais quentes e mais frios** , além de gerar  **visualizações e arquivos de saída** .

---

## 📌 Tecnologias Utilizadas

* Python 3
* Pandas
* Matplotlib
* VS Code
* Jupyter Notebook

---

## 📂 Estrutura do Projeto

```
📁 projeto
│
├── 📁 data
│   └── temperatura-RJ.csv
│
├── 📁 results
│   ├── temperatura_anual_rj.png
│   └── temperatura_anual_rj_dados.xlsx
│
├── analise_temperatura.ipynb
└── README.md
```

---

## 📥 Carregamento dos Dados

Os dados são carregados a partir de um arquivo CSV, ignorando linhas iniciais irrelevantes:

```python
tempo_df = pd.read_csv('../data/temperatura-RJ.csv', skiprows=3)
```

---

## 🧹 Tratamento dos Dados

### Definição da coluna de tempo como índice

```python
tempo_df.set_index('time', inplace=True)
```

### Conversão do índice para formato datetime

```python
tempo_df.index = pd.to_datetime(tempo_df.index)
```

---

## 🔍 Análise Exploratória

### Verificação de tipos e estrutura

```python
tempo_df.info()
```

### Verificação de valores nulos

```python
(tempo_df.isna() | tempo_df.isnull() | tempo_df == "").sum()
```

### Estatísticas descritivas

```python
tempo_df.describe()
```

### Detecção de outliers

```python
tempo_df.plot(kind='box')
```

---

## ❄️🔥 Dias Mais Frios e Mais Quentes

Identificação dos dias com menor e maior temperatura média:

```python
coldest_day = tempo_df['temperature_2m_mean (°C)'].idxmin()
hottest_day = tempo_df['temperature_2m_mean (°C)'].idxmax()
```

---

## 📆 Análises Temporais

### 📊 Médias Mensais

```python
monthly_avg = tempo_df.groupby(tempo_df.index.month).mean()
monthly_avg.plot()
```

### 📊 Médias Anuais

```python
yearly_avg = tempo_df.groupby(tempo_df.index.year).mean()
yearly_avg.plot()
```

---

## 🏆 Anos Mais Quentes e Mais Frios

O ano de 2025 foi removido por conter dados incompletos:

```python
hottest_year = yearly_avg.drop(2025).idxmax()
coldest_year = yearly_avg.idxmin()
```

---

## 📈 Visualização Gráfica

* Estilo escuro (`dark_background`)
* Gráfico anual personalizado
* Salvamento automático do gráfico

```python
fig.savefig('../results/temperatura_anual_rj.png')
```

---

## 📤 Exportação de Dados

Exportação das médias anuais para Excel:

```python
annual_data.to_excel('../results/temperatura_anual_rj_dados.xlsx')
```

---

## 🎯 Conclusão

Este projeto demonstra:

* Manipulação e limpeza de dados com Pandas
* Uso de **índices temporais**
* Análise estatística descritiva
* Visualização de dados climáticos
* Organização de resultados para relatórios
