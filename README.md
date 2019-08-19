TPC-H-Benchmarck-Anatella-Spark
===============================
Speed comparison between Anatella and Spark.

From the time measurements, it appears that Spark is not able to parallelize very well (i.e. it's incompressible runtime "s" is high). These results are confirmed by many independent researchers in the field: For example: The scientific paper named “Amdahl’s Law in Big Data Analytics: Alive and Kicking in TPCx-BB (BigBench)” also displays comparable incompressible runtimes (between 20% and 50%). This makes the whole Spark system nearly unusable since the major Spark promise (i.e. horizontal scalability: to deliver higher-speed on a larger infrastructure) is not achieved. This is not a particular problem from Spark "per se" since most distributed/parallel computation engines exhibit the same behavior that is perfectly explained by the Amdahl's Law (although the problem is quite visible in the case of Spark).

In other words: We observed that, for each TPC-H query, the total Anatella runtime is largely below the Spark incompressible time (we are cheking that with the script "compute_incompressible_time_s_v2.anatella"). This leads to the conclusion that Anatella has already finished all computations since a long time while Spark is still busy trying to complete its initialization/incompressible phase. 

The Hardware
============
These results were obtained on this machine: We used the “LDLC PC10 WANOMAN”. 
This is a standard configuration available on ldlc.com. The specs are:
* CPU: Intel Core i7-8086K (4.0 GHz) . It’s a 6 cores (12 threads) CPU.
* RAM: 16 GB (DDR4—3GHz—CL15)
* Storage: Samsung 870 SSD - NVMe - 2TB
The total price of this server is less than 3K€. 

The workload
============
We run the 22 queries from the TPC-H on 4 different database sizes: 1GB, 10GB, 100GB, 1TB.
The timing results used to compute the Spark incompressible times "s" originate from the executions on the 100GB database.

The data is stored inside .parquet files (for Spark) and .gel files (for TIMi). All the files are stored on a SSD drive (i.e. storing data on HDFS causes a huge speed penalty for Spark). We executed all queries in a non-interactive session (“as if” the queries were running during the night). This makes a big difference for Anatella since Anatella possesses an “interactive” mode that allows near instantaneous computation of the most complex queries (thanks to a unique advanced data-cache system).

Feel free to double-check yourself the results.

The results
===========
An analysis of the numerical results obtained on the TPC/H benchmarck is available here:
* White paper:           http://download.timi.eu/docs/Spark_vs_TIMi_technical_white_paper.pdf
* Summary for CEO:       http://download.timi.eu/docs/Spark_vs_TIMi_Executive_Summary.pdf
* Pptx presentation:     http://download.timi.eu/docs/TIMi_vs_Spark.pdf


