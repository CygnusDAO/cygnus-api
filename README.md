# Cygnus Finance Indexer and GraphQL API

Indexer used across all deployed chains to get the latest information of the protocol and lending pools. This includes:

* Total Value Locked
* Total Borrows
* Total LPs deposited
* Borrow APYs
* Supply APYs
* Liquidations
* Liquidators
* Current Borrowers
etc, etc.
<br /> 

The API is publicly accessible at https://api.cygnusdao.finance, making it easy for developers to integrate Cygnus Finance data into their applications. 

It is also used by the dApp frontend to check for latest borrow positions, allowing liquidators to monitor loans and liquidate positions.

## Example Queries

### Get all lender addresses on Arbitrum:

```graphql
query Lenders {
  cygUSDHolders(where: { chainId: 42161}) {
    balance
    shuttleId
    borrowable
    holder
  }
}
```

Output:

```JSON
{
  "data": {
    "cygUSDHolders": [
      {
        "balance": "0.001",
        "shuttleId": "2",
        "borrowable": "0x2236993E0a2F1dA1A9dC41A4F93547363210C5b2",
        "holder": "0x0000000000000000000000000000000000000000"
      },
      {
        "balance": "61.538687",
        "shuttleId": "2",
        "borrowable": "0x2236993E0a2F1dA1A9dC41A4F93547363210C5b2",
        "holder": "0x66EC0Da50B1B54A52817417FE1A92dF7A961d149"
      },
      {
        "balance": "0.000002",
        "shuttleId": "2",
        "borrowable": "0x2236993E0a2F1dA1A9dC41A4F93547363210C5b2",
        "holder": "0x90e06d2d9705c181Bad2A4e7c3DcA13631a6f479"
      },
      {
        "balance": "87.776556",
        "shuttleId": "2",
        "borrowable": "0x2236993E0a2F1dA1A9dC41A4F93547363210C5b2",
        "holder": "0xAaF79B2956080cdfb589216db4f3cfb5c3A33A59"
      },
      {
        "balance": "524.136032",
        "shuttleId": "2",
        "borrowable": "0x2236993E0a2F1dA1A9dC41A4F93547363210C5b2",
        "holder": "0xC7d15f80A49F396e9D5B0c07DB9D727deEaE52fc"
      },
      {
        "balance": "0.001",
        "shuttleId": "1",
        "borrowable": "0x27314579D48209786491ade5621a2cc3c2b2a644",
        "holder": "0x0000000000000000000000000000000000000000"
      },
    ]
  }
}
```
### Get all current borrowers on Polygon

```graphql
query Borrowers {
  borrowers(where: {chainId: 137}) {
    borrower
    positionUSD
    borrowBalance
    principal
    health
  }
}
```

Output:

```JSON
{
  "data": {
    "borrowers": [
      {
        "borrower": "0x19A313d0D3eF1Cd269817aE4f943DFf55CfF2568",
        "positionUSD": "38.260865",
        "borrowBalance": "30.569506",
        "principal": "30.569506",
        "health": "88.3078540691585021"
      },
      {
        "borrower": "0x66EC0Da50B1B54A52817417FE1A92dF7A961d149",
        "positionUSD": "154.177276",
        "borrowBalance": "139.34109",
        "principal": "139.34109",
        "health": "99.8905793074204592"
      },
      {
        "borrower": "0xAaF79B2956080cdfb589216db4f3cfb5c3A33A59",
        "positionUSD": "780.411062",
        "borrowBalance": "700.774219",
        "principal": "700.774219",
        "health": "99.2476868950212789"
      },
      {
        "borrower": "0xB7249313d22590f7d336Fb256cae48eB96bb1547",
        "positionUSD": "42.557563",
        "borrowBalance": "0.000006",
        "principal": "0.000006",
        "health": "0.0000155826100253"
      },
    ]
  }
}
```
### Get information of the protocol on all chains

```JSON
{
  "data": {
    "chains": [
      {
        "id": 137,
        "chainName": "polygon",
        "cygnusTvlUSD": "16776.842269",
        "allBorrowablesUSD": "13053.584353",
        "allCollateralsUSD": "3723.257916",
        "totalBorrowsUSD": "3658.291804",
        "totalLiquidations": 15
      },
      {
        "id": 42161,
        "chainName": "arbitrum",
        "cygnusTvlUSD": "6201.485529",
        "allBorrowablesUSD": "3382.377427",
        "allCollateralsUSD": "2819.108102",
        "totalBorrowsUSD": "2227.885818",
        "totalLiquidations": 3
      }
    ]
  }
}
```



