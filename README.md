# LSTM_Dataset
#### Dataset_OBT
```
1. Time --> string
2. OBT (on-board Time) --> float64
3. RTT_Bangalore_CARTOSAT2C <==> RTT_srcnode_dstnode --> float64
``` 

#### Calculate Predecessor using Dataset_OBT
```
from scipy.sparse.csgraph import dijkstra
from scipy.sparse import csr_matrix

def get_predecessors(rtt_values):
    graph = csr_matrix(rtt_values.astype(np.float64))  # Ensure data is float64
    _, predecessors = dijkstra(rtt_values, return_predecessors=True, directed=False)
    return predecessors

predecessors_list = []

# Iterating over rows, converting each row to numpy array, and ensuring float64 dtype
for _, row in data.iterrows():
    rtt_values = row[2:].values.reshape(3, 3).astype(np.float64)
    predecessors_list.append(get_predecessors(rtt_values).flatten())

Y = np.array(predecessors_list)
```
