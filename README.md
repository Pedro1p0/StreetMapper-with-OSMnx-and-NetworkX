# Análise de Mobilidade em Parnamirim, RN

## Introdução

Bem-vindo ao projeto de Análise de Mobilidade em Parnamirim, Rio Grande do Norte. Em um esforço para compreender melhor os desafios de mobilidade em uma das maiores e mais promissoras cidades do estado, decidimos explorar e analisar a infraestrutura viária e a conectividade urbana de Parnamirim. O crescimento econômico e populacional acelerado da cidade destaca a importância de abordar questões relacionadas à mobilidade de maneira eficaz.

## Objetivo

Este projeto utiliza as bibliotecas NetworkX e OSMnx para realizar uma análise abrangente da rede de ruas de Parnamirim. Buscamos identificar e compreender os desafios de mobilidade enfrentados pela cidade, avaliando a eficiência da infraestrutura viária, áreas de congestionamento e propondo soluções para melhorar a mobilidade urbana.

## Metodologia

1. **Coleta de Dados**: Utilizando a biblioteca OSMnx, extraímos dados detalhados da rede de ruas de Parnamirim a partir do OpenStreetMap.

2. **Visualização do Grafo Urbano**: Usando NetworkX e OSMnx, geramos um gráfico representativo da rede de ruas da cidade, proporcionando uma visão visual clara da infraestrutura viária.

3. **Análise de Métricas de Centralidade**: Calculamos métricas de centralidade, incluindo centralidade de grau e proximidade, para identificar áreas críticas e nós importantes na rede urbana.

4. **Identificação de Problemas de Mobilidade**: Com base na análise do grafo, identificamos áreas de congestionamento, falta de conectividade e outros desafios de mobilidade.

5. **Proposta de Soluções**: Desenvolvemos soluções potenciais para os problemas identificados, visando melhorar a eficiência da mobilidade em Parnamirim.

# Coleta de Dados

Este projeto envolve a coleta de dados geoespaciais e a criação de mapas para análise da cidade de Parnamirim, RN. A seguir, são descritas as etapas de extração do mapa inicial, do mapa de calor baseado em nós e do mapa de calor baseado nas arestas.

## 1. Extração do Mapa Inicial

### Descrição:
A biblioteca `osmnx` é utilizada para extrair o mapa inicial da cidade de Parnamirim, RN, a partir do OpenStreetMap (OSM). Essa biblioteca facilita a obtenção de dados de redes urbanas e permite a manipulação eficiente desses dados para análise posterior.

### Código:

```python
import osmnx as ox

# Definir o local (place_name) como Parnamirim, RN, e o tipo de rede como viária (network_type='drive')
place_name = "Parnamirim, RN"
G = ox.graph_from_place(place_name, network_type='drive')
```
![Mapa](https://github.com/Pedro1p0/StreetMapper-with-OSMnx-and-NetworkX/blob/2a76b922acd33869e3790c3557e28dc5427dd2cb/graph_original_Parnamirim.png)

## 2. Extração do Mapa de Calor Baseado em Nós

### Descrição:
Nesta etapa, criamos um mapa de calor baseado na centralidade dos nós da rede viária de Parnamirim. A centralidade de um nó indica sua importância na rede e pode ser calculada de várias maneiras, como centralidade de grau, proximidade, entre outras.

### Código:

```python
import networkx as nx
import matplotlib.pyplot as plt

# Calcular a centralidade de grau para cada nó
node_centrality = nx.degree_centrality(G)

# Criar um mapa de calor baseado na centralidade dos nós
plt.figure(figsize=(10, 10))
ox.plot_graph(G, bgcolor='k', node_size=[v * 1000 for v in node_centrality.values()], node_color='r', node_edgecolor='none', node_zorder=2)
plt.title("Mapa de Calor Baseado em Nós - Centralidade de Grau")
plt.show()
```
![Mapa](https://github.com/Pedro1p0/StreetMapper-with-OSMnx-and-NetworkX/blob/98dd1d7b89faf8fda44259ab08670537cebaf28e/graph_edges_Parnamirim.png)
## 3. Extração do Mapa de Calor Baseado nas Arestas

### Descrição:
Nesta etapa, geramos um mapa de calor baseado na centralidade das arestas do grafo. A centralidade das arestas pode ser calculada considerando a centralidade de proximidade ou outras métricas relevantes.

### Código:

```python
# Calcular a centralidade de proximidade para cada aresta
edge_centrality = nx.closeness_centrality(nx.line_graph(G))

# Criar um mapa de calor baseado na centralidade das arestas
plt.figure(figsize=(10, 10))
ox.plot_graph(G, bgcolor='k', node_size=0, edge_color=edge_centrality.values(), edge_cmap=plt.cm.inferno, edge_linewidth=2, edge_alpha=0.7)
plt.title("Mapa de Calor Baseado em Arestas - Centralidade de Proximidade")
plt.show()
```
![Mapa](https://github.com/Pedro1p0/StreetMapper-with-OSMnx-and-NetworkX/blob/2a76b922acd33869e3790c3557e28dc5427dd2cb/graph_nodes_Parnamirim.png)

Essas etapas representam a coleta inicial de dados e a geração de mapas que serão utilizados para análises mais aprofundadas no projeto. As visualizações fornecem insights sobre a importância relativa de nós e arestas na rede viária de Parnamirim.

# Problemática

A cidade de Parnamirim, localizada no estado do Rio Grande do Norte, enfrenta desafios significativos relacionados à mobilidade urbana, agravados por sua posição estratégica em relação à capital, Natal. A problemática envolve diversos fatores que impactam diretamente a fluidez do tráfego e a qualidade de vida dos cidadãos.

## Crescimento Constante e Conexão com Natal

Parnamirim experimenta um crescimento populacional e econômico contínuo. Sua proximidade com Natal resulta em uma complexa rede viária interligando as duas cidades por meio de várias avenidas ao longo da fronteira. Essa conexão intensa cria desafios adicionais para a mobilidade urbana, uma vez que as duas prefeituras precisam colaborar e coordenar esforços para resolver os problemas de tráfego e infraestrutura em conjunto.

## Base Aérea de Natal como Desafio Adicional

Outro ponto crítico é a presença da Base Aérea de Natal, localizada no coração de Parnamirim, ocupando uma extensa área em meio à cidade. Essa situação apresenta um desafio substancial para a mobilidade urbana, pois a cidade cresceu em torno da base militar. A necessidade de conciliar o fluxo diário de tráfego com as operações da base militar demanda uma abordagem cuidadosa e colaborativa entre as autoridades locais e militares. Além disso a base se encontra em meio a cidade, o que dificulta a construção de uma estrada entre regiões importantes que são divisadas pela base.

## Integração Necessária entre Prefeituras

Os resultados e análises deste projeto podem servir como base para discussões e tomadas de decisão relacionadas à mobilidade urbana em Parnamirim. Contribuições, sugestões e melhorias são bem-vindas por meio de issues ou pull requests.

## Licença

Este projeto é distribuído sob a licença [MIT](LICENSE). Sinta-se à vontade para usar e adaptar conforme necessário.

Explore, analise e contribua para melhorar a mobilidade em Parnamirim! 🚗🗺️
