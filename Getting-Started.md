 
## Why the need of a Pipeline

Azure Cost Insights uses an Azure DevOps Pipeline to download and prepare your cost-data. There are a couple of reasons for this. 
- **Security Context**
  
   We need an identity / security context to access Azure's Cost Apis' It is not possible to use 'Service Connections' in a Widget. We want to avoid the need for an additional principal. Using Azure Pipelines we can use the Azure Service Connection which in most cases already exists.

- **Performance**

   The cost api's are slow, very slow. The widget need to load instantly and downloading weeks of cost data can take minutes.

- **Complexity**
   
   There is no 1 simple cost api that works for everyone. There are things like rate cards, the old and the new api, etc. In the build pipeline all this logic is implemented and the output is a simple format which is the same for everyone.  

- **Storage**

   Your processed cost data is stored as a build artifact. This way there is no need for an external service/storage. The Widget has access to these build artifacts and can use this (widget optimised) cost dataset. 
 
## Subscription Types

There are a lot of different Subscription types ([OfferID's](https://azure.microsoft.com/en-us/support/legal/offer-details/)). Each Offer has it's own cost structure and this is reflected in the API's. There are multiple API's, 'Azure Cost Insights' tries to hide this complexity as much as possible. However, in some cases some user input is required.

In the 'Download Cost Data' you have to choose which API to use. For the majority of the offers the 'Consumption' is the best option because this is the [new unified api](https://azure.microsoft.com/nl-nl/blog/azure-consumption-usage-details-api/). For some offer types (Like EA & CSP) select the 'Usage' Api. If you're not sure, start the pipeline with the Consumption Api, it will tell if you have to switch. 

When you select the 'Usage' Api you have to provide some additional data:

- OfferId, this can be found on the overview pane of the Subscription in the Azure Portal. If not, try to find it [here](https://azure.microsoft.com/en-us/support/legal/offer-details/)

- Currency & locale documented [here](https://docs.microsoft.com/en-us/previous-versions/azure/reference/mt219004(v%3dazure.100)

- Regio Info, set to the 2 letter ISO code where the offer was purchased. Find your locale [here](https://account.windowsazure.com/Profile).  