# Análise de Acidentes em Porto Alegre
##Descrição
Este projeto realiza uma análise de dados sobre acidentes na cidade de Porto Alegre, utilizando um conjunto de dados contendo informações sobre a localização e a data dos acidentes. O objetivo é visualizar a distribuição dos acidentes através de mapas de calor e gráficos, permitindo uma melhor compreensão dos padrões e tendências.

#Tecnologias Utilizadas
Python
Pandas
Folium
Matplotlib

#Dataset
O dataset utilizado é composto por registros de acidentes na cidade de Porto Alegre, incluindo informações sobre latitude, longitude e data. O arquivo pode ser encontrado em cat_acidentes.csv.

#Como Utilizar
Importar as Bibliotecas
As bibliotecas necessárias são importadas no início do script:

import pandas as pd
import folium
from folium.plugins import HeatMap, MarkerCluster
import matplotlib.pyplot as plt

# Carregar os Dados
##Os dados são carregados utilizando o Pandas:

df = pd.read_csv(r"C:\Users\Pradolux\Downloads\Acidentes POA\cat_acidentes.csv", sep=";")

#Limpar os Dados
Remova linhas com valores nulos nas colunas de latitude e longitude:

df = df.dropna(subset=['latitude', 'longitude'], how='any')

#Criar um Mapa de Calor
##Um mapa de calor é gerado para visualizar a concentração de acidentes:

mapa = folium.Map(location=[-30.1, -51.15], zoom_start=11)
coordenadas = list(zip(df.latitude, df.longitude))
mapa_calor = HeatMap(coordenadas, radius=9, blur=10)
mapa.add_child(mapa_calor)
mapa


#Visualizar Acidentes por Ano
##Os dados de acidentes são convertidos em um formato de data e a quantidade de acidentes por ano é plotada em um gráfico:

df['data'] = pd.to_datetime(df['data'], errors='coerce')
df_ano = df['data'].dt.year.value_counts().drop(2202)
plt.bar(df_ano.index, df_ano.sort_values(ascending=True))
plt.show()

#Gradiente de Cores
##Um gráfico é gerado com um gradiente de cores, representando a proporção de acidentes:

gradiente = df_ano / df_ano.max()
cores = plt.cm.Blues(gradiente)
plt.bar(df_ano.index, df_ano.sort_values(ascending=True), color=cores)
plt.show()

#Resultados
Os gráficos e mapas gerados ajudam a visualizar a distribuição dos acidentes em Porto Alegre, identificando áreas com maior frequência de incidentes e permitindo uma análise mais aprofundada das tendências ao longo dos anos.
