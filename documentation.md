# Documentations

[TOC]


## Introduction
This Project Solves the Traveling Sales Person Problem using genetic algorithm with the following properties:
* Chromosomes decoded as cycles (solutions) of traveling
* Order 1 crossover
* Swap mutation
* Complete generation replacement
* Roulette Wheel Technique for choosing parents
* Negative of cycle distance as fitness

## Libraries
This project has been coded in Python 3.5 and the following libraries have been used:
* random
* math
* numpy 1.13.1+mkl
* matplotlib 2.0.0
* collections

## Functions
The following functions make up the code:
### 1. TSP_genetic
*Solves the Traveling Sales Person Problem using genetic algorithm with chromosomes decoded as cycles (solutions) of traveling Order 1 crossover, Swap mutation, complete generation replacement, Roulette Wheel Technique for choosing parents and negative of cycle distance for fitness.*

* **Parameters**:
	* **n**: integer denoting the number of points and also the number of genome of each chromosom
	* **k**: integer denoting the number of chromosomes in each population
	* **max_generation**: integer denoting the maximum generation (iterations) of the algorithm
	* **crossover_probability**: float in [0,1] denoting the crossover probability
	* **mutation_probability**: float in [0,1] denoting the mutation probability
	* **path**: string that indicates the path to the text file containing coordinates of n points
* ***Return Parameter***:
	* **None**
* ***Call to Functions***:
	* **read_input**
	* **init_population**
	* **compute_population_fitness**
	* **find_best_individual**
	* **create_new_population**
	* **plot_results**

### 2. read_input
*Reads the first N lines of the .txt file denoted by path containing the coordinates of the points in the following format:*

*x_1 y_1*

*x_2 y_2*

*...*

* **Parameters**:
	* **path**: string that indicates the path to the text file containing coordinates of n points
* ***Return Parameter***:
	* **|Nx2| numpy.array of coordinates of points**
* ***Call to Functions***:
	* **None**

### 3. init_population
*Initializes the population of K chromosomes with N genome for each chromosome by modifying pop.*


* **Parameters**:
	* **K**: number of chromosomes
    * **N**: number of genomes in each chromosome
* ***Return Parameter***:
	* **|KxN| numpy.array of K chromosomes with N genome for each**
* ***Call to Functions***:
	* **None**

### 4. compute_population_fitness
*Computes the fitness for each chromosome in the population by modifying fit. (Fitness of each chromosome is the negative of its cycle distance.)*

* **Parameters**:
	* **pop**: |KxN| list/numpy.array of K chromosomes with N genome for each
    * **points**: |Nx2| list/numpy.array of coordinates of points
    * **K**: number of chromosomes
    * **N**: number of genomes in each chromosome
* ***Return Parameter***:
	* **fit, a |K| list/numpy.array of floats where fit[k] = fitness of pop[k].**
* ***Examples***:

        >>> compute_population_fitness([[0,3,1,2],[2,1,0,3]],[[0,0],[0,4],[3,4],[3,0]],2,4)
        array([-16., -14.])
        
* ***Call to Functions***:
	* **distance**

### 5. find_best_individual
*Finds the best individual and the fitness of that individual in all the generations.*
* **Parameters**:
    * **pop**: |KxN| list/numpy.array of K chromosomes with N genome for each
    * **fitness**: |K| list/numpy.array of numbers representing the fitness for each chromosome
    * **best_individual**: |N| list/numpy.array representing the best individual/chromosome so far excluding the current population.
    * **best_fit**: number representing the fitness of best_individual
* ***Return Parameter***:
	* **{best individual so far},{fitness of best individual so far}**
* ***Call to Functions***:
	* **None**

### 6. create_new_population
*Creates a new population of K chromosomes of N genomes by crossovers and mutations over the current population.*
* **Parameters**:
    * **pop**: |KxN| list/numpy.array of K chromosomes with N genome for each chromosome representing the current population
    * **fitness**: |K| list/numpy.array of fitness of each chromosome in pop
    * **K**: number of chromosomes
    * **N**: number of genomes in each chromosome
    * **crossover_probability**: float in [0,1] representing crossover probability
    * **mutation_probability**: float in [0,1] representing mutation probability
