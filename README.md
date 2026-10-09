Language: Portuguese (Brazil)

\# Plano de Corte de MDF (liso) com Python

Algoritmo para otimização do posicionamento de peças retangulares de MDF em chapas padronizadas, com geração de um plano de corte em SVG para visualização e edição no CorelDraw ou programas semelhantes, através do Google Colab.

O projeto utiliza Python e a biblioteca `rectpack` para organizar as peças de acordo com suas dimensões, quantidades e espessuras, buscando reduzir o número de chapas necessárias. Surge da necessidade de automatizar esta atividade em uma aplicação real.

\## Funcionalidades

\* Leitura das dimensões das peças a partir de uma planilha Excel (lista medidas.xlsx).
\* Expansão automática das quantidades solicitadas em peças individuais.
\* Separação das peças por espessura.
\* Distribuição das peças em chapas de MDF de 1850 × 2750 mm.
\* Rotação das peças durante o encaixe, se necessário.
\* Consideração de espaçamento de 15 mm entre as peças.
\* Identificação de peças alocadas e não alocadas.
\* Cálculo do aproveitamento das chapas considerando as áreas reservadas, incluindo o espaçamento.
\* Exportação do plano de corte em SVG, com identificação das peças e suas dimensões, bem como das diferentes chapas.

\## Tecnologias utilizadas

\* \*\*Python\*\*
\* \*\*Pandas:\*\* leitura e manipulação dos dados da planilha.
\* \*\*Rectpack:\*\* algoritmo de encaixe bidimensional de retângulos.
\* \*\*HTML:\*\* escape de caracteres nos rótulos do SVG.
\* \*\*Google Colab:\*\* ambiente de execução do notebook.

\## Estrutura dos arquivos

| Arquivo                   | Descrição                                                                 |
| ------------------------- | ------------------------------------------------------------------------- |
| `plano\_corte\_retas.ipynb` | Notebook com o algoritmo de geração do plano de corte.                    |
| `lista\_medidas.xlsx`      | Planilha de entrada com as dimensões, quantidades e espessuras das peças. |

\## Formato da planilha

A planilha deve conter as seguintes colunas, com os nomes escritos exatamente como apresentados:

| Coluna        | Descrição                       | Unidade  |
| ------------- | ------------------------------- | -------- |
| `nome`        | Identificação da peça           | —        |
| `comprimento` | Comprimento da peça             | mm       |
| `largura`     | Largura da peça                 | mm       |
| `qtd`         | Quantidade de peças solicitadas | unidades |
| `espessura`   | Espessura do MDF                | mm       |

Cada linha representa um modelo de peça. A quantidade informada em `qtd` é expandida pelo algoritmo em peças individuais.

Exemplo:

| nome   | comprimento | largura | qtd | espessura |
| ------ | ----------: | ------: | --: | --------: |
| peca 1 |         200 |     800 |   2 |         6 |
| peca 2 |         400 |     600 |   4 |        15 |
| peca 3 |         600 |     100 |   3 |        18 |

Todas as dimensões lineares devem ser informadas em milímetros. As células das colunas obrigatórias não devem estar vazias.

\## Como executar

A execução é realizada exclusivamente pelo Google Colab, sem necessidade de instalar Python ou configurar um ambiente local.

\### 1. Abra o notebook no Google Colab

Acesse \[Google Colab](https://colab.research.google.com/).
No menu \*\*Arquivo\*\*, selecione \*\*Fazer upload de notebook\*\* e envie o arquivo `plano\_corte\_retas.ipynb`.

\### 2. Envie a planilha de entrada

No painel lateral do Colab, abra a seção \*\*Arquivos\*\* e envie o arquivo `lista\_medidas.xlsx`.

O notebook espera encontrar a planilha no caminho:
`/content/lista\_medidas.xlsx`

Se utilizar outro nome para o arquivo, será necessário alterar o caminho na célula responsável pela leitura da planilha.

\### 3. Execute o notebook

Execute as células em ordem, de cima para baixo, ou utilize a função 'Executar tudo'.

A primeira célula de código instala a biblioteca `rectpack`. As células seguintes realizam a leitura e validação dos dados, o encaixe das peças, o cálculo do aproveitamento e a geração do arquivo SVG.

\### 4. Baixe o plano de corte

Ao final da execução, será gerado o arquivo:
`plano\_corte.svg`

O arquivo pode ser baixado pelo painel \*\*Arquivos\*\* do Google Colab e aberto em um programa compatível com SVG, como o CorelDRAW.

\## Parâmetros do algoritmo

Os principais parâmetros estão definidos no notebook:

| Parâmetro        |      Valor | Descrição                        |
| ---------------- | ---------: | -------------------------------- |
| Largura da chapa |    1850 mm | Largura nominal da chapa de MDF. |
| Altura da chapa  |    2750 mm | Altura nominal da chapa de MDF.  |
| Espaçamento      |      15 mm | Espaço reservado entre peças.    |
| Rotação          | Habilitada | Permite girar as peças em 90°.   |

O algoritmo agrupa as peças por espessura, de modo que peças de espessuras diferentes sejam alocadas em chapas distintas.

\## Cálculo do aproveitamento

O aproveitamento é calculado pela razão entre a soma das áreas dos retângulos reservados às peças e a área total das chapas utilizadas.
As áreas reservadas incluem o acréscimo correspondente ao espaçamento de 15 mm nas duas dimensões de cada peça.
Esse indicador representa o aproveitamento geométrico do plano de corte considerando o espaço reservado. Não corresponde necessariamente ao rendimento real do material durante a fabricação.

\## Limitações

\* O algoritmo considera peças retangulares.
\* O encaixe é bidimensional e considera as dimensões externas das peças.
\* A rotação é permitida em incrementos de 90°.
\* O espaçamento configurado é de 15 mm.
\* O cálculo não considera automaticamente a largura efetiva do corte da serra (\*kerf\*), defeitos do material ou restrições específicas de máquinas.
\* O resultado depende das dimensões e quantidades informadas na planilha.
\* O SVG é uma representação geométrica do plano calculado e deve ser conferido antes de sua utilização na produção.

\## Objetivo

O projeto busca automatizar uma etapa do planejamento de corte de MDF, reduzindo o trabalho manual de distribuição das peças e facilitando a visualização do aproveitamento das chapas.
