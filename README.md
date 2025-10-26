# Parallel Implementation of K-Means Clustering using OpenMP

## Submitted by
**Vandrangi Sai Vivek (2023BCS0161)**  
**Arun Lingeswar (2023BCS0173)**  
B.Tech – Computer Science and Engineering  
Indian Institute of Information Technology, Kottayam  

---

## 1. Introduction
K-Means is one of the most popular clustering algorithms in machine learning and data mining.  
It classifies a dataset into *k* distinct clusters based on feature similarity.  
However, the algorithm is computationally intensive for large datasets due to repeated distance calculations and centroid updates.

To overcome this, the project implements and compares **Sequential** and **Parallel (OpenMP)** versions of the K-Means algorithm.  
The objective is to analyze how parallelization improves performance while maintaining clustering accuracy.

---

## 2. Objectives
- To implement the standard K-Means clustering algorithm in C.  
- To parallelize the algorithm using **OpenMP**.  
- To compare execution times between sequential and parallel implementations.  
- To measure performance gain (speedup) with varying dataset sizes and thread counts.

---

## 3. Methodology

### 3.1 Sequential Implementation
1. Initialize `k` random centroids.  
2. Assign each data point to the nearest centroid.  
3. Update centroids as the mean of all points in the cluster.  
4. Repeat until convergence or until the maximum number of iterations is reached.  

This version executes on a single CPU core.

### 3.2 OpenMP Implementation
The parallelized version uses OpenMP to distribute computation among multiple threads:
- Each thread handles a subset of points during the **assignment** step.  
- Thread-local arrays are used to store partial sums and counts to minimize atomic operations.  
- After all threads finish, local results are merged to compute new centroids.  

This approach reduces synchronization overhead and improves scalability.

---

## 4. Experimental Setup
- **Processor:** Intel/AMD Multi-Core CPU  
- **Compiler:** GCC with OpenMP support  
- **Operating System:** Linux / Windows  
- **Language:** C (C99 standard)  
- **Number of Clusters (K):** 4  
- **Data Points:** 1,000 to 1,000,000  

---

## 5. Compilation and Execution

### Compile
```bash
# Sequential Version
g++ -fopenmp kmeans_sequential.cpp -o kmeans_seq

# OpenMP Version
gcc -fopenmp kmeans_openmp.cpp -o kmeans_omp -fopenmp

# Sequential
./kmeans_seq

# OpenMP with 8 threads
export OMP_NUM_THREADS=8
./kmeans_omp


7. Conclusion

The OpenMP-based K-Means implementation successfully reduces execution time compared to the sequential version.
Parallelization proves highly effective for large datasets, demonstrating the importance of shared-memory parallel computing in data-intensive tasks.

Future work could include:

Implementing K-Means++ initialization for better convergence.

Exploring SIMD vectorization for additional speedup.

Extending to higher-dimensional or real-world datasets.