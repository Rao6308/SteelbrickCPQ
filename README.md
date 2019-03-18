# SteelbrickCPQ
Tips and Tricks
1) Avoiding multiple Queueable services from getting scheduled/ avoiding CPQ triggers from getting fired multiple times and causing too many SOQL queries

When it comes to CPQ there is an useful option to turn of Quote/QLI calculation trigger if there is a scenario where the Quote/QLI(S) have to be both updated / inserted. During these times the CPQ triggers get called multiple times and schedule a heroku queueable service.

If not handled carefully this can end up causing governor issues like "Too many SOQL"/ "Too many Queuable jobs" error.

A solution / option to explore is to turn of the triggers as shown below
https://developer.salesforce.com/docs/atlas.en-us.cpq_dev_api.meta/cpq_dev_api/cpq_api_disable_apex_triggers.htm

Since I was dealing with Flows executing a huge chunk of logic, the sheer number of fast lookups were causing Too many SOQL Queries issue. One way we rearchitected was to break the flow using invocable method. Using an invocable method we ended up breaking a single flow into 2 flow there by splitting the same context into 2 different contexts and gaining back control on the process.

2)Avoid setting debug logs/ debug monitoring unless required.
Since both the process execution and logging happen in the same thread be careful when setting debug levels at Extrafine, this can cause CPU timeout to occur.

3) Leverage standard API(s) as much as you can instead of doing the heavy lifting and updating quote/quote lines manually.

For my use case I had to leverage Amender API via the service router class in CPQ and then modify the QLIS created on the amended quote since our business need was to modify the QLIS based on an incoming payload.

https://developer.salesforce.com/docs/atlas.en-us.cpq_dev_api.meta/cpq_dev_api/cpq_api_contract_amender.htm
