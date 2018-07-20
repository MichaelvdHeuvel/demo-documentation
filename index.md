##Differences between merchant and merchant-demo

####Not all query parameters work

We kept the demo environment a mvp. Therefore not all query parameters are supported.

####Process status flow is mocked

We did not want to host a database and a queue on our demo environment and decided that we process status flow is going to be static.

####Invoices

Xml is not supported by spring cloud contracts, this is currently being build and will be released in the next version of spring cloud contract. Therefore Invoice calls only supports JSON.

####PDF endpoints

PDF files are not supported by spring cloud contracts, we decided to fix this on a later moment. Endpoints with PDF's do not work for now.

####Commission endpoints

The commission endpoints without the query params: condition, price gives the totalcost in the response while in Merchant this does only happen with the params. This is because of keeping the product as minimal as possible.
