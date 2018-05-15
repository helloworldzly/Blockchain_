# [Paper]Detecting Ponzi Schemes on Ethereum: Towards Healthier Blockchain Technology

#### The paper is published in WWW 2018, the full paper please visit: [dblp:Zibin Zheng](http://dblp.uni-trier.de/pers/hd/z/Zheng:Zibin)


#### Abstract
The paper builds a XG-Boost based classification model to detect Ponzi contracts in Ethereum using features from use accounts and operation codes.

#### Contribution
* The previous study used **normalized Levenshtein distance**  to compute similarity between bytecodes, but it derectly uses bytecode features(opcode frequency).
* It combines contract behavior and bytecode features, and is more accurate in detecting Ponzi schemes, and finds more hidden abnormal contracts.

#### Framework

![framework](/img/framwork.jpg)
