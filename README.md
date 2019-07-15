
2)Avoid setting debug logs/ debug monitoring unless required.
Since both the process execution and logging happen in the same thread be careful when setting debug levels at Extrafine, this can cause CPU timeout to occur.

3) Leverage standard API(s) as much as you can instead of doing the heavy lifting and updating quote/quote lines manually.

For my use case I had to leverage Amender API via the service router class in CPQ and then modify the QLIS created on the amended quote since our business need was to modify the QLIS based on an incoming payload.

https://developer.salesforce.com/docs/atlas.en-us.cpq_dev_api.meta/cpq_dev_api/cpq_api_contract_amender.htm
