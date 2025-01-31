# Desafio Pipeline de Dados - Secretaria de Saúde do Recife
 
**Desenvolvedor do projeto**: João Paulo Oliveira Nolasco  
**Data de entrega**: 31/01/2025  

---

## Índice

1. [Credenciais do Banco de Dados](#credenciais-do-banco-de-dados)
2. [Resumo do Projeto](#resumo-do-projeto)
3. [Arquitetura do Pipeline](#arquitetura-do-pipeline)
4. [Ferramentas Utilizadas](#ferramentas-utilizadas)
5. [Consultas SQL](#consultas-sql)
6. [Organização do Repositório](#organização-do-repositório)
7. [Conclusão](#conclusão)

---

## Credenciais do Banco de Dados

O banco de dados foi configurado utilizando o PostgreSQL dentro de um container Docker. Para se conectar ao banco, use as seguintes credenciais:

- **Container**: meu_postgres  
- **Username**: joaonolasco  
- **Senha**: 32313167  
- **Host**: localhost  
- **Porta**: 5432  
- **Database**: meu_banco  

---

## Resumo do Projeto

Este projeto consiste na construção de um **pipeline de dados** para processamento e análise de informações sobre medicamentos distribuídos pela **Secretaria de Saúde do Recife**. O pipeline organiza os dados em três camadas de processamento, utilizando a **Arquitetura Medalhão**.

---

## Arquitetura do Pipeline

A arquitetura do pipeline segue o modelo **Medalhão**, que organiza os dados em três camadas:

1. **Camada Bronze**: Armazena os dados brutos extraídos de fontes externas, sem nenhuma alteração.
2. **Camada Silver**: Contém toda a parte de limpeza, tratamento e transformação dos dados.
3. **Camada Gold**: Armazena os dados finais com análises e consultas que geram informação.

---

## Ferramentas Utilizadas

- **Docker**: Para containerizar o banco PostgreSQL.
- **PostgreSQL**: Sistema de gerenciamento de banco de dados para armazenar e manipular os dados.
- **Python**: Linguagem utilizada para o processo de extração, transformação e carregamento (ETL).
  - Bibliotecas: Pandas, SQLAlchemy, Requests.
- **Jupyter Notebook**: Ambiente interativo para desenvolvimento do pipeline.

---
## Consultas SQL

Duas consultas principais foram realizadas, e os resultados foram carregados na camada **Gold**:

1. **Consulta por Bairro**: Agrupa os dados por bairro, somando a quantidade de medicamentos distribuídos e contando o número de produtos distintos por bairro.
2. **Consulta por Classe de Produto**: Agrupa os dados por classe de produto, mostrando o número de produtos disponíveis e o número de bairros atendidos por cada classe.

### Justificativa para Escolha das Consultas

As consultas foram escolhidas para fornecer um recorte interessante e pertinente para um posterior trabalho de analistas/cientistas de dados. A ideia aqui foi realmente deixar uma consulta bem aberta e com possibilidades de análises sobre elas, e não já fazer a query com a análise minuciosa já feita. As queries trazem recortes sobre a distribuição geográfica dos medicamentos e a diversidade de classes de produtos. A consulta por bairro permite identificar áreas com maior demanda de medicamentos, enquanto a consulta por classe ajuda a entender quais tipos de medicamentos são mais distribuídos. Essas consultas oferecem uma visão clara e detalhada do panorama da distribuição de medicamentos na cidade.


---

## Organização do Repositório

A estrutura do repositório é organizada da seguinte forma:

- **`/scripts`**: Contém os arquivos Python (Jupyter Notebooks) responsáveis pela extração, transformação e carregamento dos dados nas camadas **Bronze**, **Silver** e **Gold**.
    - **Camada Bronze**: Arquivo que carrega os dados brutos para o banco.
    - **Camada Silver**: Arquivo responsável pelas transformações e limpeza dos dados.
    - **Camada Gold**: Arquivo que realiza as consultas analíticas e armazena os resultados finais.
- **`/relatorio`**: Contém o relatório em PDF detalhado sobre o projeto, com a descrição do processo de ETL, análise e discussões sobre as escolhas feitas durante o desenvolvimento.
- **`/scripts/requirements.txt`**: Arquivo que lista todas as dependências necessárias para rodar o projeto (bibliotecas Python como Pandas, SQLAlchemy, Requests, etc.).

---

## Conclusão

Este projeto demonstrou a construção de um pipeline de dados eficiente e escalável, utilizando a arquitetura Medalhão para organizar e processar os dados. Ele pode ser expandido para incluir novas consultas analíticas e, com mais tempo, melhorias como a automação da atualização dos dados e a orquestração do pipeline de ETL.

Para mais detalhes sobre o projeto, consulte o código e o relatório completo no repositório.

