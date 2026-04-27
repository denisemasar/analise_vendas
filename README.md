# analise_vendas
Projeto desenvolvido como exercício de análise de dados utilizando Python e técnicas de exploração de dados.
PROJETO ANÁLISE EXPLORATÓRIA DE DADOS
ALUNA: DENISE MARIA DE ASSIS ARAUJO Id: 1629014df = pd.read_csv("vendas_supermercado_com_cliente.csv")
CURSO: CAIXAVERSO - FC | Analista Dados - I 

OBJETIVO: O objetivo desse projeto será de analisar os dados de vendas de um supermercado gerando assim ideias que auxiliem nas decisões da empresa. 

Os dados incluem:
- Data da venda
- Produto
- Categoria
- Preço
- Quantidade
- Desconto
- Total da venda
- Idade do cliente
- Renda do cliente

ESTRUTURA SEQUENCIAL DO PROJETO:
    1 importar biblioteca
    2 ler dados
    3 explorar dados
    4 limpar dados
    5 criar variáveis novas
    6 responder perguntas
    7 interpretar resultado



1º PASSO: INSTALAR E OU IMPORTAR BIBLIOTECAS
    
    Neste passo vamos importar as bibliotecas necessárias para o projeto. 
    
        import nome_bbt as bbt. #importa a biblioteca
    
    Se elas não tiverem instaladas teremos que fazer sua instalação com o comando: 
        
        pip install nome_bbt 
    
    No caso desse trabalho vamos importar 4 bibliotecas pois cada uma delas terá uma função específica:

        - NumPy → cálculos numéricos.
        - pandas → manipulação de dados em tabelas.
        - matplotlib → gráficos básicos e flexíveis.
        - seaborn → gráficos estatísticos mais bonitos e fáceis.

2º PASSO: LER O ARQUIVO DE DADOS
    
    df = pd.read_csv("vendas_supermercado_com_cliente.csv")
    df é dataframe que é uma tabela aí pedimos para a biblioteca pandas fazè-lo. pandas.lê.tal_arquivo
    
    Na escrita das funções temos que saber diferenciar Parênteses, colchetes e chaves:
        - Parênteses servem para executar funções ou escrever parâmetros 
        - Colchetes servem para acessar dados.
        - Chaves servem para dicionários. É uma estrutura de chave → valor.

3º PASSO: EXPLORAR OS DADOS E TRATAR TIPOS INCORRETOS
    
    ETAPA A - VISÃO GERAL DO DATASET
        df.head()        # primeiras 5 linhas
        df.shape         # número de linhas e colunas
        df.info()        # tipos de dados e valores nulos

    ETAPA B - CORRIGINDO TIPOS
    
        .astype() #para tipos simples (int, float, str, category, bool).
        pd.to_datetime() #para datas.
        pd.to_numeric()  #para números com tratamento de erros.
        .set_index() / .reset_index() → para manipular índices.
    
  4º PASSO:VERIFICAÇÃO E TRATAMENTO DE VALORES AUSENTES
    
    df.isnull().sum()        # contagem de nulos por coluna
    df.dropna()              # remove linhas com nulos
    df.fillna(0)             # substitui nulos por 0
    df.fillna(df.mean())     # substitui nulos pela média

  5º PASSO- EXTRAÇÃO DE PARTES E CRIAÇÃO DE VARIAVES NOVAS
    
    df["Ano"] = df["Data"].dt.year
    df["Mes"] = df["Data"].dt.month
    df["Dia"] = df["Data"].dt.day
    df["Dia_Semana"] = df["Data"].dt.day_name()




