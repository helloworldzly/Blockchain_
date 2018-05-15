# [Paper]Detecting Ponzi Schemes on Ethereum: Towards Healthier Blockchain Technology

#### The paper is published in WWW 2018, the full paper please visit: [dblp:Zibin Zheng](http://dblp.uni-trier.de/pers/hd/z/Zheng:Zibin)


#### Abstract
The paper builds a XG-Boost based classification model to detect Ponzi contracts in Ethereum using features from accounts and operation codes.

#### Contribution
* The previous study used **normalized Levenshtein distance**  to compute similarity between bytecodes, but it derectly uses bytecode features(opcode frequency).
* It combines contract behavior and bytecode features, and is more accurate in detecting Ponzi schemes, and finds more hidden abnormal contracts.
* Detect Ponzi contracts even the source codes are intentional hidden
* Detect Ponzi schemes before it causing any damage
* Build a risk warning platform based on it


#### Framework

![framework](/img/framwork.jpg)

* Collect transaction data from Etherscan.io and get the Ether Flow Graph of contracts
* Ponzi contract behavior: the operator generates returns for older investors through revenue paid by new investors. Participants' confidence in continuously paying back is the key factor in successful operation of Ponzi schemes.
* The sending Ether transaction is called **normal tx** and the tiggered payment transaction is called **fired tx** 
* Use a disassembly tool to get the operation code(like PUSH, ADD..) and calculate their frequency in a contract
* Draw the Ether flow of a contract to extract its account features

#### Feature and Metric
* Known Rate(Kr): the proportion of recievers who have invested before payment. High Kr means the the contract interact more with Acs knew.
* Balance: contract balance
* N_investment: # investments
* N_payment: # payments
* Difference index(D_ind): measure the difference of Acs between payment and investment for all participants in a contract. D_ind is negative as many users invest more and receive less.
* Paid rate: # investors who get at least one payment
* N_maxpay(N_max): the max of counts of payments to participants.

* **Code Feature**: opcode frequency vector

* **Evaluation metrics**: Precision, Recall, F-score

#### Conclusion

区块链领域的data analysis难点在于没有label和ground truth，无法进行各种训练模型的效果对比，只能从insight角度讲story。本文抓住Ponzi scheme场景，人工检测合约代码挑出131 Ponzi合约和1251 non-Ponzi合约作为训练数据，根据合约用户的Ether交易流特征和合约opcode频率向量作为Feature，训练XGBoost回归分类模型检测Ponzi合约，并用一些评测metric表明模型效果不错，且用模型检测出更多的潜在Ponzi合约（不过这部分也无法知道是否检测正确，因为潜在的都是合约不公开的，不知道实际行为）。Pros：提供利用opcode的新思路
