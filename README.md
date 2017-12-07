# publicIPAddresses
Reference deployment
```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "StorageAccountName": {
      "type": "string",
      "defaultValue": ""
    },
    "ContainerName": {
      "type": "string",
      "defaultValue": ""
    },
    "SasToken": {
      "type": "string",
      "defaultValue": ""
    }
  },
  "variables": {
    "publicIpAddressUri": "[concat('https://',parameters('StorageAccountName'),'.blob.core.windows.net/',parameters('ContainerName'),'/Microsoft.Network','/publicIpAddresses')]"
  },
  "resources": [
    {
      "name": "DeployPublicIpAddress",
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2016-09-01",
      "dependsOn": [ ],
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[concat(variables('publicIpAddressUri'), '/publicIpAddresses.json', parameters('SasToken'))]",
          "contentVersion": "2017.09.01.0"
        },
        "parameters": {
          "name": {
            "value": ""
          },
          "domainNameLabel": {
            "value": null
          },
          "idleTimeoutInMinutes": {
            "value": 4
          },
          "publicIPAddressVersion": {
            "value": "IPv4"
          },
          "publicIPAllocationMethod": {
            "value": "Dynamic"
          },
          "sku": {
            "value": "Basic"
          }
        }
      }
    }
  ],
  "outputs": {
  "publicIpAddresses": {
      "type": "object",
      "value": "[reference('DeployPublicIpAddress').outputs.publicIpAddresses.value]"
    }
  }
}
```
