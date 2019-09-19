```graphql
interface Requriment{
  name: String!
}


type Any implements Requirement {name: String!} 
type Latest implements Requirement {name: String!}

type GT implements Requirment{
  name: String!
  version: String!
}

type GTE implements Requirment{
  name: String!
  version: String!
}

type LT implements Requirment{
  name: String!
  version: String!
}

type LTE implements Requirment{
  name: String!
  version: String!
}



```
