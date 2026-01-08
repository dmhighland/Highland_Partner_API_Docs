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

## Examples

A company id has been created: "1a9a1d8ddc9311f09e024c50dd6c0d86". 

You can test query this company with this API: GET "/b2b/company/summary".

You can then call the eSIM acquire API, POST "/b2b/sim/acquire". This API wil acquire an eSIM for the given company id. 

If there is no more eSIM in the inventory, this API will fail with error: {"status":"failure","details":"No more eSIM available for activation."}

If you need to add more fake eSIM to inventory for testing, you can use this API: PUT "highland/esim", example:

61007763,8948010000042217613,260010191724652,14254458443,1$sm-dp-address.com$ACTIVATIONCODE12346
61007764,8948010000042217614,260010191724653,14254458444,1$sm-dp-address.com$ACTIVATIONCODE12347
61007765,8948010000042217615,260010191724654,14254458445,1$sm-dp-address.com$ACTIVATIONCODE12348
61007766,8948010000042217616,260010191724655,14254458446,1$sm-dp-address.com$ACTIVATIONCODE12349
61007767,8948010000042217617,260010191724656,14254458447,1$sm-dp-address.com$ACTIVATIONCODE12350
61007768,8948010000042217618,260010191724657,14254458448,1$sm-dp-address.com$ACTIVATIONCODE12351
61007769,8948010000042217619,260010191724658,14254458449,1$sm-dp-address.com$ACTIVATIONCODE12352
61007770,8948010000042217623,260010191724659,14254458450,1$sm-dp-address.com$ACTIVATIONCODE12353
61007771,8948010000042217624,260010191724650,14254458451,1$sm-dp-address.com$ACTIVATIONCODE12354

Once the eSIM is acquired, you can add/remove data product on that eSIM, APIs: POST "/b2b/sim/product/add" or POST "/b2b/sim/product/remove". 

Please note when adding product you need to specify which market that product is configured, but when removing product you don't need to specify the market. 

When testing with add/remove product API, please only use this testing eSIM ID: 76010106, all other eSIM id won't work. 

The following product id/market id pairs were created for testing:
842/157

844/160

845/161

846/162

851/162

852/162

847/163

856/166

867/166

871/166

857/167

858/167

859/167

868/168

869/168

870/168







    



