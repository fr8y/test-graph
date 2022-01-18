# init
```graph init```

  Creates subgraph.yaml, schema.graphql, enerated/schema.ts, src/mapping.ts
  

  Fetch ABI from etherscan


- generated/schema.ts - Define entities
- src/mapping.ts - Mapping events to entities 
- schema.graphql - Mapping entities to graphql type 

# build
```graph build```

Compile data source to build/ .wasm


Copy schema file to build/ .graphql


Write subgraph file to build/ .json


Write subgraph manifest to build/ .yaml


# create
```graph create --node http://44.192.123.37:8020 test/felix```

# deploy
```graph deploy --node http://44.192.123.37:8020 --ipfs http://44.192.123.37:5001 test/felix```

# remove
```graph remove --node http://44.192.123.37:8020 test/felix```

# status page
Open in web browser ```http://44.192.123.37:8030/graphql/playground``` to run queries

```http://44.192.123.37:8030/``` will return "OK" if node running

Replace "Qm...." with string returned from successful ```graph deploy```

Run query to display status for that subgraph
```
{
  indexingStatuses(subgraphs: ["Qm...."]) {
    node
    synced
    health
    fatalError {
      message
      block {
        number
        hash
      }
      handler
    }
    nonFatalErrors {
      message
      block {
        number
        hash
      }
      handler
    }
    chains {
      network
      chainHeadBlock {
        number
      }
      earliestBlock {
        number
      }
      latestBlock {
        number
      }
      lastHealthyBlock {
        number
      }
    }
    entityCount
  }
}
```

# query entities
Navigate to URL returned from successful ```graph deploy```


```http://44.192.123.37:8000/subgraphs/name/test/felix/graphql```


```
query approvals{
  approvalEntities(subgraphError: deny orderBy: id orderDirection: desc first: 100){
    id
    count
    owner
    operator
    approved
  }
}
```


```
query transfers{
  transferEntities(subgraphError: deny orderBy: id orderDirection: desc first:100){
    from
    to
    tokenId
  }
}
```


```
query transfers{
  transferEntities(subgraphError: deny where:{tokenId: 6712}){
    from
    to
    tokenId
  }
}
```