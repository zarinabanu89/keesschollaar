If you want your 'Azure Cost Insights pipeline definition in code , this is fully supported.

An example of this pipeline can be found [here](https://github.com/keesschollaart81/AzureCostInsights.Marketplace/blob/master/azure-pipelines-example.yml).

``` YAML
trigger: none
pr: none

jobs:
- job: "Azure_Cost_Insights"
  timeoutInMinutes: 120 # A bit longer, for the bigger customers
  pool: "Hosted Ubuntu 1604" # The other ones will do, this one is fastest

  steps:
  
  - task: keesschollaart.AzureCostInsights-Dev.AzureCostInsightsWidget.DownloadTask.DownloadCostData@1
    displayName: 'Download Cost Data - Subscription 1'
    inputs:
      ConnectedServiceNameARM: '86af7676-6a6f-aaaa-9fea-538d6b69d1ca' 
      apiToUse: usage
      currency: USD
      locale: 'en-US'
      regioInfo: US

  - task: keesschollaart.AzureCostInsights-Dev.AzureCostInsightsWidget.DownloadTask.DownloadCostData@1
    displayName: 'Download Cost Data - Second Subscription'
    inputs:
      ConnectedServiceNameARM: 'e5834a49-9dd8-aaaa-8dda-df2d20501da0'
  
  - task: keesschollaart.AzureCostInsights-Dev.AzureCostInsightsWidget.PublishTask.PublishCostData@1
    displayName: 'Publish Cost Data'
    continueOnError: true ## sometimes this task fails (outside our code stack) with a system error that is not important
```

# Schedule
The Azure Cost Insights pipeline typically runs scheduled, this is not yet supported in YAML pipelines:

https://docs.microsoft.com/en-us/azure/devops/pipelines/build/triggers?view=vsts&tabs=yaml#scheduled

Therefor make sure to set the schedule in the designer view of this pipeline (don't forget to **un**check the 'Only schedule builds if the source or pipeline has changed' checkbox)

# Service Connection
The Azure Service Connection's are referenced by their Guid. This Guid can be found in the Project Settings:

```https://<<yourtenant>>.visualstudio.com/<<yourproject>>/_settings/adminservices```

Open the Service Connection and find the Guid in the url (the resourceId query string parameter).

For the first run, the pipeline needs to be authorized to use this Service Connection. To do this, try to queue the pipeline, a warning will show up with a button to Authorize. Otherwise, checkout [this page](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/resources?view=vsts#troubleshooting-authorization-for-a-yaml-pipeline).  
