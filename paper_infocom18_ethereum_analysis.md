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








