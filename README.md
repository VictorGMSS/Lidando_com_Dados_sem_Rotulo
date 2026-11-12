# Lidando com Dados sem Rotulo

Aqui está uma proposta completa, clara e bem estruturada para o `README.md` do seu projeto, cobrindo tanto a etapa de exploração e modelagem no notebook quanto a aplicação web interativa com Streamlit.

---

# 🎯 Clusterização de Dados de Marketing: Segmentação de Perfis sem Rótulo

Projeto desenvolvido durante o curso **"Clusterização: Lidando com dados sem rótulo"**. O objetivo é explorar técnicas de aprendizado não supervisionado utilizando o algoritmo **K-Means** para identificar padrões de comportamento e agrupar perfis de usuários a partir de seus interesses e características demográficas, culminando na criação de uma aplicação web interativa com **Streamlit** para classificação em tempo real.

---

## 📋 Sobre o Projeto

Trabalhar com dados sem rótulo (*unsupervised learning*) exige estratégias específicas para preparar as variáveis, definir o número ideal de grupos e validar a qualidade das divisões criadas. Neste projeto, analisamos uma base de dados de marketing (`dados_mkt.csv`) contendo **12.992 registros** e **27 atributos**, incluindo informações demográficas (sexo, idade, número de amigos) e frequência de menções a diversos interesses (esportes, música, moda, marcas e consumo).

### 🎯 Objetivos Alcançados

* **Exploração e Pré-processamento:** Tratamento de variáveis categóricas com `OneHotEncoder` e normalização de escala com `MinMaxScaler`.


* **Modelagem:** Implementação do algoritmo de agrupamento `KMeans`.


* **Avaliação e Otimização:** Análise de performance utilizando **Inércia** (Método do Cotovelo) e **Coeficiente de Silhueta** (*Silhouette Score* global e por amostra).


* **Escolha do Melhor $K$:** Comparação entre dados brutos e dados escalados, elevando o *Silhouette Score* de `0.380` para **`0.745`** ao definir **$K = 3$** clusters.


* **Deploy Interativo:** Exportação dos transformadores (`encoder.pkl` e `scaler.pkl`) e do modelo treinado para integração em uma aplicação web com **Streamlit**, permitindo upload e previsão em tempo real para novos conjuntos de dados.



---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3


* **Manipulação e Análise de Dados:** `pandas`, `numpy`


* **Machine Learning:** `scikit-learn` (`KMeans`, `OneHotEncoder`, `MinMaxScaler`, `silhouette_score`, `silhouette_samples`)


* **Visualização de Dados:** `matplotlib`, `seaborn`


* **Serialização de Modelos:** `joblib`


* **Aplicação Web:** `streamlit`



---

## 📊 Metodologia e Resultados

1. **Pré-processamento Inicial:**
* A coluna categórica `sexo` (`F`, `M`, `NE`) foi transformada via `OneHotEncoder`.


* O artefato foi salvo em `encoder.pkl` para garantir consistência na inferência.




2. **Baseline (Dados sem Escala):**
* Avaliando valores de $K$ entre 2 e 20, o melhor resultado sem normalização ocorreu em $K = 2$, com *Silhouette Score* de `0.380` e inércia elevada (`24.912.957,59`), indicando forte distorção causada pelas diferentes escalas das variáveis (ex.: `numero_de_amigos` variando até 605 enquanto variáveis binárias variam entre 0 e 1).




3. **Otimização com Escalonamento (`MinMaxScaler`):**
* Após normalizar todas as *features* para o intervalo $[0, 1]$ (salvando o transformador em `scaler.pkl`), a separação entre os grupos melhorou drasticamente.


* Com **$K = 3$**, o modelo atingiu um **Silhouette Score médio de `0.745**`, demonstrando clusters bem definidos e coesos.





---

## 📁 Estrutura de Arquivos

```text
├── notebooks/
│   └── clusterizacao_mkt.ipynb   # Análise exploratória, testes de K, gráficos e exportação dos artefatos
├── models/
│   ├── encoder.pkl               # OneHotEncoder treinado para a variável 'sexo'
│   ├── scaler.pkl                # MinMaxScaler treinado para normalização das features
│   └── modelo_kmeans.pkl         # Modelo K-Means final (k=3)
├── app.py                        # Aplicação web interativa em Streamlit
├── dados_mkt.csv                 # Conjunto de dados utilizado no treinamento
├── requirements.txt              # Dependências do projeto
└── README.md                     # Documentação do projeto

```

---

## 🚀 Como Executar o Projeto

### 1. Pré-requisitos

Certifique-se de ter o Python 3.8+ instalado. Clone o repositório e instale as dependências:

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
pip install -r requirements.txt

```

*(Caso ainda não tenha um `requirements.txt`, instale diretamente: `pip install pandas numpy matplotlib seaborn scikit-learn joblib streamlit`)*

### 2. Executando o Notebook

Abra o arquivo `.ipynb` no Jupyter Notebook, VS Code ou Google Colab para acompanhar toda a análise exploratória, visualizar os gráficos de cotovelo e silhueta, e gerar os arquivos `.pkl`.

### 3. Executando a Aplicação Web (Streamlit)

Para iniciar a interface interativa e realizar previsões em tempo real com novos arquivos CSV:

```bash
streamlit run app.py

```

A aplicação abrirá automaticamente no seu navegador (geralmente em `http://localhost:8501`), onde você poderá carregar uma nova base de dados, aplicar automaticamente o `encoder.pkl` e o `scaler.pkl`, visualizar a distribuição dos clusters gerados e baixar os resultados.

---
## 👨‍💻 Informações pessoais

Victor Gabriel Martins e Souza

* 💼 LinkedIn: [https://www.linkedin.com/in/victorgms](https://www.linkedin.com/in/victorgms)
* 🌐 Portfólio: [https://verxstech.vercel.app](https://verxstech.vercel.app)
## 📌 Fonte dos Dados

Os dados utilizados neste projeto foram obtidos a partir do repositório do curso (`dados_mkt.csv`).
