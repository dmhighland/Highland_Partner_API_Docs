# Highland_Partner_API_Docs

## Summary
Highland Soltuions LLC is a eSIM wholesaler. We distribute eSIMs to our partners in bulk, and these partners may use Highland Partner APIs to manage their eSIM portfolio.

Please contact Highland Solutions LLC for API access info: https://www.highlandai.net/, david@highlandai.net.


## Onboarding Company

A partner may call this API to onboard:

**PUT /b2b/company**

This creates a company entitiy and assigns a company ID.

## Acquire eSIM

With a company ID assignd, the partner may call this API to acquire an eSIM:

**POST /b2b/sim/acquire**

This API doesn't require specific eSIM ID, as the system will automatically assign the next available eSIM with the provided company ID. 

The LPA code and installation bar code URL will be returned as part of the response. The bar code is good for 3 days after activation. 


If the partner knows a given eSIM id, another API call may assigne that eSIM ID to the given company ID.

**POST /b2b/sim/acquire/simid**

## Query Default Data Product List

The partner may define its own data products, or use any of the default data products.

To see the default data product list, the partner may use Highland's company ID to query the built-in product list: 4345d86fbf8a11f09f474c50dd6c0d86 with the following API:

**GET /b2b/company/product_list**

## Add Data Product to eSIM

The partner may add a data product to an eSIM with the following API:

**POST /b2b/sim/product/add**

## Remove Data Product from eSIM

The partner may also remove a data product from an eSIM with the following API:

**POST /mvno/sim/product/remove**

## Check Data Usage

The parner may use the follwoing API to query data usage with the current data product:

**GET /b2b/sim/product_usage**

## Check Data Usage With Time Window

If the parter wants to query data usage within a given time window, this API is available:

**GET /b2b/sim/product_usage/window**

## Check Data Usage On All Products

If the given eSIM has mulltiple data products provisioned, this following API can be used to query usage on all products:

**GET /b2b/sim/product_usage/all_product/**

## Suspend eSIM

To suspend a given eSIM, a partner may use the following API:

**POST /b2b/sim/suspend**

Note: Highland Solutions LLC doesn't provide APIs to deactivate an eSIM at this time. Suspend is the only way to prevent an eSIM to consume data services. 

## Restore eSIM

To restore a given eSIM, a partner may use the following API:

**POST /b2b/sim/restore**

