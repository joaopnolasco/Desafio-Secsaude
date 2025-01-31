# Desafio-Secsaude

# Desafio Pipeline de Dados - Secretaria de Saúde do Recife
**Vaga**: Engenheiro de Dados Júnior - GGMA  
**Data**: 31/01/2025  
**Candidato**: João Paulo Oliveira Nolasco

---

## Índice

- [Introdução](#introdução)
- [Descrição dos Dados](#descrição-dos-dados)
  - [Fontes de Dados](#fontes-de-dados)
  - [Motivo da Escolha dos Dados](#motivo-da-escolha-dos-dados)
- [Arquitetura do Pipeline de Dados](#arquitetura-do-pipeline-de-dados)
  - [Arquitetura Medalhão](#arquitetura-medalhão)
  - [Aplicação da Arquitetura Medalhão](#aplicação-da-arquitetura-medalhão)
- [Ambiente e Ferramentas Utilizadas](#ambiente-e-ferramentas-utilizadas)
- [Processo de Extração e Transformação](#processo-de-extração-e-transformação)
  - [Extração dos Dados](#extração-dos-dados)
  - [Transformação dos Dados](#transformação-dos-dados)
- [Consultas](#consultas)
  - [Descrição das Consultas SQL](#descrição-das-consultas-sql)
  - [Justificativa para Escolha das Consultas](#justificativa-para-escolha-das-consultas)
- [Conclusão](#conclusão)
- [Reflexões Finais](#reflexões-finais)

---

## Introdução
Este repositório contém o projeto de construção de um **pipeline de dados** para análise de informações sobre medicamentos disponibilizados pela **Secretaria de Saúde do Recife**. O objetivo é extrair dados públicos, transformá-los para adequação analítica e carregá-los em um banco de dados para facilitar consultas e análises. O pipeline segue a **Arquitetura Medalhão**, que organiza os dados em camadas **Bronze**, **Silver** e **Gold**.

---

## Descrição dos Dados

### Fontes de Dados
Os dados utilizados foram extraídos do portal de dados públicos da Prefeitura do Recife, especificamente do conjunto de dados sobre medicamentos distribuídos no município. O arquivo contém informações sobre:
- Nome do produto
- Quantidade distribuída
- Bairro de distribuição
- Classe do medicamento
- Entre outras.

**Link para a fonte dos dados**: [Portal de Dados Recife - Medicamentos](http://dados.recife.pe.gov.br/dataset/443797b4-5c9c-421c-8509-62eb7e6d2fc9/resource/4c52c602-6b6f-4ca5-bcb9-a64248578058/download/medicamentos.csv)

### Motivo da Escolha dos Dados
Escolhi esse conjunto de dados por sua relevância social e por ser um exemplo realista de análise de dados no setor público. A distribuição de medicamentos é um tema crucial para a saúde pública e, ao mesmo tempo, fornece um contexto interessante para aplicar conceitos de engenharia de dados, como o tratamento e análise de grandes volumes de dados.

---

## Arquitetura do Pipeline de Dados

### Arquitetura Medalhão
A **Arquitetura Medalhão** organiza os dados em três camadas distintas:
- **Bronze**: Armazenamento de dados brutos, sem transformações.
- **Silver**: Dados limpos e transformados, mas ainda não prontos para análises finais.
- **Gold**: Dados analíticos, prontos para consultas e visualizações detalhadas.

### Aplicação da Arquitetura Medalhão
A arquitetura foi aplicada da seguinte forma:
- **Camada Bronze**: Dados extraídos diretamente do arquivo CSV e armazenados na tabela `bronze_table` do PostgreSQL.
- **Camada Silver**: Após a carga na camada Bronze, os dados passaram por transformações de limpeza e normalização, sendo armazenados no schema `silver`.
- **Camada Gold**: Consultas analíticas, como a distribuição de medicamentos por bairro e classe, foram realizadas e os resultados carregados no schema `gold`.

---

## Ambiente e Ferramentas Utilizadas
O ambiente de desenvolvimento foi configurado com ferramentas modernas para garantir eficiência, escalabilidade e reprodutibilidade:

- **Docker**: Utilizado para criar um ambiente isolado e replicável, com o PostgreSQL rodando dentro de um container. Isso garantiu um ambiente controlado e livre de configurações manuais complicadas.
- **PostgreSQL**: Sistema de gerenciamento de banco de dados relacional (SGBD) para armazenar dados nas camadas Bronze, Silver e Gold.
- **SQLAlchemy**: Biblioteca Python para facilitar a interação com o PostgreSQL de forma eficiente e flexível.
- **Bibliotecas Python**:
  - **Pandas**: Manipulação e transformação de dados.
  - **Requests**: Realização da requisição HTTP para baixar o arquivo CSV.
  - **IPython**: Exibição de DataFrames para visualização intermediária dos dados.
- **Jupyter Notebook**: Ambiente de desenvolvimento para codificação interativa, facilitando testes e ajustes rápidos.

---

## Processo de Extração e Transformação

### Extração dos Dados
A extração foi feita a partir de um arquivo CSV hospedado no portal de dados da Prefeitura. Utilizando a biblioteca **requests**, o arquivo foi baixado e carregado diretamente na camada **Bronze** do banco de dados PostgreSQL.

### Transformação dos Dados
Na camada **Silver**, diversas transformações foram aplicadas:
- **Limpeza de Caracteres Especiais**: Remoção de caracteres indesejados nas colunas de texto.
- **Substituição de Valores Nulos**: Substituição de valores nulos por valores apropriados para garantir a integridade dos dados.
- **Conversão de Tipos de Dados**: Colunas de texto, numéricas e datas foram convertidas para tipos adequados.
- **Normalização dos Nomes das Colunas**: Colunas renomeadas para garantir consistência.
- **Criação de ID (Chave Primária)**: Cada linha recebeu um identificador único.
- **Criação de Timestamps**: Colunas `DT_CREATED` e `DT_UPDATED` foram adicionadas para rastrear alterações no pipeline.

---

## Consultas

### Descrição das Consultas SQL
Duas consultas principais foram realizadas na camada **Silver** e os resultados carregados na camada **Gold**:
- **Consulta por Bairro**: Agrupamento por bairro, somando a quantidade de medicamentos distribuídos e o número de produtos distintos.
- **Consulta por Classe de Produto**: Agrupamento por classe de medicamento, mostrando a quantidade de produtos e o número de bairros atendidos.

### Justificativa para Escolha das Consultas
As consultas foram escolhidas com foco em gerar insights relevantes sobre a distribuição dos medicamentos, com potencial para análises mais profundas:
- A consulta por **bairro** revela áreas com maior demanda.
- A consulta por **classe de produto** destaca os tipos de medicamentos mais distribuídos.

Essas consultas são versáteis e podem servir como base para análises futuras, permitindo ao time de dados explorar diferentes perspectivas da distribuição de medicamentos.

---

## Conclusão
Este projeto proporcionou uma excelente oportunidade de aplicar conceitos de **engenharia de dados** em um contexto real. A utilização da **Arquitetura Medalhão** e o processo de **ETL** (extração, transformação e carregamento) organizaram os dados de maneira eficiente, com um pipeline robusto, escalável e pronto para análises detalhadas.

---

## Reflexões Finais
Enfrentei desafios técnicos durante o desenvolvimento, como a configuração do ambiente no Docker e o uso de ferramentas novas, mas esses obstáculos proporcionaram um aprendizado significativo. No futuro, eu implementaria a **automação do processo de atualização** dos dados, utilizando ferramentas de **orquestração de pipeline** como **Apache Airflow** ou **Prefect**. Isso garantiria que os dados estivessem sempre atualizados automaticamente, sem a necessidade de intervenção manual.

Esse aprimoramento não só melhoraria a eficiência do pipeline, mas também garantiria que ele fosse mais robusto e confiável a longo prazo.
