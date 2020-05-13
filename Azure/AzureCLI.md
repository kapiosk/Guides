# Azure CLI

## Installation

```bash
sudo apt-get install azure-cli
```

## Login

```bash
az login
```

## Accounts

List Subscriptions

```bash
az account list
```

Set Active Subscription

```bash
az account set -s "SubNameOrId"
```

```bash
az group list
az group show --name "ResourceGroupName"
az group export --name "ResourceGroupName"
```
