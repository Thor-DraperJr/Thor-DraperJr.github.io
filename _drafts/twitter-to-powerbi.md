This article will use an Azure Logic App, Azure SQL database, and Power BI to display whether or not I'm spending my time well or if I'm just spending my time.

# Introduction
I've been on a productivity kick for forever. Also, since making the jump into tech, I've used social media as a way to connect to people in the industry. I'll walk you how to quickly spin up a 

# Create SQL Database
_Basics_
**Project details**
Subscription: Azure subscription 1
	Resource Group: rg-01
**Database details**
Database name: sql-01
Server: thordraperjr-sql-server-01
	+Username: 
	+Password: 
Want to use SQL elastic pool? No
Compute + storage: Basic
**Backup storage redundancy**
Backup storage redundancy: Locally-redundant backup storage - Preview

_Networking_
**Network connectivity**
Connectivity method: No access
**Connection Policy**
Connection policy: Default
**Encrypted connections**
Minimum TLS version: TLS 1.2

_Security_
**Azure Defender for SQL**
Enable Azure Defender for SQL: []Start free trial(30 Days)[x]Not now

_Additional settings_
**Datasource**
Use existing data: None
**Database collation**
Collation: SQL_Latin_General_CP1_CI_AS
**Maintenance window**
Maintenance window: System default (5pm to 8am)

_Tags_
Development:Twitter-to-PowerBi-App

```sql
CREATE TABLE TweetData (
    CreatedAt datetime,
    TweetText varchar(512),
);
```
^Creating a table with two columns
* `Drop TABLE TweetData;` <---Delete the
* 

```sql
```

```sql
```


# Logic App

from:@Thor_DraperJr, #TimeSpent OR #TimeWellSpent


{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "workflows_twitter_to_powerBi_name": {
            "defaultValue": "twitter-to-powerBi",
            "type": "String"
        },
        "connections_sql_2_externalid": {
            "defaultValue": "/subscriptions/5c01b8b4-6642-4c2d-bb51-51e06a4f52fa/resourceGroups/rg-01/providers/Microsoft.Web/connections/sql-2",
            "type": "String"
        },
        "connections_twitter_externalid": {
            "defaultValue": "/subscriptions/5c01b8b4-6642-4c2d-bb51-51e06a4f52fa/resourceGroups/rg-01/providers/Microsoft.Web/connections/twitter",
            "type": "String"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Logic/workflows",
            "apiVersion": "2017-07-01",
            "name": "[parameters('workflows_twitter_to_powerBi_name')]",
            "location": "eastus",
            "tags": {
                "Development": "Twitter-to-PowerBi-App"
            },
            "properties": {
                "state": "Enabled",
                "definition": {
                    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {
                        "$connections": {
                            "defaultValue": {},
                            "type": "Object"
                        }
                    },
                    "triggers": {
                        "When_a_new_tweet_is_posted": {
                            "recurrence": {
                                "frequency": "Hour",
                                "interval": 1
                            },
                            "splitOn": "@triggerBody()?['value']",
                            "type": "ApiConnection",
                            "inputs": {
                                "host": {
                                    "connection": {
                                        "name": "@parameters('$connections')['twitter']['connectionId']"
                                    }
                                },
                                "method": "get",
                                "path": "/onnewtweet",
                                "queries": {
                                    "searchQuery": "from:@Thor_DraperJr, #TimeSpent OR #TimeWellSpent"
                                }
                            }
                        }
                    },
                    "actions": {
                        "Insert_row_(V2)": {
                            "runAfter": {},
                            "type": "ApiConnection",
                            "inputs": {
                                "body": {
                                    "CreatedDate": "@triggerBody()?['CreatedAtIso']",
                                    "TweetText": "@triggerBody()?['TweetText']"
                                },
                                "host": {
                                    "connection": {
                                        "name": "@parameters('$connections')['sql_1']['connectionId']"
                                    }
                                },
                                "method": "post",
                                "path": "/v2/datasets/@{encodeURIComponent(encodeURIComponent('default'))},@{encodeURIComponent(encodeURIComponent('default'))}/tables/@{encodeURIComponent(encodeURIComponent('[dbo].[TweetData]'))}/items"
                            }
                        }
                    },
                    "outputs": {}
                },
                "parameters": {
                    "$connections": {
                        "value": {
                            "sql_1": {
                                "connectionId": "[parameters('connections_sql_2_externalid')]",
                                "connectionName": "sql-2",
                                "id": "/subscriptions/5c01b8b4-6642-4c2d-bb51-51e06a4f52fa/providers/Microsoft.Web/locations/eastus/managedApis/sql"
                            },
                            "twitter": {
                                "connectionId": "[parameters('connections_twitter_externalid')]",
                                "connectionName": "twitter",
                                "id": "/subscriptions/5c01b8b4-6642-4c2d-bb51-51e06a4f52fa/providers/Microsoft.Web/locations/eastus/managedApis/twitter"