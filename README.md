PROJETO ANÁLISE EXPLORATÓRIA DE DADOS
ALUNA: DENISE MARIA DE ASSIS ARAUJO Id: 1629014
CURSO: CAIXAVERSO - FC | Analista Dados - I 

OBJETIVO: O objetivo desse projeto será de analisar os dados de vendas de um supermercado gerando assim ideias que auxiliem nas decisões da empresa. 

ESTRUTURA SEQUENCIAL DO PROJETO:
    
    1 INSTALAR E OU IMPORTAR BIBLIOTECAS
    2 LEITURA DO ARQUIVO DE DADOS
    3 EXPLORAR OS DADOS E TRATAR OS TIPOS INCORRETOS
    4 VERIFICAÇÃO E TRATAMENTO DE DADOS AUSENTES
    5 EXTRAÇÃO DE PARTES E CRIAÇÃO DE VARIÁVEIS NOVAS
    6 RESPONDENDO AS PERGUNTAS COM FERRAMENTAS COMO SELEÇÃO FILTROS E AGRUPAMENTO DE DADOS
    7 CRIAÇÃO DE GRÁFICOS E INTERPRETAÇÃO DE RESULTADOS

1º PASSO: INSTALAR E OU IMPORTAR BIBLIOTECAS
    
       
    ETAPA A - INSTALAÇÃO DE BIBLIOTECAS
        Se elas não tiverem instaladas teremos que fazer sua instalação com o comando: 
        
            pip install nome_bbt 
    
    ETAPA B - IMPORTAÇÃO DE BIBLIOTECAS
        
        - Neste passo vamos importar as bibliotecas necessárias para o projeto. 
            import nome_bbt as bbt. #importa a biblioteca
        
        - No caso desse trabalho vamos importar 4 bibliotecas pois cada uma delas terá uma função específica:

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

6º PASSO - RESPONDENDO AS PERGUNTAS COM FERRAMENTAS COMO SELEÇÃO FILTROS E AGRUPAMENTO DE DADOS

    ETAPA A - AGRUPAR DADOS POR CATEGORIA

        df.groupby("Categoria")

    ETAPA B - OPERAR COM ESSES DADOS AGRUPADOS

        df.groupby("coluna")["coluna_calculo"].operacao()

        Com o uso dos colchetes, acessamos os dados e os operamos. 

            df.groupby("Categoria")["Total_Venda"].sum()                                #SOMA
            df["Total_Venda"].mean()                                                    #MEDIA
            df.groupby("Categoria")["Produto"].count()                                  #CONTAGEM
            df.groupby("Categoria")["Total_Venda"].max()                                #MAIOR VALOR
            df.groupby("Categoria")["Total_Venda"].min()                                #MENOR VALOR
            df.groupby("Categoria")["Total_Venda"].agg(["sum","mean","max"])            #VÁRIAS METRICAS DE UMA VEZ
            df.groupby(["Mes","Categoria"])["Total_Venda"].sum()                        #AGRUPAR MAIS DE UMA COLUNA
            df.groupby("Categoria")["Total_Venda"].sum().sort_values(ascending=False)   #ORDENAR RESULTADOS
            df.groupby("Categoria")["Total_Venda"].sum().reset_index()                  #TRANSF. RESULTADO EM TAB NOV.
            
    ETAPA C - CRIAÇÃO DE NOVAS VARIÁVEIS DERIVADAS DE OPERAÇÕES COM DADOS AGRUPADOS
       Após realizar o agrupamento e as operações de agregação nos dados, foram criadas novas variáveis para armazenar os resultados dessas análises.Essas variáveis representam novas tabelas (dataframes) derivadas dos dados originais e facilitam a análise de padrões. 

        vendas_categoria_mes = (df.groupby(["Categoria","Mes"])["Quantidade"].sum().reset_index())
        pico_vendas = vendas_categoria_mes.loc[vendas_categoria_mes.groupby("Categoria")["Quantidade"].idxmax()]

    7º PASSO - CRIAÇÃO DE GRÁFICOS E INTERPERETAÇÃO DE RESULTADOS
        Após realizar os cálculos e análises, utilizamos gráficos para facilitar a interpretação dos resultados.
        A visualização ajuda a identificar padrões, comparações entre categorias e tendências ao longo do tempo.
        Neste projeto foram utilizadas principalmente as bibliotecas pandas, matplotlib e seaborn para criação dos gráficos.

        ETAPA A – PADRÃO DE CRIAÇÃO DE GRÁFICOS COM PANDAS

            O pandas possui um método próprio para gerar gráficos diretamente a partir de um DataFrame ou Series.
            
            variavel.plot(kind="barh", figsize=(10, 6), colormap="viridis")         #tipo, tamanho, cor
            plt.title("Titulo do gráfico")

        ETAPA B – PADRÃO DE PERSONALIZAÇÃO COM MATPLOTLIB

            A biblioteca matplotlib é utilizada para personalizar os gráficos, adicionando títulos, nomes dos eixos e ajustes visuais.
                
                plt.title() → define o título do gráfico.
                plt.xlabel() → define o nome do eixo horizontal.
                plt.ylabel() → define o nome do eixo vertical.
                plt.show() → exibe o gráfico.

        ETAPA C – PADRÃO DE CRIAÇÃO DE GRÁFICOS COM SEABORN

            O seaborn é utilizado para criar gráficos estatísticos mais elaborados, utilizando diretamente os dados do dataframe.
            
            sns.tipo_grafico(data=dataset, x=variavel, y=variavel, hue=Categoria)
                
                data → dataset utilizado no gráfico
                x → variável do eixo horizontal
                y → variável do eixo vertical
                hue → separa os dados por categoria usando cores diferentes

        ETAPA D – INTERPRETAÇÃO DOS RESULTADOS
        
            Após a criação de novos dados, tabelas e gráficos, realizamos sua interpretação para compreender os padrões identificados na análise.
            Essa etapa consiste em analisar os resultados obtidos nas operações e visualizações, buscando extrair informações relevantes sobre o comportamento das vendas.  