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

Highland Solutions LLC provides some default data products, the following list contains default products a partner may start using immediately:

```json
{
  "status": "success",
  "product_list": [
    {
      "id": "842",
      "name": "China-10MB/90days",
      "description": "★★★ China-10MB/90days ★★★\n==============================\n* This package has a maximum usage of 10MB days\n* Valid for 90 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage:【China】",
      "useAreaId": "157",
      "type": "DataPlan",
      "market_name": "China",
      "market_area": "China(76)",
      "market_country_code": "460",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:30.462721"
    },
    {
      "id": "844",
      "name": "Australia & Malaysia & Taiwan & Singapore-100GB/1800days",
      "description": "★★★ Australia & Malaysia & Taiwan & Singapore -100GB/1800days ★★★\n==============================\n* This package has a maximum usage of 100GB days\n* Valid for 1800 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: Australia & Malaysia & Taiwan & Singapore",
      "useAreaId": "160",
      "type": "DataPlan",
      "market_name": "Australia & Malaysia & Taiwan & Singapore",
      "market_area": "(76)Australia,Malaysia,Taiwan,Singapore",
      "market_country_code": "460",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:31.708084"
    },
    {
      "id": "845",
      "name": "Canada -100GB/1800days",
      "description": "★★★ Canada -100GB/1800days ★★★\n==============================\n* This package has a maximum usage of 100GB days\n* Valid for 1800 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: Canada",
      "useAreaId": "161",
      "type": "DataPlan",
      "market_name": "Canada",
      "market_area": "Canada(76)",
      "market_country_code": "460",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:32.821847"
    },
    {
      "id": "846",
      "name": "USA -50GB/30days",
      "description": "★★★ USA -50GB/30days ★★★\n==============================\n* This package has a maximum usage of 50GB days\n* Valid for 30 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: USA",
      "useAreaId": "162",
      "type": "DataPlan",
      "market_name": "USA",
      "market_area": "USA(76)",
      "market_country_code": "310,311",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:33.939373"
    },
    {
      "id": "851",
      "name": "USA -1GB/7days",
      "description": "★★★ USA -1GB/7days ★★★\n==============================\n* This package has a maximum usage of 1 GB days\n* Valid for 7 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: USA",
      "useAreaId": "162",
      "type": "DataPlan",
      "market_name": "USA",
      "market_area": "USA(76)",
      "market_country_code": "310,311",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:34.008587"
    },
    {
      "id": "852",
      "name": "USA-5GB/30days",
      "description": "★★★ USA-5GB/30days ★★★\n==============================\n* This package has a maximum usage of 5 GB days\n* Valid for 30 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: USA",
      "useAreaId": "162",
      "type": "DataPlan",
      "market_name": "USA",
      "market_area": "USA(76)",
      "market_country_code": "310,311",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:34.069102"
    },
    {
      "id": "847",
      "name": "New Zealand -100GB/1800days",
      "description": "★★★ New Zealand -100GB/1800days ★★★\n==============================\n* This package has a maximum usage of 100GB\n* Valid for 1800 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: New Zealand",
      "useAreaId": "163",
      "type": "DataPlan",
      "market_name": "New Zealand",
      "market_area": "New Zealand(76)",
      "market_country_code": "460",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:35.179835"
    },
    {
      "id": "856",
      "name": "Asia Pacific 24 Countries-360MB/365days",
      "description": "★★★ Asia Pacific 24 Countries-360MB/365days ★★★\n==============================\n* This package has a maximum usage of 360MB\n* Valid for 365 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: Australia/Bangladesh/Cambodia/China/Hong Kong/India/Indonesia/Israel/Japan/Kazakhstan/Kyrgyzstan/Laos/Macao China/Malaysia/New Zealand/Pakistan/Philippines/Singapore/South Korea/Sri Lanka/Taiwan/Thailand/Uzbekistan/Vietnam",
      "useAreaId": "166",
      "type": "DataPlan",
      "market_name": "Asia Pacific-24 countries",
      "market_area": "Asia Pacific-24 countries(76)",
      "market_country_code": "460",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:36.439670"
    },
    {
      "id": "867",
      "name": "Asia Pacific 24 Countries-10GB/60days",
      "description": "★★★ Asia Pacific 24 Countries-10GB/60days ★★★\n==============================\n* This package has a maximum usage of 10GB days\n* Valid for 60 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: Australia/Bangladesh/Cambodia/China/Hong Kong/India/Indonesia/Israel/Japan/Kazakhstan/Kyrgyzstan/Laos/Macao China/Malaysia/New Zealand/Pakistan/Philippines/Singapore/South Korea/Sri Lanka/Taiwan/Thailand/Uzbekistan/Vietnam",
      "useAreaId": "166",
      "type": "DataPlan",
      "market_name": "Asia Pacific-24 countries",
      "market_area": "Asia Pacific-24 countries(76)",
      "market_country_code": "460",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:36.504602"
    },
    {
      "id": "871",
      "name": "Asia Pacific 24 Countries -1200MB/365days",
      "description": "★★★ Asia Pacific 24 Countries -1200MB/365days ★★★\n==============================\n* This package has a maximum usage of 1200MB days\n* Valid for 365 days (starting from the first use package)\n* Local 3G/4G/LTE network\n* APN setting: plus\n* Coverage: Australia/Bangladesh/Cambodia/China/Hong Kong/India/Indonesia/Israel/Japan/Kazakhstan/Kyrgyzstan/Laos/Macao China/Malaysia/New Zealand/Pakistan/Philippines/Singapore/South Korea/Sri Lanka/Taiwan/Thailand/Uzbekistan/Vietnam",
      "useAreaId": "166",
      "type": "DataPlan",
      "market_name": "Asia Pacific-24 countries",
      "market_area": "Asia Pacific-24 countries(76)",
      "market_country_code": "460",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:36.564992"
    },
    {
      "id": "857",
      "name": "Multi-Countries & Regions_A11-2GB/365days",
      "description": "★★★ Multi-Countries & Regions_A11-2GB/365days ★★★\n=======================================\n* This package has a maximum usage of 2GB\n* Valid for 365 days (The time is calculated from the first connect to the network start) \n* Local 3G/4G/LTE network\n* APN setting(Manual mode):  plus\n* Coverage: Kyrgyzstan,Uzbekistan,Hong Kong,Kazakhstan,Macau,New Zealand,Pakistan,Malaysia,Russia,Armenia,Australia,Israel,Thailand,Indonesia,Reunion,Kuwait,India,Philippines,Qatar,Singapore,Sri Lanka,Azerbaijan,Bahrain,Taiwan,Tunisia,Ghana,Cambodia,Kosovo,Oman,United Arab Emirates,Bangladesh,South Korea,Vietnam,Egypt,Iraq,Saudi Arabia,Japan,Laos,China,Mongolia,Afghanistan,Nepal,Niger,Jordan,Benin,Iran,Maldives",
      "useAreaId": "167",
      "type": "DataPlan",
      "market_name": "Multi-Countries & Regions - A11",
      "market_area": "(76) Kyrgyzstan,Uzbekistan,Hong Kong,Kazakhstan,Macau,New Zealand,Pakistan,Malaysia,Russia,Armenia,Australia,Israel,Thailand,Indonesia,Reunion,Kuwait,India,Philippines,Qatar,Singapore,Sri Lanka,Azerbaijan,Bahrain,Taiwan,Tunisia,Ghana,Cambodia,Kosovo,Oman,United Arab Emirates,Bangladesh,South Korea,Vietnam,Egypt,Iraq,Saudi Arabia,Japan,Laos,China,Mongolia,Afghanistan,Nepal,Niger,Jordan,Benin,Iran,Maldives",
      "market_country_code": "All",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:37.760264"
    },
    {
      "id": "858",
      "name": "Multi-Countries & Regions_A11-200MB/30days",
      "description": "★★★ 多国家和地区_A11-200MB/30天 ★★★\n=======================================\n* This package has a maximum usage of 2GB\n* Valid for 365 days (The time is calculated from the first connect to the network start) \n* Local 3G/4G/LTE network\n* APN setting(Manual mode):  plus\n* Coverage: Kyrgyzstan,Uzbekistan,Hong Kong,Kazakhstan,Macau,New Zealand,Pakistan,Malaysia,Russia,Armenia,Australia,Israel,Thailand,Indonesia,Reunion,Kuwait,India,Philippines,Qatar,Singapore,Sri Lanka,Azerbaijan,Bahrain,Taiwan,Tunisia,Ghana,Cambodia,Kosovo,Oman,United Arab Emirates,Bangladesh,South Korea,Vietnam,Egypt,Iraq,Saudi Arabia,Japan,Laos,China,Mongolia,Afghanistan,Nepal,Niger,Jordan,Benin,Iran,Maldives",
      "useAreaId": "167",
      "type": "DataPlan",
      "market_name": "Multi-Countries & Regions - A11",
      "market_area": "(76) Kyrgyzstan,Uzbekistan,Hong Kong,Kazakhstan,Macau,New Zealand,Pakistan,Malaysia,Russia,Armenia,Australia,Israel,Thailand,Indonesia,Reunion,Kuwait,India,Philippines,Qatar,Singapore,Sri Lanka,Azerbaijan,Bahrain,Taiwan,Tunisia,Ghana,Cambodia,Kosovo,Oman,United Arab Emirates,Bangladesh,South Korea,Vietnam,Egypt,Iraq,Saudi Arabia,Japan,Laos,China,Mongolia,Afghanistan,Nepal,Niger,Jordan,Benin,Iran,Maldives",
      "market_country_code": "All",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:37.825106"
    },
    {
      "id": "859",
      "name": "Multi-Countries & Regions_A11-1GB/180days",
      "description": "★★★ Multi-Countries & Regions_A11-1GB/180days ★★★\n=======================================\n* This package has a maximum usage of 1GB\n* Valid for 180 days (The time is calculated from the first connect to the network start) \n* Local 3G/4G/LTE network\n* APN setting(Manual mode):  plus\n* Coverage: Kyrgyzstan,Uzbekistan,Hong Kong,Kazakhstan,Macau,New Zealand,Pakistan,Malaysia,Russia,Armenia,Australia,Israel,Thailand,Indonesia,Reunion,Kuwait,India,Philippines,Qatar,Singapore,Sri Lanka,Azerbaijan,Bahrain,Taiwan,Tunisia,Ghana,Cambodia,Kosovo,Oman,United Arab Emirates,Bangladesh,South Korea,Vietnam,Egypt,Iraq,Saudi Arabia,Japan,Laos,China,Mongolia,Afghanistan,Nepal,Niger,Jordan,Benin,Iran,Maldives",
      "useAreaId": "167",
      "type": "DataPlan",
      "market_name": "Multi-Countries & Regions - A11",
      "market_area": "(76) Kyrgyzstan,Uzbekistan,Hong Kong,Kazakhstan,Macau,New Zealand,Pakistan,Malaysia,Russia,Armenia,Australia,Israel,Thailand,Indonesia,Reunion,Kuwait,India,Philippines,Qatar,Singapore,Sri Lanka,Azerbaijan,Bahrain,Taiwan,Tunisia,Ghana,Cambodia,Kosovo,Oman,United Arab Emirates,Bangladesh,South Korea,Vietnam,Egypt,Iraq,Saudi Arabia,Japan,Laos,China,Mongolia,Afghanistan,Nepal,Niger,Jordan,Benin,Iran,Maldives",
      "market_country_code": "All",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:37.890192"
    },
    {
      "id": "868",
      "name": "Global 163 Countries & Regions_2GB/365days",
      "description": "★★★ Global 163 Countries & Regions_2GB/365days ★★★\n=======================================\n* This package has a maximum usage of 2GB\n* Valid for 365 days (The time is calculated from the first connect to the network start) \n* Local 3G/4G/LTE network\n* APN setting(Manual mode):  plus\n* Coverage: (76) Ukraine, Slovakia, Liechtenstein, Poland, Finland, Kyrgyzstan, Romania, Lithuania, Kazakhstan, Uzbekistan, Germany, Netherlands, Cyprus, Greece, United Kingdom, Norway, France, Spain, Montenegro, Pakistan, Albania, Belgium, Czech Republic, Moldova, Croatia, Hungary, Estonia, Hong Kong, Macao China, Austria, Portugal, Luxembourg, Turkey, Bulgaria, Sweden, Italy, Vatican City, Slovenia, Malta, Serbia, Denmark, Ireland, Israel, Switzerland, Bangladesh, Latvia, New Zealand, Malaysia, Russian Federation, Armenia, Iceland, Thailand, Australia, Indonesia, Reunion, Algeria, Kuwait, United States, Sri Lanka, Georgia, Philippines, Tunisia, Belarus, Bosnia and Herzegovina, India, Qatar, Singapore, Faroe Islands, Taiwan, Macedonia, Bahrain, Azerbaijan, South Korea, Ghana, Kosovo, Tajikistan, Oman, Brazil, Andorra, Vietnam, Cambodia, Isle of Man, Guernsey, Jersey, Argentia, Japan, Saudi Arabia, Ecuador, Costa Rica, Uruguay, Chile, Gibraltar, Peru, Mexico, Canada, Iraq, Egypt, French Guiana, China, Laos, Nigeria, Morocco, Madagascar, United Arab Emirates, Tanzania, Kenya, Samoa, Zambia, Uganda, South Africa, Congo Dem. Rep, Gabon, Malawi, Chad, Congo Republic, Paraguay, Afghanistan, Nepal, Colombia, Netherlands Antilles, Guadeloupe, Mongolia, Montserrat, Panama, Jamaica, Niger, Mauritius, El Salvador, Barbados, Antigua and Barbuda, Dominica, Jordan, Anguilla, Cayman Islands, Grenada, Saint Kitts and Nevis, Saint Lucia, Saint Vincent and Grenadines, British Virgin Islands, Benin, Turks and Caicos Islands, Rwanda, Honduras, Bolivia, Dominican Republic, Nicaragua, Iran, Guatemala, Bahamas, Maldives, Venezuela, Senegal, Cape Verde, Palestinian Territory, Sudan, Belize, Trinidad and Tobago, Mozambique, Curacao, French Polynesia, Suriname, Guyana, Bermuda",
      "useAreaId": "168",
      "type": "DataPlan",
      "market_name": "Global 163 Countries & Regions",
      "market_area": "(76) Ukraine, Slovakia, Liechtenstein, Poland, Finland, Kyrgyzstan, Romania, Lithuania, Kazakhstan, Uzbekistan, Germany, Netherlands, Cyprus, Greece, United Kingdom, Norway, France, Spain, Montenegro, Pakistan, Albania, Belgium, Czech Republic, Moldova, Croatia, Hungary, Estonia, Hong Kong, Macao China, Austria, Portugal, Luxembourg, Turkey, Bulgaria, Sweden, Italy, Vatican City, Slovenia, Malta, Serbia, Denmark, Ireland, Israel, Switzerland, Bangladesh, Latvia, New Zealand, Malaysia, Russian Federation, Armenia, Iceland, Thailand, Australia, Indonesia, Reunion, Algeria, Kuwait, United States, Sri Lanka, Georgia, Philippines, Tunisia, Belarus, Bosnia and Herzegovina, India, Qatar, Singapore, Faroe Islands, Taiwan, Macedonia, Bahrain, Azerbaijan, South Korea, Ghana, Kosovo, Tajikistan, Oman, Brazil, Andorra, Vietnam, Cambodia, Isle of Man, Guernsey, Jersey, Argentia, Japan, Saudi Arabia, Ecuador, Costa Rica, Uruguay, Chile, Gibraltar, Peru, Mexico, Canada, Iraq, Egypt, French Guiana, China, Laos, Nigeria, Morocco, Madagascar, United Arab Emirates, Tanzania, Kenya, Samoa, Zambia, Uganda, South Africa, Congo Dem. Rep, Gabon, Malawi, Chad, Congo Republic, Paraguay, Afghanistan, Nepal, Colombia, Netherlands Antilles, Guadeloupe, Mongolia, Montserrat, Panama, Jamaica, Niger, Mauritius, El Salvador, Barbados, Antigua and Barbuda, Dominica, Jordan, Anguilla, Cayman Islands, Grenada, Saint Kitts and Nevis, Saint Lucia, Saint Vincent and Grenadines, British Virgin Islands, Benin, Turks and Caicos Islands, Rwanda, Honduras, Bolivia, Dominican Republic, Nicaragua, Iran, Guatemala, Bahamas, Maldives, Venezuela, Senegal, Cape Verde, Palestinian Territory, Sudan, Belize, Trinidad and Tobago, Mozambique, Curacao, French Polynesia, Suriname, Guyana, Bermuda",
      "market_country_code": "All",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:39.017925"
    },
    {
      "id": "869",
      "name": "Global 163 Countries & Regions_1GB/180days",
      "description": "★★★ Global 163 Countries & Regions_1GB/180days ★★★\n=======================================\n* This package has a maximum usage of 1GB\n* Valid for 180 days (The time is calculated from the first connect to the network start) \n* Local 3G/4G/LTE network\n* APN setting(Manual mode):  plus\n* Coverage: (76) Ukraine, Slovakia, Liechtenstein, Poland, Finland, Kyrgyzstan, Romania, Lithuania, Kazakhstan, Uzbekistan, Germany, Netherlands, Cyprus, Greece, United Kingdom, Norway, France, Spain, Montenegro, Pakistan, Albania, Belgium, Czech Republic, Moldova, Croatia, Hungary, Estonia, Hong Kong, Macao China, Austria, Portugal, Luxembourg, Turkey, Bulgaria, Sweden, Italy, Vatican City, Slovenia, Malta, Serbia, Denmark, Ireland, Israel, Switzerland, Bangladesh, Latvia, New Zealand, Malaysia, Russian Federation, Armenia, Iceland, Thailand, Australia, Indonesia, Reunion, Algeria, Kuwait, United States, Sri Lanka, Georgia, Philippines, Tunisia, Belarus, Bosnia and Herzegovina, India, Qatar, Singapore, Faroe Islands, Taiwan, Macedonia, Bahrain, Azerbaijan, South Korea, Ghana, Kosovo, Tajikistan, Oman, Brazil, Andorra, Vietnam, Cambodia, Isle of Man, Guernsey, Jersey, Argentia, Japan, Saudi Arabia, Ecuador, Costa Rica, Uruguay, Chile, Gibraltar, Peru, Mexico, Canada, Iraq, Egypt, French Guiana, China, Laos, Nigeria, Morocco, Madagascar, United Arab Emirates, Tanzania, Kenya, Samoa, Zambia, Uganda, South Africa, Congo Dem. Rep, Gabon, Malawi, Chad, Congo Republic, Paraguay, Afghanistan, Nepal, Colombia, Netherlands Antilles, Guadeloupe, Mongolia, Montserrat, Panama, Jamaica, Niger, Mauritius, El Salvador, Barbados, Antigua and Barbuda, Dominica, Jordan, Anguilla, Cayman Islands, Grenada, Saint Kitts and Nevis, Saint Lucia, Saint Vincent and Grenadines, British Virgin Islands, Benin, Turks and Caicos Islands, Rwanda, Honduras, Bolivia, Dominican Republic, Nicaragua, Iran, Guatemala, Bahamas, Maldives, Venezuela, Senegal, Cape Verde, Palestinian Territory, Sudan, Belize, Trinidad and Tobago, Mozambique, Curacao, French Polynesia, Suriname, Guyana, Bermuda",
      "useAreaId": "168",
      "type": "DataPlan",
      "market_name": "Global 163 Countries & Regions",
      "market_area": "(76) Ukraine, Slovakia, Liechtenstein, Poland, Finland, Kyrgyzstan, Romania, Lithuania, Kazakhstan, Uzbekistan, Germany, Netherlands, Cyprus, Greece, United Kingdom, Norway, France, Spain, Montenegro, Pakistan, Albania, Belgium, Czech Republic, Moldova, Croatia, Hungary, Estonia, Hong Kong, Macao China, Austria, Portugal, Luxembourg, Turkey, Bulgaria, Sweden, Italy, Vatican City, Slovenia, Malta, Serbia, Denmark, Ireland, Israel, Switzerland, Bangladesh, Latvia, New Zealand, Malaysia, Russian Federation, Armenia, Iceland, Thailand, Australia, Indonesia, Reunion, Algeria, Kuwait, United States, Sri Lanka, Georgia, Philippines, Tunisia, Belarus, Bosnia and Herzegovina, India, Qatar, Singapore, Faroe Islands, Taiwan, Macedonia, Bahrain, Azerbaijan, South Korea, Ghana, Kosovo, Tajikistan, Oman, Brazil, Andorra, Vietnam, Cambodia, Isle of Man, Guernsey, Jersey, Argentia, Japan, Saudi Arabia, Ecuador, Costa Rica, Uruguay, Chile, Gibraltar, Peru, Mexico, Canada, Iraq, Egypt, French Guiana, China, Laos, Nigeria, Morocco, Madagascar, United Arab Emirates, Tanzania, Kenya, Samoa, Zambia, Uganda, South Africa, Congo Dem. Rep, Gabon, Malawi, Chad, Congo Republic, Paraguay, Afghanistan, Nepal, Colombia, Netherlands Antilles, Guadeloupe, Mongolia, Montserrat, Panama, Jamaica, Niger, Mauritius, El Salvador, Barbados, Antigua and Barbuda, Dominica, Jordan, Anguilla, Cayman Islands, Grenada, Saint Kitts and Nevis, Saint Lucia, Saint Vincent and Grenadines, British Virgin Islands, Benin, Turks and Caicos Islands, Rwanda, Honduras, Bolivia, Dominican Republic, Nicaragua, Iran, Guatemala, Bahamas, Maldives, Venezuela, Senegal, Cape Verde, Palestinian Territory, Sudan, Belize, Trinidad and Tobago, Mozambique, Curacao, French Polynesia, Suriname, Guyana, Bermuda",
      "market_country_code": "All",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:39.124853"
    },
    {
      "id": "870",
      "name": "Global 163 Countries & Regions_200MB/30days",
      "description": "★★★ Global 163 Countries & Regions_200MB/30days ★★★\n=======================================\n* This package has a maximum usage of 200MB\n* Valid for 30 days (The time is calculated from the first connect to the network start) \n* Local 3G/4G/LTE network\n* APN setting(Manual mode):  plus\n* Coverage: (76) Ukraine, Slovakia, Liechtenstein, Poland, Finland, Kyrgyzstan, Romania, Lithuania, Kazakhstan, Uzbekistan, Germany, Netherlands, Cyprus, Greece, United Kingdom, Norway, France, Spain, Montenegro, Pakistan, Albania, Belgium, Czech Republic, Moldova, Croatia, Hungary, Estonia, Hong Kong, Macao China, Austria, Portugal, Luxembourg, Turkey, Bulgaria, Sweden, Italy, Vatican City, Slovenia, Malta, Serbia, Denmark, Ireland, Israel, Switzerland, Bangladesh, Latvia, New Zealand, Malaysia, Russian Federation, Armenia, Iceland, Thailand, Australia, Indonesia, Reunion, Algeria, Kuwait, United States, Sri Lanka, Georgia, Philippines, Tunisia, Belarus, Bosnia and Herzegovina, India, Qatar, Singapore, Faroe Islands, Taiwan, Macedonia, Bahrain, Azerbaijan, South Korea, Ghana, Kosovo, Tajikistan, Oman, Brazil, Andorra, Vietnam, Cambodia, Isle of Man, Guernsey, Jersey, Argentia, Japan, Saudi Arabia, Ecuador, Costa Rica, Uruguay, Chile, Gibraltar, Peru, Mexico, Canada, Iraq, Egypt, French Guiana, China, Laos, Nigeria, Morocco, Madagascar, United Arab Emirates, Tanzania, Kenya, Samoa, Zambia, Uganda, South Africa, Congo Dem. Rep, Gabon, Malawi, Chad, Congo Republic, Paraguay, Afghanistan, Nepal, Colombia, Netherlands Antilles, Guadeloupe, Mongolia, Montserrat, Panama, Jamaica, Niger, Mauritius, El Salvador, Barbados, Antigua and Barbuda, Dominica, Jordan, Anguilla, Cayman Islands, Grenada, Saint Kitts and Nevis, Saint Lucia, Saint Vincent and Grenadines, British Virgin Islands, Benin, Turks and Caicos Islands, Rwanda, Honduras, Bolivia, Dominican Republic, Nicaragua, Iran, Guatemala, Bahamas, Maldives, Venezuela, Senegal, Cape Verde, Palestinian Territory, Sudan, Belize, Trinidad and Tobago, Mozambique, Curacao, French Polynesia, Suriname, Guyana, Bermuda",
      "useAreaId": "168",
      "type": "DataPlan",
      "market_name": "Global 163 Countries & Regions",
      "market_area": "(76) Ukraine, Slovakia, Liechtenstein, Poland, Finland, Kyrgyzstan, Romania, Lithuania, Kazakhstan, Uzbekistan, Germany, Netherlands, Cyprus, Greece, United Kingdom, Norway, France, Spain, Montenegro, Pakistan, Albania, Belgium, Czech Republic, Moldova, Croatia, Hungary, Estonia, Hong Kong, Macao China, Austria, Portugal, Luxembourg, Turkey, Bulgaria, Sweden, Italy, Vatican City, Slovenia, Malta, Serbia, Denmark, Ireland, Israel, Switzerland, Bangladesh, Latvia, New Zealand, Malaysia, Russian Federation, Armenia, Iceland, Thailand, Australia, Indonesia, Reunion, Algeria, Kuwait, United States, Sri Lanka, Georgia, Philippines, Tunisia, Belarus, Bosnia and Herzegovina, India, Qatar, Singapore, Faroe Islands, Taiwan, Macedonia, Bahrain, Azerbaijan, South Korea, Ghana, Kosovo, Tajikistan, Oman, Brazil, Andorra, Vietnam, Cambodia, Isle of Man, Guernsey, Jersey, Argentia, Japan, Saudi Arabia, Ecuador, Costa Rica, Uruguay, Chile, Gibraltar, Peru, Mexico, Canada, Iraq, Egypt, French Guiana, China, Laos, Nigeria, Morocco, Madagascar, United Arab Emirates, Tanzania, Kenya, Samoa, Zambia, Uganda, South Africa, Congo Dem. Rep, Gabon, Malawi, Chad, Congo Republic, Paraguay, Afghanistan, Nepal, Colombia, Netherlands Antilles, Guadeloupe, Mongolia, Montserrat, Panama, Jamaica, Niger, Mauritius, El Salvador, Barbados, Antigua and Barbuda, Dominica, Jordan, Anguilla, Cayman Islands, Grenada, Saint Kitts and Nevis, Saint Lucia, Saint Vincent and Grenadines, British Virgin Islands, Benin, Turks and Caicos Islands, Rwanda, Honduras, Bolivia, Dominican Republic, Nicaragua, Iran, Guatemala, Bahamas, Maldives, Venezuela, Senegal, Cape Verde, Palestinian Territory, Sudan, Belize, Trinidad and Tobago, Mozambique, Curacao, French Polynesia, Suriname, Guyana, Bermuda",
      "market_country_code": "All",
      "company_id": "4345d86fbf8a11f09f474c50dd6c0d86",
      "company_name": "Highland Solutions LLC",
      "last_updated": "2026-01-01T19:49:39.234122"
    }
  ]
}
```




    



