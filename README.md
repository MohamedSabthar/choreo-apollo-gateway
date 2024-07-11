A federation example written using Ballerina graphql

How to run:
1. Use Ballerina 2201.5.0 (Swan Lake Update 5)
2. Execute command `bal run product` to start the product service
3. Execute command `bal run review` to start the review service
4. Execute command `cd gateway && npm start` to start the gateway

Try the following queries and mutation:
1. View the reviews of a product:
```graphql
query Product($productId: String!) {
  product(id: $productId) {
    title
    reviews {
      comment
    }
  }
}
```

```
{
  "productId": "1"
}
```

2. Add a review to a product:
```graphql
mutation Mutation($reviewInput: ReviewInput!) {
  addReview(reviewInput: $reviewInput) {
    comment
  }
}
```

```
{
  "input": {
    "bookId": "1",
    "author": "hema22",
    "comment": "nice book"
  }
}
```

3. Again execute 1 to view the newly added reviews

curl --location 'https://c33dcfdf-5752-4e3c-9d16-9c2d9719b1db-dev.e1-us-east-azure.choreoapis.dev/ffme/gateway/v1.0/' \
--header 'Content-Type: application/json' \
--data '{"query": "query Product {\n products {\n id \n title \n description \n price \n reviews {\n id \n rating \n comment \n author \n } \n } \n }"
}'