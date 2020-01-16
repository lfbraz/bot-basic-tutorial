# bot-basic-tutorial
Build a simple bot using Azure Bot Framework SDK with Python.

## Create your Bot
We will use an echo template from **[cookiecutter](https://cookiecutter.readthedocs.io/)** to be able
to create a simple ChatBot using **Azure Bot Framework SDK**.

An description of this template can be found in this [link](https://marketplace.visualstudio.com/items?itemName=BotBuilder.botbuilderv4).

We will use the [oficial Azure guide reference](https://docs.microsoft.com/pt-br/azure/bot-service/bot-builder-tutorial-basic-deploy?view=azure-bot-service-4.0&tabs=python%2Ccsharp)
to follow the steps to create and test the ChatBot.

Feel free to adapt using another template or to customize as you want :)
`cookiecutter https://github.com/microsoft/botbuilder-python/releases/download/Templates/echo.zip`

## Deploy
Here we will use [azcli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
to be able to set the configurations required.

### Login in Azure Portal
`az login`
It will open your browser asking for your credentials. Please login with your Azure Account.

### Set the subscription
`az account set --subscription "<YOUR_SUBSCRIPTION>"`
Get the Subscription ID from the Azure portal or using the command `az account list`

### Create an App registration
`az ad app create --display-name "<YOUR_DISPLAY_NAME>" --password "<YOUR_APP_PASSWORD>" --available-to-other-tenants`
Register your App to be able to authenticate users and request access to user resources.
It will returns a json with an `appId` key. Please save this value to be used in the deployment.

### Deploy via ARM template with new Resource Group
```
az deployment create --name "<YOUR_DEPLOYMENT_NAME>" \
--template-file "<PATH_OF_JSON_TEMPLATE_FILE>" \
--location "<LOCATION_NAME>" \
--parameters appId="<YOUR_APPID>" \
appSecret="<YOUR_APP_PASSWORD>" \
botId="<UNIQUE_GLOBAL_APP_ID>" \
botSku=<S1 OR F0> \
newAppServicePlanName="<APP_SERVICE_PLAN_NAME>" \
newWebAppName="<WEB_APP_NAME>" \
groupName="<RESOURCE_GROUP_NAME>" \
groupLocation="<LOCATION_NAME>" \
newAppServicePlanLocation="<LOCATION_NAME>"
```

### Deploy code to Azure
First zip all the files inside your bot directory (the folder of `app.py` file).
Pass this .zip to `--src` parameter of the code bellow:

`az webapp deployment source config-zip --resource-group "<resource-group-name>" --name "<name-of-web-app>" --src "code.zip"`
