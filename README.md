# bot-basic-tutorial
Build a simple bot using Azure Bot Framework SDK with Python

## To create your bot run
`cookiecutter https://github.com/microsoft/botbuilder-python/releases/download/Templates/echo.zip`

## Deploy

### Login in Azure Portal
`az login`

### Set the subscription
`az account set --subscription "<YOUR_SUBSCRIPTION>"`

### Create an App registration
It will returns a json with `appId` key. Please save this value to be used for in the deployment.
`az ad app create --display-name "echo-chat-bot" --password "<YOUR_APP_PASSWORD>" --available-to-other-tenants`

### Deploy via ARM template with new Resource Group
