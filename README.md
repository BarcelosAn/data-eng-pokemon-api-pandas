<p align="center">
  <img src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="PokéAPI Logo" width="200"/>
</p>

# 📊 Projeto de Análise Pokémon com Python + Pandas + Jupyter Notebook

Este projeto realiza a extração e análise de dados da [PokeAPI](https://pokeapi.co), utilizando **Python**, **Pandas** e **Jupyter Notebook** para tratamento, organização e exploração interativa das informações. Os dados coletados são transformados em um modelo relacional e exportados em arquivos `.csv`, prontos para análise em Power BI, Excel ou qualquer ferramenta de BI.

> ✅ Versão pensada para usuários fora do Databricks, utilizando apenas bibliotecas Python tradicionais e execução no Jupyter Notebook.

---
## 🚀 Antes de começar a explicação do projeto, vamos para a instalação

1. **Criar um ambiente virtual Python**
   Cria um ambiente isolado para evitar conflitos entre bibliotecas de outros projetos.

   ```bash
   python -m venv .venv
   ```

2. **Ativar o ambiente virtual**
   Faz com que todas as instalações de pacotes ocorram apenas dentro deste ambiente.
   *(No Windows)*

   ```bash
   .venv/Scripts/activate
   ```

   *(No macOS/Linux)*

   ```bash
   source .venv/bin/activate
   ```

3. **Instalar as dependências do projeto**
   Baixa e instala automaticamente todas as bibliotecas listadas no arquivo `requirements.txt`.

   ```bash
   pip install -r requirements.txt
   ```

4. **Criar as pastas para organização dos dados**
   Crie as pastas **raw**, **silver** e **gold** na raiz do projeto para armazenar as diferentes camadas dos dados durante o pipeline de engenharia:

   * `raw`: dados brutos extraídos da API, sem modificações
   * `silver`: dados intermediários, tratados e transformados
   * `gold`: dados finais prontos para análise e exportação

   Você pode criar as pastas manualmente ou via terminal:

   ```bash
   mkdir raw 
   mkdir silver
   mkdir gold
   ```

5. **Abrir o Jupyter Notebook**
   Inicia a interface interativa para executar o código passo a passo.

   ```bash
   jupyter notebook
   ```

   Após rodar este comando, o Jupyter abrirá no navegador. Basta selecionar o arquivo `.ipynb` do projeto e começar a explorar.

---


## 🏗️ Arquitetura do Pipeline (Modelo de Medalhão)

```
API (pokeapi.co)
     │
     ▼
[Bronze Layer]
  - raw_pokemon_list.json
  - raw_pokemon_descriptions.json
     │
     ▼
[Silver Layer]
  - silver_pokemon_ids (.csv)
     │
     ▼
[Gold Layer]
  - Tabelas dimensionais (.csv)
  - Tabelas de relacionamento (bridge)
```



## ⚙️ Tecnologias Utilizadas

- Python 3.8+
- requests
- pandas
- json
- concurrent.futures

## 📚 Notebooks do Projeto

| Ordem | Notebook                      | Camada   | Descrição |
|-------|-------------------------------|----------|-----------|
| 1     | `01_bronze_extract_list`      | Bronze   | Extrai todos os Pokémons da API, com nome e link para detalhes. |
| 2     | `02_silver_transform_ids`     | Silver   | Extrai IDs e nomes dos Pokémons e salva em Delta. |
| 3     | `03_bronze_extract_details`   | Bronze   | Extrai dados completos (imagem, status, habilidades, movimentos) para cada Pokémon. |
| 4     | `04_gold_transform_final_data`| Gold     | Gera tabelas estruturadas de dimensão e relacionamento para análise. |

## 📦 Tabelas Geradas (Gold)

### 🔹 Tabelas Dimensionais

  | Tabela             | Descrição |
  |--------------------|-----------|
  | `dim_pokemons.csv` | ID, nome e URL da imagem do Pokémon |
  | `dim_habilidades.csv` | Nome da habilidade e ID do Pokémon |
  | `dim_movimentos.csv`  | Nome do movimento e ID do Pokémon |
  | `dim_status.csv`      | Status base com colunas: `hp`, `attack`, `defense`, `special_attack`, `special_defense`, `speed` e ID do Pokémon |

### 🔗 Tabelas de Relacionamento (Bridge)

| Tabela                      | Descrição |
|-----------------------------|-----------|
| `rel_pokemons_habilidade.csv` | Relaciona Pokémon com suas habilidades (N:N) |
| `rel_pokemons_movimentos.csv` | Relaciona Pokémon com seus movimentos (N:N) |




## 📊 Pronto para BI

Todas as tabelas `.csv` geradas estão organizadas em `gold/` e podem ser usadas diretamente em Power BI, Excel ou qualquer ferramenta de análise.



## 💡 Possível Arquitetura em Produção

Se este pipeline fosse executado em ambiente corporativo com recursos, ele poderia ser:

- Orquestrado via **Azure Data Factory** ou **Airflow**
- Executado em **Databricks** com notebooks interligados
- Dados armazenados como **Delta Lake** em Azure Data Lake
- Monitoramento com **logs e alertas por e-mail** via Power Automate
- Análise conectada diretamente ao **Power BI** via Lakehouse


## 🔍 Futuras Melhorias

- Adicionar **tratamento de exceções e retries** com backoff
- Criar **sistema de logging estruturado**
- Implementar **testes de qualidade dos dados**
- Adicionar **interface gráfica (Streamlit)** para visualização rápida
- Exportar para banco de dados (SQLite, PostgreSQL)

## 📁 Estrutura de Diretórios

```
pokemon_api_project/
├── 01_bronze_extract_list.py
├── 02_silver_transform_ids.py
├── 03_bronze_extract_details.py
├── 04_gold_transform_final_data.py
├── raw/
│   ├── pokemon_list_raw.json
│   └── desc_list_raw.json
├── silver/
│   └── silver_pokemon_ids.csv
└── gold/
│   ├── dim_pokemons.csv
│   ├── dim_habilidades.csv
│   ├── dim_movimentos.csv
│   ├── dim_status.csv
│   ├── rel_pokemons_habilidade.csv
│   └── rel_pokemons_movimentos.csv
├── README.md
```

## 🤝 Contribuição

Este projeto faz parte do meu portfólio de estudos com foco em engenharia de dados. Sugestões e feedbacks são muito bem-vindos!


## ✍️ Autor

**Bruno Barcelos**  
Engenheiro de Dados | Python • Pandas • Spark • Databricks • APIs  
[LinkedIn](#) | [Portfólio](#)