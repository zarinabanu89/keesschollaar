This extension will never send any of your cost data to any remote endpoint. So things like Azure Data (Subscription/Resource-Group/Tags), Cost data or identities/tokens never leave your Azure DevOps tenant! 

Some telemetry data is collected to make this a better product. The 'Download Cost Data' and 'Publish Cost Data' tasks send a request to Application Insights containing the duration of the task and the version of the task. 
Both the Widget and the Widget-Configuration-panel will send a 'PageView' request to Application Insights containing the configuration of that widget (grouped by, period, etc.). 
The Widget and the Configuration-panel use https://license.prd.azurecostinsights.com to validate the license, this request only contains your tenant ID (a guid) and the ID of that widget (a random number).

Only when you create a subscription:

When creating a subscription the data entered in the form (email, company name, quantity, currency) is send to the api mentioned above. The Credit Card details and payments are processed by Stripe.com (a widely used service, [more info here](https://stripe.com/docs/security/stripe)). So no credit card info is send to this api. 

