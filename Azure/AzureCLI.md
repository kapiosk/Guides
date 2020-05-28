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

## Storage

Download container files (note does not create initial ToFolder)

```bash
az storage blob download-batch -d "ToFolder" -s "FromContainer" --connection-string ""
```

Upload files to container (note does not create container)

```bash
az storage blob upload-batch -d "ToContainer" -s "FromFolder" --connection-string ""
```
