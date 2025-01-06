# Optimization-Graph
Optimization Graph Phyton
import pandas as pd
print(pd.__version__)
records = pd.read_csv('data/records_uker.csv')
records.head()
lokasi = pd.read_csv('data/lokasi_uker.csv')
lokasi.head()
records.info()
lokasi.info()
data = records[['start', 'end', 'biaya_perpindahan']]
data.head()
# Membuat objek graph
Graf = nx.Graph()
# Iterasi per baris dari dataframe
for ind in range(len(data)):
  # Mengakses nilai setiap baris menjadi list
    row = data.iloc[ind].tolist()
   # Memasukkan edges tiap node ke dalam graf
    Graf.add_edge(row[0], row[1], weight = row[2])
  # Visualisasi graf
graph.visualize_graph(Graf)
nx.single_source_dijkstra(Graf, source='E')
# source = A, target = F, cutoff = 2
graph.get_total(Graf, source='A', target='F', cutoff=2)
# Mendapatkan path optimal menggunakan tsp
path_tsp = nx.approximation.traveling_salesman_problem(G, cycle=False)
path_tsp
# Membuat dataframe hasil dari TSP
data = [['C', 'A', 'Uker'],
        ['A', 'B', 'Uker'],
        ['B', 'E', 'Uker'],
       ['E', 'D', 'Uker'],
       ['D', 'F', 'Uker']]

optimize_tsp = pd.DataFrame(data, columns = ['start', 'end', 'day'])
optimize_tsp
from helper import graph
merge_tsp = pd.merge(optimize_tsp, lokasi, left_on='start', right_on='kode')
final_tsp = pd.merge(merge_tsp, lokasi, left_on='end', right_on='kode', suffixes=('_start', '_end'))
final_tsp
# #Membuat objek peta
map_object = graph.create_map_object('Jakarta, Indonesia')
graph.visualize_route(map_object, final_tsp)
