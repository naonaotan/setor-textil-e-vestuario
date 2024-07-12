# Setor têxtil e vestuário no Brasil. Apenas uma necessidade básica ou um movimentador da economia? 1º semestre 2024
A partir de dados abertos extraídos do CVM (Comissão de Valores Mobiliários) escolhemos um setor específico do mercado brasileiro e mostramos sua relevância e números.

### Proposta de desafio
Fomos propostos a seguinte ideia:

  "Imagine que sou um investidor e estou interessado em fazer novos investimentos em variados setores e escolhi vocês como consultores para me auxiliar na tomada decisão.
  Montar um pitch sobre o porquê do seu setor ser interessante para investir e também qual a melhor empresa do setor na opinião do grupo.
  Informações interessantes para investidores são:
- Lucro Líquido (3.11 da DRE)
- Patrimônio Líquido (2.03 do BPP)
- Receita Bruta (3.01 da DRE)
- Resultado Antes do Resultado Financeiro e dos Tributos (EBIT) (3.05 da DRE)
- Dentre outros
  
Vocês podem comparar esses valores entre setores (intersetorial) e dentro do mesmo setor (intrasetorial), trazer a evolução histórica deles, etc."
  
[Clique aqui para visualizar a apresentação no Canva](https://www.canva.com/design/DAGCsXNBK1g/64wqNAD9UKimqUOThV_UtA/edit?utm_content=DAGCsXNBK1g&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

### Extração dos dados
Inicialmente extraímos os dados manualmente da plataforma CVM. Sendo:
Apenas as bases consolidadas, de 2019 a 2023.

### Tratamento por Python no Google Colab
Como cada dataframe estava separado, fizemos uma união com join para concatenar.

### Filtrar pelo Setor
Retornarmos apenas as linhas referentes ao setor Têxtil e Vestuário e com ordem de exercício sendo último.

### Cálculo de índices
Calculamos os seguintes indicadores financeiros para todas as empresas do setor utilizando a DRE (Demonstração do Resultado) e o Balanço Patrimonial Ativo:
- ROE (Return on Equity)
- ROA (Return on Assets)
- Margem líquida

![Indices](https://raw.githubusercontent.com/naonaotan/Setor-textil-e-vestuario/main/%C3%ADndices.png)

Para facilitar o cálculo, inicialmente selecionamos colunas específicas - Nome da empresa (DENOM_CIA), Código da Conta (CD_CONTA) e Valor (VL_CONTA).

Então, criamos quatro novos DataFrames (df_ll, df_pl, df_ta, df_rc), cada um contendo apenas as varíaveis referentes aos cálculos sendo Código da Conta (CD_CONTA) 1 (Ativo Total), 3.11 (Lucro Líquido), 2.03 (Patrimônio Líquido) e 3.01 (Receita Líquida).

Mesclamos os dataframes novamente com merge.

Por fim, calculamos três indicadores (ROE, ROA, ML) dividindo os valores de Lucro Líquido (VL_CONTA_311) pelos valores das outras contas específicas (VL_CONTA_203, VL_CONTA_1, VL_CONTA_301),
e adicionamos esses indicadores como novas colunas.

### Retorno de outros valores
Como fomos solicitados uma análise financeira pela visão de um investidor, decidimos trazer além dos índices calculados, os valores de Lucro Líquido e trazer o EBIT também.
1. Filtragem dos valores necessários na coluna CD_CONTA
   Filtramos o DataFrame original df para selecionar apenas as linhas onde a coluna CD_CONTA contém os valores '3.11', '2.03', '3.01', '1' ou '3.05'.
   O resultado é salvo em um novo DataFrame chamado df_indicadores.
2. Selecionando apenas as colunas que serão utilizadas
   Criamos um novo DataFrame df_colunas que contém apenas as colunas DENOM_CIA, CD_CONTA, DT_FIM_EXERC e VL_CONTA do DataFrame df_indicadores.
3. Pivotando a tabela
   Transformamos (pivotando) o DataFrame df_colunas de forma que as combinações de DENOM_CIA e DT_FIM_EXERC se tornem as linhas (index),
   os valores de CD_CONTA se tornem as colunas (columns), e os valores de VL_CONTA preencham as células da tabela resultante (values).
   Em seguida, você usa reset_index() para transformar o índice gerado pela pivotagem em colunas normais, resultando em df_pivot.
4. Criando novas colunas baseadas em cálculos de colunas existentes
   Criamos três novas colunas no DataFrame e as renomeamos.
### Extração
Extraímos esse df como arquivo xlsx para desenvolvimento de visualização no Power Bi.

#### Para instalar e visualizar o arquivo `.pbix` no Power BI, siga os passos abaixo:

#### Pré-requisitos

1. **Power BI Desktop**: Certifique-se de ter o [Power BI Desktop](https://powerbi.microsoft.com/desktop/) instalado no seu computador.

#### Passos

1. **Baixe o Arquivo `.pbix`**:
   - Clique [aqui](https://github.com/naonaotan/Setor-textil-e-vestuario/raw/main/Apresentação%20dos%20gráficos.pbix) para baixar o arquivo `.pbix`.

2. **Abra o Power BI Desktop**:
   - Inicie o Power BI Desktop no seu computador.

3. **Abra o Arquivo `.pbix`**:
   - No Power BI Desktop, clique em `Arquivo` -> `Abrir`.
   - Navegue até o local onde você baixou o arquivo `.pbix`.
   - Selecione o arquivo `.pbix` e clique em `Abrir`.
