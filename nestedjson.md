in the resources section


### The nested template is in the json
```
 "resources": [
        {
            "type": "Microsoft.Resources/deployments",
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "properties": {
                "expressionEvaluationOptions": {
                    "scope": "inner"
                },
                "mode": "Incremental",
                "parameters": {
                    "parentVariable": {
                        "value": "[variables('exampleVariable')]"
                    }
                },
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {
                        "parentVariable": {
                            "type": "string"
                        }
                    },
                    "variables": {
                        "exampleVariable": "NESTED variable"
                    },
                    "resources": [

                    ],
                    "outputs": {
                        "resultVarNested": {
                            "type": "string",
                            "value": "[variables('exampleVariable')]"
                        },
                        "resultVarParent": {
                            "type": "string",
                            "value": "[parameters('parentVariable')]"
                        }
                    }
                }
            }
        }
    ],```

### The template is linked

```
    {
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2020-10-01",
      "name": "[format('create-{0}-{1}', parameters('tfStorageContainerName'), parameters('utcValue'))]",
      "resourceGroup": "[parameters('resourceGroupName')]",
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[concat(variables('deploymentUrlBase'),'storage-blob-container.json')]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('tfStorageAccountName')]"
          },
          "storageContainerName": {
            "value": "[parameters('tfStorageContainerName')]"
          }
        }
      },
      "dependsOn": [
        "[format('create-{0}-{1}', parameters('tfStorageAccountName'), parameters('utcValue'))]"
      ]
    },
    ```