#PROJETO ANÁLISE EXPLORATÓRIA DE DADOS
## Informações do Projeto

**Aluna:** Denise Maria de Assis Araujo  
**ID:** 1629014  
**Curso:** CAIXAVERSO – FC | Analista de Dados I 

## Objetivo

O objetivo deste projeto é realizar uma **análise exploratória de dados (EDA)** utilizando um conjunto de dados de vendas de um supermercado.

A análise busca identificar padrões de consumo, comportamento de vendas e possíveis insights que possam auxiliar na **tomada de decisões estratégicas da empresa**.
## Tecnologias Utilizadas

- Python
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook / VS Code
- Git e GitHub

## Estrutura do Projeto

O projeto foi desenvolvido seguindo as seguintes etapas:

1. Importação de bibliotecas
2. Leitura do arquivo de dados
3. Exploração inicial dos dados
4. Tratamento de tipos de dados
5. Tratamento de valores ausentes
6. Criação de novas variáveis
7. Análise dos dados utilizando filtros e agrupamentos
8. Criação de gráficos
9. Interpretação dos resultados
10. Publicação do projeto no GitHub


1º PASSO: IMPORTAR BIBLIOTECAS
           

        
    - Neste passo vamos importar as bibliotecas necessárias para o projeto. 
        import nome_bbt as bbt. #importa a biblioteca
        
    - No caso desse trabalho vamos importar 4 bibliotecas pois cada uma delas terá uma função específica:

        - NumPy → cálculos numéricos.
        - pandas → manipulação de dados em tabelas.
        - matplotlib → gráficos básicos e flexíveis.
        - seaborn → gráficos estatísticos mais bonitos e fáceis.

2º PASSO: LER O ARQUIVO DE DADOS
    
    df = pd.read_csv("vendas_supermercado_com_cliente.csv")
    O objeto **df** representa um **DataFrame**, que é uma estrutura de dados do pandas semelhante a uma tabela, composta por linhas e colunas.    
    
    Na escrita das funções em Python é importante entender alguns símbolos:

    - **Parênteses ()** → usados para executar funções ou definir parâmetros.
    - **Colchetes []** → usados para acessar colunas ou elementos de dados.
    - **Chaves {}** → usadas para criar dicionários (estrutura chave → valor).

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

7º PASSO - CRIAÇÃO DE GRÁFICOS E INTERPRETAÇÃO DE RESULTADOS
    
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

    ETAPA E - RESULTADOS

        A análise exploratória permitiu identificar padrões importantes nas vendas do supermercado, como:

        - categorias com maior volume de vendas
        - impacto de promoções no comportamento de compra
        - variações de vendas ao longo do tempo
        - produtos com maior desempenho
        

8º passo - ENVIO NO GITHUB
    ETAPA A - CRIAR UM DEPOSITÓRIO NO GITHUB
        
        No site do Github crie um novo repositório de acordo com suas preferências e necessidades. 
    
    ETAPA B - ABRIR O PROJETO NO VSCODE
        
        Abra a pasta do seu projeto no VSCODE e abra um novo terminal. 

    ETAPA C - ENVIO DE COMANDOS NO TERMINAL
        
        git init                                                        #transforma sua pasta em um repositório Git.
        git add .                                                       #O ponto significa todos os arquivos da pasta.
        git commit -m "primeiro envio do projeto"                       #Commit - salva a versão do projeto. 
        git remote add origin https://github.com/seunome/projeto.git    #Conecta ao git pelo link do repositório
        git branch -M main                                              #Renomeia a branch para main
        git push -u origin main                                         #Envia e conecta

    ETAPA D - ATUALIZAÇÃO DO PROJETO NO GITHUB
        
        git status                                          #verifica as mudanças
        git add .                                           #adiciona os arquivos modificados
        git commit -m "atualização da análise"              #cria um novo commit 
        git push                                            #envia para o Github    
        git pull origin main                                #em caso de erro, ele baixa as atualizações do git e faz um merge com o local.  


