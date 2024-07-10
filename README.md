# Setor textil e vestuário no Brasil. Apenas uma necessidade básica ou um potencial setor? 
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

