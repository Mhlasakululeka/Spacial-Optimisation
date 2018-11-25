
# Spatial Optimisation Problem


Formally, the problem asks to find the optimal time (minimum time) route between different locations in KwaZulu Natal.The locations are as folllow:
1. 115 St Andrews Drive, Durban North, KwaZulu Natal, South Africa
2. 67 Boshoff Street, Pietermaritzburg, KwaZulu Natal, South Africa
3. 4 Pual Avenue, Fairview, Empangeni, KwaZulu Natal, South Africa
4. 166 Kerk Street, Vryheil, KwaZulu Natal, South Africa
5. 9 Margaret Street, Ixopo, KwaZulu Natal, South Africa
6. 16 Poort Road, Ladysmith, Durban North, KwaZulu Natal, South Africa

Informally, you have a delivery driver who wants to visit a number of delivery address locations and wants to find the shortest path to visit all the locations.

An exhaustive search of all possible paths would be guaranteed to find the shortest, but is computationally intractable for all but small sets of locations. For larger problems, optimization techniques are needed to intelligently search the solution space and find near-optimal solutions.![img](tsp.png) 

## Travelling Salesman Problem
The travelling salesman problem (TSP) asks the following question: "Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city and returns to the origin city ? Wesolve the above mentioned sptial optimisation problem by using this approach

##  Solving TSPs with OR-Tools
You can solve TSPs using the OR-Tools [vehicle routing library](https://developers.google.com/optimization/reference/constraint_solver/routing/), a collection of algorithms designed especially for TSPs, and more general problems with multiple vehicles. The routing library is an added layer on top of the [constraint programming](https://developers.google.com/optimization/cp/) solver. See [RoutingModel](https://developers.google.com/optimization/reference/constraint_solver/routing/RoutingModel/) for detailed information about the available methods for setting up and solving routing problems.
___


## Installation
```
pip install ortools
```
### The following section represent python program that solves the obove mentioned problem.  


The data for the problem: the lovcations and the distance matrix, whose entry in row i and column j is the distance from location i to location j in km. The figure shows the distance matrix between each location.
<img src="DATA.png" width="600">


### The following code declares an instance of the solver and sets the default options for it.
```
  tsp_size = len(address_names)
  num_routes = 1
  depot = 0

  # Create routing model
  if tsp_size > 0:
    routing = pywrapcp.RoutingModel(tsp_size, num_routes, depot)
    search_parameters = pywrapcp.RoutingModel.DefaultSearchParameters()
    # Create the distance callback.
    dist_callback = create_distance_callback(dist_matrix)
    routing.SetArcCostEvaluatorOfAllVehicles(dist_callback)
```
The instance solver is declared by 
```
routing = pywrapcp.RoutingModel(tsp_size, num_routes, depot)
```

