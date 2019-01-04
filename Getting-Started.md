Azure Cost Insights uses an Azure DevOps Pipeline to download and prepare your cost-data. There are a couple of reasons for this. 
- **Security Context**
  
   We need an identity / security context to access Azure's Cost Apis' It is not possible to use 'Service Connections' in a Widget. We want to avoid the need for an additional principal. Using Azure Pipelines we can use the Azure Service Connection which in most cases already exists.

- **Performance**

   The cost api's are slow, very slow. The widget need to load instantly and downloading weeks of cost data can take minutes.

- **Complexity**
   
   There is no 1 simple cost api that works for everyone. There are things like rate cards, the old and the new api, etc. In the build pipeline all this logic is implemented and the output is a simple format which is the same for everyone.  

- **Storage**

   Your processed cost data is stored as a build artifact. This way there is no need for an external service/storage. The Widget has access to these build artifacts and can use this (widget optimised) cost dataset. 
 