* ***Return Parameter***:
	* **|KxN| list/numpy.array of K chromosomes with N genome for each chromosome representing the new population**
* ***Call to Functions***:
	* **select_parent**
	* **decide_to**
	* **crossover**
	* **mutate**

### 7. plot_results
*Plots and displays the best last 15 chromosomes generated through the generations.*
* **Parameters**:
    * **pop**: |KxN| list/numpy.array of K chromosomes with N genome for each chromosome representing the current population
	* **best_last_15**: |M| deque/list of (A,B) where A is one of the best chromosomes and B is its cycle distance and M<=15
    * **points**: |Nx2| list/numpy.array of coordinates of points
* ***Return Parameter***:
	* **None**
* ***Call to Functions***:
	* **plot_individual_path**


### 8. distance
*Computes the euclidean distance of a cycle*
* **Parameters**:
    * **points**  : |Nx2| list/numpy.array of coordinates of points
    * **order**   : |N|   list/numpy.array of ordering of points (zero indexed)
* ***Return Parameter***:
	* **euclidean distance of points from point0 to point1 to ... to pointN back to point0**
* ***Examples***:

        >>> distance([[0,0],[0,4],[3,4]],[0,1,2],3)
        12.0
        
* ***Call to Functions***:
	* **None**

### 9. select_parent
*Select and index for parent based on fitness of each chromosome using the roulette wheel technique.*
* **Parameters**:
    * **fitness**: |K| list/numpy.array of numbers representing the fitness for each chromosome
    * **K**: length of fitness
* ***Return Parameter***:
	* **index of the randomly selected parent**
* ***Call to Functions***:
	* **find_cumulative_distribution**

### 10. decide_to
*Randomly returns True/False based on probability.*
* **Parameters**:
    * **p**   :float of [0,1]; probability of the return value being True
* ***Return Parameter***:
	* **True with the probability of p and False with the probability of (1-p)**
* ***Call to Functions***:
	* **None**


### 11. crossover
*Performs the Order 1 Crossover and produces two children by modifying child1 and child2.*
* **Parameters**:
    * **father**: |N| list/numpy.array representing the father chromosome
    * **mother**: |N| list/numpy.array representing the mother chromosome
    * **child1**: |N| list/numpy.array representing the first child
    * **child2**: |N| list/numpy.array representing the second child
    * **N**: length of all the input chromosomes
* ***Return Parameter***:
	* **None**
* ***Call to Functions***:
	* **None**

### 12. mutate
*Mutates the individual ind by swapping two genomes.*
* **Parameters**:
	* **ind** : |N| list/numpy.array of chromosome/individual
    * **N**   : length of ind
* ***Return Parameter***:
	* **None**
* ***Call to Functions***:
	* **None**

### 13. plot_individual_path
*Plots individual cycle in the index of a 3x5 plot*
* **Parameters**:
    * **individual**:  |N| list/numpy.array of a chromosome
    * **points**: |Nx2| list/numpy.array of coordinates of points
    * **title**: title of the plot
    * **index**: integer in [1,15] denoting the position of the plot in a 3x5 matplotlib subplots.
* ***Return Parameter***:
	* **None**
* ***Call to Functions***:
	* **None**

### 14. find_cumulative_distribution
*Computes cumulative distribution (percentages) of arr.*
* **Parameters**:
	* arr: |K| numpy.array of numbers.
    * K: length of arr
* ***Return Parameter***:
	* **cd**: |K| numpy.array of floats containing the cumulative distributions
        where cd[i] is the probability that a uniform random number in [0,arr.sum()] is
        less than arr[:i].sum()
* Examples:
 
        >>> find_cumulative_distribution(numpy.array([4,2,2]),3)
        array([ 0.5 ,  0.75,  1.  ])
 
* ***Call to Functions***:
	* **None**

## Author

[Amin Fadaee](https://www.linkedin.com/in/aminfadaee/)

## License
The MIT License. Copyright (c) 2017 Amin Fadaee
