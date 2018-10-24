### How Representative is a SPARQL Benchmark? An Analysis of RDF Triplestore Benchmarks
We provide a fine-grained comparative analysis of existing triplestore benchmarks. In particular, we have analyzed the data and queries, provided with the existing triplestore benchmarks in addition to several real-world datasets. Further, we have measured the correlation between the query execution time and various SPARQL query features and ranked those features based on their significance levels. Our experiments have revealed  several interesting insights about the design of such benchmarks. We can hope such fine-grained evaluation will be helpful for SPARQL benchmark designers to design diverse benchmarks in the future.

### Licence 
All of the data and results presented in our evaluation will be available under [GNU General Public License v3.0].

### Benchmark Datasets and Queries
We provide the datasets and queries of the benchmarmks and real-world datasets used in our evaluation. The datasets are also provided as portable virtuoso triplestores which can be started from bin/start_virtuoso.sh.

Datasets are available at our research group's site (redacted to allow double blind reviewing).

### Analysis
Our analysis is based on the following benchmark design features:
* Dataset structuredness (**dataset related**)
* Dataset relationship specialty (**dataset related**)
* Overall queries diversity score based on important SPARQL query features, i.e., number of triple patterns, number of projection variables, result set sizes, query execution time, number of BGPs, number of join vertices, mean join vertex degree, mean triple pattern selectivities, BGP-restricted and join-restricted triple pattern selectivities, and join vertex types. (**queries related**)
* Percentages-wise distribution of the use of important SPARQL clauses (e.g., LIMIT, OPTIONAL, ORDER BY, DISTINCT,
UNION, FILTER, REGEX) in benchmark queries  (**queries related**)
* SPearsman's correlation of the query runtimes and important SPARQL query features (**queries related**)

The first two features are related to benchmark datasets and later three are related to benchmark queries. Please refer to the manuscript for the details of above design features.

### Reproducing Results
Please follow the following steps to reproduce the complete results presented in the paper.
 1. Download the folder `cli` which contains a runable jar **benchmark-util.jar** (removed from the repository to allow double blind reviewing).
 2. To calculate the structuredness or relationship specialty of an RDF datasets, we need to first load the dataset into a triple store and provide the endpoint url as input to the jar file. The linux based virtuoso SPARQL endpoints of the datasets of all the triplestore benchmarks and real-world datasets used in our evaluation can be downloaded from our research group's site. Note the virtuoso can be started from bin/start_virtuoso.sh script. The utility work for any SPARQL endpoint.
 3. Download the Virtuoso instance which contains the LSQ datasets of all the selected 10 triplestores benchmarks and 5 real-world datasets.

 ```html
java -jar benchmark-util.jar  -m <measure> -e <endpoint> -g <graph> -q <queriesFile>

where

measure = structuredness or specialty or diversity or percentage or correlation
endpoint = endpoint url
graph = graph name (optional)
queriesFile = queries file (only required to produce queries related statistics, i.e., diversity, percentages, and correlation).
 please note the queries files are already provided with the cli folder downloaded in step 1.

An example formats:
java -jar benchmark-util.jar -m structuredness -e http://localhost:8890/sparql
java -jar benchmark-util.jar -m specialty -e http://localhost:8890/sparql -g ...

java -jar benchmark-util.jar -m diversity -e http://localhost:8890/sparql -g ... -q queries-diversity.txt
java -jar benchmark-util.jar -m percentage -e http://localhost:8890/sparql -q queries-percent.txt -g ...
java -jar benchmark-util.jar -m correlation -e http://localhost:8890/sparql -q queries-correlation.txt -g ...

You can run SPARQL SELECT DISTINCT ?g WHERE { GRAPH ?g {?s ?p ?o }} on the virtuoso downloded in step 2 to get the graph names of all the selected benchmarks and real-world datasets. Note you can add more queries into the input files in -q argument to get results for other features.
```

### Complette Evaluation Results
Our complete evaluation results can be found [here](complete-evaluation-results.xlsx)
