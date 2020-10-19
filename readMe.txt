https://docs.microsoft.com/en-us/azure/app-service/tutorial-dotnetcore-sqldb-app?pivots=platform-linux



az group create --name myResourceGroupSQLDb --location "Central US"

az sql server create --name mySqlDbBR1 --resource-group myResourceGroupSQLDb --location "Central US" --admin-user briegel --admin-password wriegelPs#2

        {- Finished ..
        "administratorLogin": "briegel",
        "administratorLoginPassword": null,
        "fullyQualifiedDomainName": "mysqldbbr1.database.windows.net",
        "id": "/subscriptions/f73d5946-3d0b-4ffd-8ead-6e8eaa213d9f/resourceGroups/myResourceGroupSQLDb/providers/Microsoft.Sql/servers/mysqldbbr1",
        "identity": null,
        "kind": "v12.0",
        "location": "centralus",
        "minimalTlsVersion": null,
        "name": "mysqldbbr1",
        "privateEndpointConnections": [],
        "publicNetworkAccess": "Enabled",
        "resourceGroup": "myResourceGroupSQLDb",
        "state": "Ready",
        "tags": null,
        "type": "Microsoft.Sql/servers",
        "version": "12.0"
        }

az sql server firewall-rule create --resource-group myResourceGroupSQLDb --server mysqldbbr1 --name AllowAzureIps --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0   

        {
        "endIpAddress": "0.0.0.0",
        "id": "/subscriptions/f73d5946-3d0b-4ffd-8ead-6e8eaa213d9f/resourceGroups/myResourceGroupSQLDb/providers/Microsoft.Sql/servers/mysqldbbr1/firewallRules/AllowAzureIps",
        "kind": "v12.0",
        "location": "Central US",
        "name": "AllowAzureIps",
        "resourceGroup": "myResourceGroupSQLDb",
        "startIpAddress": "0.0.0.0",
        "type": "Microsoft.Sql/servers/firewallRules"
        }

    RPC5CD7011QSR
    172.25.176.1

// vpn on

az sql server firewall-rule create --name AllowLocalClient --server mysqldbbr1 --resource-group myResourceGroupSQLDb --start-ip-address=98.201.1.0 --end-ip-address=98.201.1.255   

    {
    "endIpAddress": "98.201.1.255",
    "id": "/subscriptions/f73d5946-3d0b-4ffd-8ead-6e8eaa213d9f/resourceGroups/myResourceGroupSQLDb/providers/Microsoft.Sql/servers/mysqldbbr1/firewallRules/AllowLocalClient",
    "kind": "v12.0",
    "location": "Central US",
    "name": "AllowLocalClient",
    "resourceGroup": "myResourceGroupSQLDb",
    "startIpAddress": "98.201.1.0",
    "type": "Microsoft.Sql/servers/firewallRules"
    }

 az sql db show-connection-string --client ado.net --server mysqldbbr1 --name coreDB   

    "Server=tcp:mysqldbbr1.database.windows.net,1433;Database=coreDB;User ID=briegel;Password=wriegelPs#2;Encrypt=true;Connection Timeout=30;" 