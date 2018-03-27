# Artist Market
### An Hyperledger Composer business network exercise

#HSLIDE

#HSLIDE

#HSLIDE

Model

```
participant Buyer identified by email { ...  }

participant Artist identified by email { ...  }

asset Request identified by requestId {
    o String requestId
    o String description
    o Double price
    --> Buyer buyer
    --> Artist artist
}

asset Commission identified by comissionId {
    o String comissionId
    o String url
    --> Buyer buyer
    --> Artist artist
    --> Request request
}

transaction RequestTx { o Request request }

transaction CommissionTx { o Commission commission }
```

#HSLIDE

Access Control

```
rule Artist {
    description: "Allow artists to see all requests"
    participant(i): "org.acme.artistmarket.Artist"
    operation: READ
    resource(a): "org.acme.artistmarket.Request"
    condition: (true)
    action: ALLOW
}

rule Buyer {
    description: "Allow buyer to see their commissions"
    participant(i): "org.acme.artistmarket.Buyer"
    operation: READ
    resource(a): "org.acme.artistmarket.Commission"
    condition: (a.buyer.email == i.email)
    action: ALLOW
}
```
