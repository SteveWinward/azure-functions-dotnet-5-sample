# Azure Functions dotnet 5 Sample Project
Sample GitHub Actions CI/CD Pipeline for Azure Function .NET 5 Isolated Process

## Setup Notes

1. Clone this repo
2. Create an Azure Function resource in your own Azure subscription
3. Create an AAD Service Principal that has contribute permissions to the Azure Function resource

```
az ad sp create-for-rbac --name "dotnet5-test-app-sp" --sdk-auth --role contributor --scopes /subscriptions/<SUBSCRIPTION_GUID>/resourcegroups/<RESOURCE_GROUP>/providers/Microsoft.Web/sites/<FUNCTION_APP_NAME>
```
4. Save the output of the operation and save that to a GitHub Action Secret with the name ```AZURE_CREDS_FUNCTION_APP```
5. Update the ```dotnet.yml``` file to specify the actual Azure Function resource name you created previously

```yaml
env:
  AZURE_FUNCTIONAPP_NAME: <ACTUAL_FUNCTION_RESOURCE_NAME> # set this to the name of your azure function app resource
  AZURE_FUNCTION_PROJ_PATH: src/Sample.FunctionApp  # set this to the path to your function app project
  ROOT_SOLUTION_PATH: src # set this to the root path of your solution/project file
```
