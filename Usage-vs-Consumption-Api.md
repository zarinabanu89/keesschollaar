There are a lot of different Azure Subscription types ([OfferID's](https://azure.microsoft.com/en-us/support/legal/offer-details/)). Each Offer has it's own cost structure and this is reflected in the API's. There are multiple API's, 'Azure Cost Insights' tries to hide this complexity as much as possible. However, in some cases some user input is required.

In the 'Download Cost Data' you have to choose which API to use. For the majority of the offers the 'Consumption' is the best option because this is the [new unified api](https://azure.microsoft.com/nl-nl/blog/azure-consumption-usage-details-api/). For some offer types (Like EA & CSP) select the 'Usage' Api. If you're not sure, start the pipeline with the Consumption Api, it will tell if you have to switch. 

When you select the 'Usage' Api you have to provide some additional data:

- OfferId, this can be found on the overview pane of the Subscription in the Azure Portal. If not, try to find it [here](https://azure.microsoft.com/en-us/support/legal/offer-details/)

- Currency & locale documented [here](https://docs.microsoft.com/en-us/previous-versions/azure/reference/mt219004(v%3dazure.100)

- Regio Info, set to the 2 letter ISO code where the offer was purchased. Find your locale [here](https://account.windowsazure.com/Profile).  