# 🎯 Clusterização de Dados de Marketing: Segmentação de Perfis sem Rótulo

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1WdUbi6qiaO8QAXutEhXcqixruGxtmjZ-)

Projeto prático desenvolvido durante o curso **"Clusterização: Lidando com dados sem rótulo"**. O objetivo deste repositório é explorar técnicas de aprendizado não supervisionado utilizando o algoritmo **K-Means** para identificar padrões de comportamento e agrupar perfis de usuários a partir de seus interesses e características demográficas, culminando na criação de uma aplicação web interativa com **Streamlit** para classificação em tempo real.

Trabalhar com dados sem rótulo (*unsupervised learning*) exige estratégias específicas para preparar as variáveis, definir o número ideal de grupos e validar a qualidade das divisões criadas. Neste projeto, analisamos uma base de dados de marketing (`dados_mkt.csv`) contendo **12.992 registros** e **27 atributos**, incluindo informações demográficas (sexo, idade, número de amigos) e frequência de menções a diversos interesses (esportes, música, moda, marcas e consumo).

---

## 🎯 Objetivos do Projeto

* **Exploração e Pré-processamento:** Tratamento de variáveis categóricas com `OneHotEncoder` e normalização de escala com `MinMaxScaler`.
* **Modelagem:** Implementação do algoritmo de agrupamento `KMeans`.
* **Avaliação e Otimização:** Análise de performance utilizando **Inércia** (Método do Cotovelo) e **Coeficiente de Silhueta** (*Silhouette Score* global e por amostra).
* **Escolha do Melhor $K$:** Comparação entre dados brutos e dados escalados, elevando o *Silhouette Score* de `0.380` para **`0.745`** ao definir **$K = 3$** clusters.
* **Deploy Interativo:** Exportação dos transformadores (`encoder.pkl` e `scaler.pkl`) e do modelo treinado para integração em uma aplicação web com **Streamlit**, permitindo upload e previsão em tempo real para novos conjuntos de dados.

---

## 🗂️ Estrutura do Repositório

* `notebooks/clusterizacao_mkt.ipynb`: Notebook com a análise exploratória, testes de $K$, gráficos e exportação dos artefatos.
* `models/encoder.pkl`: `OneHotEncoder` treinado para a variável `sexo`.
* `models/scaler.pkl`: `MinMaxScaler` treinado para normalização das *features*.
* `models/modelo_kmeans.pkl`: Modelo K-Means final ($K = 3$).
* `app.py`: Aplicação web interativa em Streamlit.
* `dados_mkt.csv`: Conjunto de dados utilizado no treinamento, obtido a partir do repositório do curso.
* `requirements.txt`: Dependências do projeto.

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas

* **Python 3**
* **Pandas & NumPy:** Manipulação e análise dos dados.
* **Scikit-Learn:** Modelagem e avaliação (`KMeans`, `OneHotEncoder`, `MinMaxScaler`, `silhouette_score`, `silhouette_samples`).
* **Matplotlib & Seaborn:** Visualização dos dados e dos gráficos de cotovelo e silhueta.
* **Joblib:** Serialização dos modelos e transformadores.
* **Streamlit:** Aplicação web para previsões em tempo real.

---

## 🚀 Etapas Desenvolvidas no Notebook

1. **Pré-processamento Inicial:** Transformação da coluna categórica `sexo` (`F`, `M`, `NE`) com `OneHotEncoder`, salvando o artefato em `encoder.pkl` para garantir consistência na inferência.
2. **Baseline (Dados sem Escala):** Avaliação de valores de $K$ entre 2 e 20. O melhor resultado sem normalização ocorreu em $K = 2$, com *Silhouette Score* de `0.380` e inércia elevada (`24.912.957,59`), indicando forte distorção causada pelas diferentes escalas das variáveis (ex.: `numero_de_amigos` variando até 605 enquanto variáveis binárias variam entre 0 e 1).
3. **Otimização com Escalonamento (`MinMaxScaler`):** Normalização de todas as *features* para o intervalo $[0, 1]$ (salvando o transformador em `scaler.pkl`), o que melhorou drasticamente a separação entre os grupos. Com **$K = 3$**, o modelo atingiu um *Silhouette Score* médio de **`0.745`**, demonstrando clusters bem definidos e coesos.
4. **Exportação e Deploy:** Salvamento do modelo final e dos transformadores para uso na aplicação Streamlit.

---

## 💻 Como Executar

1. **Via Google Colab (Recomendado):** Clique no botão **"Open in Colab"** no topo deste README para abrir e executar o notebook diretamente no navegador sem precisar configurar ambiente local.
2. **Localmente:** Certifique-se de ter o Python 3.8+ instalado, clone o repositório e instale as dependências:
```bash
git clone https://github.com/VictorGMSS/[NOME-DO-REPOSITORIO].git
cd [NOME-DO-REPOSITORIO]
pip install -r requirements.txt
```
Caso ainda não tenha um `requirements.txt`, instale diretamente: `pip install pandas numpy matplotlib seaborn scikit-learn joblib streamlit`. Em seguida, abra o notebook `clusterizacao_mkt.ipynb` no Jupyter Notebook, VS Code ou Google Colab para acompanhar a análise e gerar os arquivos `.pkl`.
3. **Aplicação Web (Streamlit):** Para iniciar a interface interativa e realizar previsões em tempo real com novos arquivos CSV:
```bash
streamlit run app.py
```
A aplicação abrirá automaticamente no navegador (geralmente em `http://localhost:8501`), onde você poderá carregar uma nova base de dados, aplicar automaticamente o `encoder.pkl` e o `scaler.pkl`, visualizar a distribuição dos clusters gerados e baixar os resultados.

---

## 👨‍💻 Informações pessoais

Victor Gabriel Martins e Souza

* 💼 LinkedIn: [https://www.linkedin.com/in/victorgms](https://www.linkedin.com/in/victorgms)
* 🌐 Portfólio: [https://verxstech.vercel.app](https://verxstech.vercel.app)
