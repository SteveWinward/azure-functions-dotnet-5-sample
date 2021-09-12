# Azure Functions dotnet 5 Sample Project
Sample GitHub Actions CI/CD Pipeline for Azure Function .NET 5 Isolated Process

## Setup Notes

1. Clone/fork this repo
2. Create a local file in the root of the Sample.FunctionApp project local.settings.json. There is a .gitignore setting to not check this file into source code. 
3. Create an Azure Function resource in your own Azure subscription
4. Create an AAD Service Principal that has contribute permissions to the Azure Function resource. Easiest way to do this is to launch the [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview) in the Azure Portal

```
az ad sp create-for-rbac --name "<FUNCTION_APP_NAME>-sp" --sdk-auth --role contributor --scopes /subscriptions/<SUBSCRIPTION_GUID>/resourcegroups/<RESOURCE_GROUP>/providers/Microsoft.Web/sites/<FUNCTION_APP_NAME>
```
5. Save the entire JSON output of the operation and save that to a [GitHub Action Secret](https://docs.github.com/en/actions/reference/encrypted-secrets) with the name ```AZURE_CREDS_FUNCTION_APP```
6. Update the ```dotnet.yml``` file to specify the actual Azure Function resource name you created previously

```yaml
env:
  AZURE_FUNCTIONAPP_NAME: <ACTUAL_FUNCTION_RESOURCE_NAME> # set this to the name of your azure function app resource
  AZURE_FUNCTION_PROJ_PATH: src/Sample.FunctionApp  # set this to the path to your function app project
  ROOT_SOLUTION_PATH: src # set this to the root path of your solution/project file
```
7. The full YAML file can be found [here](.github/workflows/dotnet.yml)
8. Kick off the GitHub Action to deploy your .NET 5 Isolated Process Azure Function App!
