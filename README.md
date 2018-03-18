# Hyperledger Fabric 

### Hyperledger fabric delivers the following advantages:
* Chaincode trust flexibility - The architecture separates trust assumptions for chaincodes (blockchain applications) from trust assumptions for ordering. In other words, the ordering service may be provided by one set of nodes (orderers) and tolerate some of them to fail or misbehave, and the endorsers may be different for each chaincode.
* Scalability - As the endorser nodes responsible for particular chaincode are orthogonal to the orderers, the system may scale better than if these functions were done by the same nodes. In particular, this results when different chaincodes specify disjoint endorsers, which introduces a partitioning of chaincodes between endorsers and allows parallel chaincode execution (endorsement). Besides, chaincode execution, which can potentially be costly, is removed from the critical path of the ordering service.
* Confidentiality - The architecture facilitates deployment of chaincodes that have confidentiality requirements with respect to the content and state updates of its transactions.
* Concensus modularity - The architecture is modular and allows pluggable consensus (i.e., ordering service) implementations.

### System Architecture:
The blockchain is a distributed system consisting of many nodes that communicate with each other. The blockchain runs programs called chaincode, holds state and ledger data, and executes transactions. The chaincode is the central element as transactions are operations invoked on the chaincode. Transactions have to be “endorsed” and only endorsed transactions may be committed and have an effect on the state. There may exist one or more special chaincodes for management functions and parameters, collectively called system chaincodes.

#### Transactions:
Transactions may be of two types:
* Deploy transactions create new chaincode and take a program as parameter. When a deploy transaction executes successfully, the chaincode has been installed “on” the blockchain.
* Invoke transactions perform an operation in the context of previously deployed chaincode. An invoke transaction refers to a chaincode and to one of its provided functions. When successful, the chaincode executes the specified function - which may involve modifying the corresponding state, and returning an output.

#### Blockchain datastructues:
##### State:
The latest state of the blockchain (or, simply, state) is modeled as a versioned key/value store (KVS), where keys are names and values are arbitrary blobs. These entries are manipulated by the chaincodes (applications) running on the blockchain through put and get KVS-operations. The state is stored persistently and updates to the state are logged. Notice that versioned KVS is adopted as state model, an implementation may use actual KVSs, but also RDBMSs or any other solution.

More formally, state s is modeled as an element of a mapping K -> (V X N), where:

* <span style="color:red">K</span> is a set of keys
* <span style="color:red">V</span> is a set of values
* <span style="color:red">N</span> is an infinite ordered set of version numbers.