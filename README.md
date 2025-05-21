# ✈️ Transformando Dados de Ocorrências Aéreas em Insights Regionais com Databricks

Transformei dados brutos da **ANAC** em uma base de dados analítica, limpa e confiável, utilizando **Azure Data Lake**, **Databricks** (com PySpark) e arquitetura de dados moderna com **Bronze, Silver e Gold**.





## Arquitetura da Solução

<p align="center">
  <img src="https://raw.githubusercontent.com/CrisSantosDB/pipeline-anac-azure-databricks/main/medalhao.jpg" width="800"/>
</p>






---

## 💼 Objetivo de Negócio

Reduzir o tempo gasto por analistas estaduais com limpeza e preparação de dados sobre **ocorrências aéreas no Brasil**, oferecendo uma base final intuitiva e pronta para análise — com destaque para a **ocorrência de lesões por Estado (UF)**.

---

## ⚙️ Tecnologias Usadas

- **Azure Storage (Data Lake Gen2)**
- **Azure Databricks (PySpark)**
- **Arquitetura em camadas (Bronze / Silver / Gold)**

---

## 🧱 Arquitetura do Projeto

### 🟫 Bronze – Dados Brutos
Importação direta do dataset `V_OCORRENCIA_AMPLA.json` da ANAC. Nenhuma transformação aplicada.

---

### 🟪 Silver – Dados Tratados
- Preenchimento de valores nulos com `"Sem Registro"` para colunas de texto.
- Conversão de colunas numéricas (relacionadas a lesões) de string para inteiro.
- Preenchimento de nulos com `0` nessas colunas.
- Salvamento no formato **Parquet**, pronto para agregações e filtros.

> 💡 Resultado: dados estruturados e tipados, com consistência de valores faltantes.

---

### 🟨 Gold – Base Final para Análise
- Seleção apenas das colunas solicitadas pelos analistas.
- Criação da coluna `Total_Lesoes` com a soma de todas as lesões (fatais, graves, leves, desconhecidas).
- Renomeação das colunas para nomes mais simples e intuitivos.
- Filtro para remover Estados com classificação "Indeterminado", "Sem Registro" e "Exterior".
- Adição da coluna `Atualizacao` com data/hora da atualização (timezone: São Paulo).
- Escrita em Parquet particionado por `Estado (UF)` para melhorar performance de leitura.

> ✅ Base final simples, intuitiva e pronta para dashboards ou análises com Power BI, Synapse ou ferramentas de BI.

---

## 📈 Impacto de Negócio

- **Redução de +70%** no tempo de preparação dos dados pelos analistas estaduais.
- Eliminação de dados inválidos e inconsistentes.
- Criação de uma métrica-chave: **Total de Lesões por Ocorrência**, facilitando a priorização de investigações.
- **Organização por Estado** permite análises regionais imediatas.
---
## ⚙️ Pipeline no Azure Data Factory (ADF)

- Uma pipeline simples foi criada com o Azure Data Factory com o objetivo de praticar a orquestração de processos no ambiente Azure.
- Embora o processamento principal tenha sido feito diretamente no Databricks, a inclusão do ADF mostra a possibilidade de integração entre os serviços e reforça minha familiaridade com ferramentas de orquestração em nuvem.
---
## 🗂️ Estrutura do Repositório

├── Anac/                           # Dados utilizados no projeto


├── Notebooks - Desenvolvimento/   # Notebooks usados para testes e desenvolvimento inicial


├── Notebooks - Produção/          # Versões finais dos notebooks utilizados em produção


├── pipeline/                      # Pipeline criada com Azure Data Factory para orquestração de testes no fluxo de dados


├── trigger/                       # Trigger de agendamento para a execução da pipeline


├── README.md                      # Documentação do projeto


├── publish_config.json           # Configurações de publicação do ADF




