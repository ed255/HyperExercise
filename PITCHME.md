# Artist Market
### An Hyperledger Composer business network exercise

#HSLIDE

- Marketplace for artists to sell commissions that fulfill individual requests.

- A buyer will submit a request for a particular artists with a price and description.

- The artist may fulfill a request and get paid for the commission.

#HSLIDE

### Model

Participants: Buyer, Artist

Assets: Request, Comission

Transactions: RequestTx, CommissionTx

- Transactions just publish the Request/Comission to the network.

- A published commission can only be seen by the seller.

#HSLIDE

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
```

#HSLIDE

Access Control

```
rule Artist {
    description: "Allow artists to see all requests"
    participant(i): "org.acme.artistmarket.Artist"
    operation: READ
    resource(a): "org.acme.artistmarket.Request"
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
