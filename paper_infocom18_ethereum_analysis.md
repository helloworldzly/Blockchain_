# [Paper]Understanding Ethereum via Graph Analysis

#### The paper is published in INFOCOM 2018, the full paper can visit: [INFOCOM: Ting Chen](http://www4.comp.polyu.edu.hk/~csxluo/EthereumGraphAnalysis.pdf)

### Abstract
In this paper, we conduct the **first systematic study** on Ethereum by leveraging graph analysis to characterize three major activities on Ethereum, namely **money transfer, smart contract creation, and smart contract invocation**. We propose new approaches based on cross-graph analysis to address two security issues in Ethereum, including **attack forensics** and **anomaly detection**.

### Overview
![overview](/img/overview.jpg)

### Data Collection
* All transactions of Ethereum on July, 30th, 2015 to June, 10th, 2017: 28,502,131 external tx and 19,759,821 internal tx
* Customized EVM: replay all external tx to get internal ones by inserting instrumentation code
* Five operations leading to internal tx: CREATE, CALL, CALLCODE, DELEGATECALL, SELFDESTRUCT(SUICIDE)

### Graph Construction
* **Preprocess:** exclude 4 kinds of tx(external tx without Ether, self-destruct contracts with no Ether remaining, unsuccessful tx among EOAs, failed tx for contract creation)
* **Construction:** divide tx into three groups(MF, CC, CI)
* **Statistics:** the distribution of the Num of transactions related to accounts

### Graph Statistics
![distribution](/img/distribution.jpg)

* (a)0.8% of EOAs do not transfer Ether.
* (a)More than 2/3(point(0,0.69)) contracts do not transfer Ether
* (a)About 81%(0.96 contracts, 0.77 EOAs) have no more than 5 tx

* (b)99%(point(0,0.99)) EOAs do not create contracts = only 1% developers(?)
* (b)99.5% contracts are involved in 1 tx(point(0, 0.995))

* (c)73% EOAs do not invoke contracts, 96% EOAs call contracts no more than 5 times
* (c)81% contracts are not invoked
* (c)60% contracts neither transfer money nor be invoked(waste resources) 

### Graph Construction
* **MFG**: a weighted directed graph, each edge with a weight, which is the total amount of transferred Ether.
* **CCG**: a forest consisting of multiple trees. The root is an EOA, other nodes are contracts directly or indirectly created by the root.
* **CIG**: a wighted directed graph, each edge with a weight, which is the total number of invocations.

### Insights
* **Insight 1:** Users prefer to transferring money on Ethereum instead of using smart contracts.
* **Insight 2:** Smart contracts are not used widely.
* **Insight 3:** Not all users frequently use Ethereum. 

### Graph Analysis
* **SCC/WCC:** strong/weak connected component. SCC: a sub-graph where there is a path from every node to every other node).
* **Clustering coefficient:** a measure of the degree to which nodes in a graph tend to cluster together.
* **Pearson coefficient:** evaluate the correlation between the indegree and out degree of nodes.(value in [-1, 1])
* **Assortativity coefficient:** evaluate the preference for nodes to attach to others.
* **PageRank algorithm:** evaluate node’s importance.
* **Node identity: check all nodes in WCC to look for hints about their identity.**

### MFG Analysis
![graph_metric.jpg](/img/graph_metric.jpg)
![10_nodes_MFG.jpg](/img/10_nodes_MFG.jpg)
* **Degree/Indegree/Outdegree distribution:** the power law, a few large-degree nodes and many small-degree nodes.
* **Clustering coefficient is large:** A-C, B-C then A-B
* **Assortativity coefficient is negative:** a large-degree node prefer to trade with  small-degree node(exchange)
* **Pearson coefficient:** deposit is uncommon in Ethereum
* The largest **SCC** contains 86% nodes: **hub nodes.**






