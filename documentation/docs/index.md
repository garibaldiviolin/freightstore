# Freight Store

Freight Store is a freight REST API, that uses Python, Django and Django REST frameworks to receive the maps and the map's routes (between many points, including the distance), and then allows the client to query the shortest path (map points / routes sequence) and the freight rate of this path's distance. 

Since the freight map's structure matches well with graph data type, the idea is to use these structures to represent the points and routes (using the nodes and edges of graphs), and calculate the shortest path and distance using Dijkstra's algorithm.

The freight rate is based not only on the distance between the two points, but also on the fuel litter price and the vehicle fuel consumption, that is informed in the shortest path query.

The map's name, routes and distance between the points are persisted to a database, and when the client requests the shortest path and freight rate, the API uses the Networkx python library to load the graph's edges and points and to calculate the shortest path and distance using Dijkstra's algorithm. 

This python library was used since it performs well using multiple graph nodes and edges, and has a rich documentation. However, there are other python libraries that could be used instead.


## More information

* [Installing and Running](installation.md)
* [API Documentation](api.md)
