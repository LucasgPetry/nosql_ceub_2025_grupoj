README – Projeto SIPACC (Sistema Integrado de Processamento e Análise de Crimes Cibernéticos)
1. Introdução

Este projeto apresenta o desenvolvimento de um ambiente completo para simulação, armazenamento, processamento e análise de dados relacionados a crimes cibernéticos. A solução foi construída utilizando o banco NoSQL MongoDB, com foco na modelagem de coleções inter-relacionadas, geração sintética de dados estruturados e criação de visualizações analíticas a partir de DataFrames derivados dessas coleções.

O objetivo central é demonstrar, de forma prática, como bancos NoSQL podem ser utilizados para apoiar investigações, análises estatísticas e monitoramento de incidentes por meio de pipelines de dados, validação via JSON Schema e desenvolvimento de dashboards interativos.

2. Estrutura do Banco de Dados

O banco de dados foi modelado com base em um conjunto de coleções que representam diferentes entidades do ecossistema de investigação e processamento judicial. As principais coleções são:

* instituicoes_investigativas

* instituicoes_judiciais

* agentes

* autoridades_judiciais

* denuncias

* ocorrencias

* perfis_digitais

* documentos_processuais

Cada coleção possui seu próprio JSON Schema, definindo:

* tipos e formatos de dados

* campos obrigatórios

* restrições de valores (enumerações)

* estrutura de subdocumentos

* listas de referências

* consistência dos relacionamentos

Essa modelagem garante integridade estrutural e validação automática durante a inserção dos documentos.

3. Geração Sintética dos Dados

Para povoamento do banco, foi desenvolvido um módulo Python que gera dados sintéticos realistas. O processo inclui:

3.1 Funções utilitárias

* Criação de ObjectId no formato Extended JSON

* Geração de datas aleatórias em formato ISO

* Produção de nomes, CPFs, telefones, registros funcionais e endereços MAC

3.2 Base de valores

Listas contendo cidades, tipos de crime, perfis de conta, cargos, plataformas, status e outros atributos necessários.

3.3 Funções de geração por coleção

Cada coleção possui uma função específica para a criação de documentos em conformidade com seu JSON Schema

A coleção "ocorrencias" apresenta o caso mais complexo, contendo:

* listas de vítimas

* listas de evidências

* dispositivos apreendidos

* referência para denúncias, agentes, perfis digitais, instituições e processos

4. Inserção dos Dados no MongoDB Atlas

Os arquivos JSON gerados foram inseridos no MongoDB através de um pipeline que realiza:

* Leitura dos arquivos

* Inserção com insert_many()

O processo foi automatizado para rodada em lote, garantindo eficiência e prevenção de erros de duplicação, formato ou estrutura.

5. Normalização dos DataFrames

Após a inserção, cada coleção foi convertida em um DataFrame Pandas. Como as estruturas do MongoDB incluem listas, subdocumentos e ObjectIds, foi implementado um normalizador capaz de:

* Converter ObjectIds para strings

* Converter datas ISO para objetos datetime

* Explodir listas de referências

* Tratar listas de subdocumentos (vítimas, evidências, dispositivos)

* Uniformizar colunas para permitir análises estatísticas e visuais

6. Construção das Visualizações Analíticas

Com os DataFrames tratados, foi possível realizar análises quantitativas e exploratórias. Entre as visualizações desenvolvidas estão:

* Série histórica de ocorrências por ano

* Geolocalização aproximada das cidades com maior volume de ocorrências

* Distribuição etária das vítimas

* Heatmap cruzando tipo de crime e plataforma utilizada

* Identificação dos crimes mais recorrentes

Essas visualizações fornecem direcionamentos sobre padrões comportamentais, tendências temporais e características relevantes dos incidentes.

7. Dashboard Interativo com Streamlit

Foi desenvolvido um painel interativo com Streamlit 

8. Tecnologias Utilizadas

* Python 3.11

* MongoDB Atlas

* PyMongo

* Pandas

* Streamlit

* Plotly, Matplotlib e Seaborn

* Pydeck

* JSON Schema

* BSON / json_util

10. Estrutura do diretório

Os arquivos em PDF são respectivos aos requisitos e ao projeto, a pasta mongodump é o dump do database completo com suas collections e metadata. Por fim, a outra pasta zipada contém o script python gerador dos json, eles próprios, o script que constrói o dashboard em streamlit e um notebook ipynb contendo exemplos de operações CRUD com o cluster conectado. 

11. Conclusão

O projeto demonstra, de maneira integrada, como bancos NoSQL podem ser aplicados para a modelagem, simulação e análise de dados complexos. Desde a validação de documentos via JSON Schema, passando pela geração sintética estruturada, normalização analítica com Pandas e construção de dashboards com Streamlit, o trabalho evidencia o potencial de soluções NoSQL para cenários que envolvem relacionamentos flexíveis, grandes volumes de dados e análises exploratórias ricas.

