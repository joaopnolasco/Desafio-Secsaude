# Projeto: Pipeline de Dados - Secretaria de Saúde do Recife

**Desenvolvedor do projeto**: João Paulo Oliveira Nolasco  
**Data de entrega**: 31/01/2025  

---

## Índice

1. [Credenciais do Banco de Dados](#credenciais-do-banco-de-dados)
2. [Resumo do Projeto](#resumo-do-projeto)
3. [Descrição do Dataset](#descrição-do-dataset)
4. [Arquitetura do Pipeline](#arquitetura-do-pipeline)
5. [Ferramentas Utilizadas](#ferramentas-utilizadas)
6. [Consultas SQL](#consultas-sql)
7. [Organização do Repositório](#organização-do-repositório)
8. [Conclusão](#conclusão)

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

Este projeto consiste na construção de um pipeline de dados utilizando Python e SQL. Mais especificamente, conforme foi solicitado:

Foi Construído um pipeline para extrair, elaborar duas consultas sobre esses dados, usando SQL, e por fim um breve relatório sobre o projeto.

Este read.me foca da descrição resumida do projeto e principalmente na organização do repositório, e informações essenciais para a execução. Para conferir detalhadamente os detalhes do código, projeto e insights, confira o relatório juntamente com os scripts disponibilizados na pasta.

---

## Descrição do Dataset

O **dataset** utilizado contém informações detalhadas sobre a distribuição de medicamentos realizados pela **Secretaria de Saúde do Recife**. Ele foi coletado de uma plataforma pública da prefeitura e abrange dados como:

- Nome do produto
- Quantidade distribuída
- Classe do produto
- Bairro de distribuição

A escolha desse conjunto de dados se deu pela relevância e impacto direto na saúde pública, fornecendo uma visão da distribuição de medicamentos essenciais para a população de Recife. Esse tipo de dado pode ser analisado para ajudar a entender as áreas com maior demanda de medicamentos, identificar padrões e, consequentemente, melhorar a logística e a alocação de recursos. Além disso, acheu extremamente pertinente um dataset na área da saúde pois já "simularia" uma tarefa de engenheiro de dados na Secretária de Saúde do Recife.

---

## Arquitetura do Pipeline

A arquitetura do pipeline segue o modelo **Medalhão**, que organiza os dados em três camadas:

![image](https://github.com/user-attachments/assets/035da02e-58ab-4921-b553-f8a395702a0b)

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

Este projeto proporcionou uma excelente oportunidade de aplicar conceitos fundamentais de **engenharia de dados** em um contexto real, utilizando dados sobre a distribuição de medicamentos pela **Prefeitura do Recife**. A arquitetura **Medalhão** foi adotada para estruturar o pipeline em três camadas distintas: **Bronze**, **Silver** e **Gold**, organizando os dados de forma eficiente. A camada **Bronze** armazenou os dados brutos, a **Silver** continha os dados tratados e a **Gold** foi a camada final para consultas analíticas. Esse processo de organização permitiu uma estrutura robusta e escalável, ideal para análise de dados.

As transformações realizadas nos dados, como a **limpeza de valores nulos**, **normalização de colunas** e **ajustes de tipos de dados**, foram essenciais para garantir que os dados estivessem prontos para análises mais detalhadas. O uso do **Docker** para rodar o banco de dados PostgreSQL foi uma experiência valiosa, permitindo a criação de um ambiente isolado e facilmente replicável, embora tenha exigido esforços adicionais na configuração inicial.

### Pontos de Melhoria

Uma melhoria importante que eu gostaria de implementar, caso tivesse mais tempo, seria a **automação do processo de atualização dos dados**. Isso garantiria que o pipeline estivesse sempre atualizado com as informações mais recentes, sem a necessidade de intervenção manual. Para isso, ferramentas de **orquestração de pipelines**, como **Apache Airflow** ou **Prefect**, poderiam ser utilizadas para agendar, monitorar e gerenciar a execução dos processos ETL de maneira mais eficiente. A automação garantiria que as atualizações de dados ocorressem automaticamente, conforme o arquivo original fosse atualizado no portal da Prefeitura, tornando o pipeline mais robusto e menos dependente de ações manuais.

Além disso, a **orquestração** do pipeline poderia coordenar todas as etapas do processo (extração, transformação e carregamento), proporcionando uma solução mais escalável e eficiente, com maior confiabilidade e menos necessidade de supervisão constante. Com essas melhorias, o pipeline seria mais autossuficiente e poderia ser utilizado em produção de forma mais eficiente e confiável.
