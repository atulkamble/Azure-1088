# Azure Table Storage

## Overview

Azure Table Storage is a NoSQL key-value data store service in Microsoft Azure used for storing large amounts of structured, non-relational data.

It is highly scalable, cost-effective, and optimized for fast read/write operations.

---

# Theory

## What is Azure Table Storage?

Azure Table Storage stores data in the form of:

* Tables
* Entities (Rows)
* Properties (Columns)

It is a schema-less NoSQL database service.

---

## Important Concepts

| Component     | Description                            |
| ------------- | -------------------------------------- |
| Table         | Collection of entities                 |
| Entity        | A single row of data                   |
| Property      | Column inside an entity                |
| Partition Key | Used for scaling and partitioning data |
| Row Key       | Unique identifier for each entity      |

---

## NoSQL Key-Value Model

Azure Table Storage follows a:

* NoSQL
* Key-Value
* Semi-structured data model

Unlike traditional SQL databases:

* No fixed schema
* Fast scalability
* High availability
* Massive storage support

---

## Partition Key

Partition Key is used for:

* Data grouping
* Performance optimization
* Horizontal scaling

Entities with the same Partition Key are stored together.

Example:

```text
PartitionKey = IT
```

---

## Row Key

Row Key acts as:

* Unique identifier
* Primary key within a partition

Example:

```text
RowKey = 101
```

Combination of:

```text
PartitionKey + RowKey
```

must always be unique.

---

# Real-Time Use Cases

## IoT Applications

Used for:

* Sensor data
* Device telemetry
* Real-time readings

---

## Logs Storage

Stores:

* Application logs
* Monitoring logs
* System events

---

## Metadata Storage

Stores:

* Data about data
* File attributes
* Object properties

Example:

* Blob metadata
* User activity metadata

---

# Practical

## Prerequisites

### Install Azure CLI

For macOS/Linux:

```bash
brew install azure-cli
```

For Windows:

```powershell
winget install Microsoft.AzureCLI
```

---

## Verify Azure CLI

```bash
az --version
```

---

## Login to Azure

```bash
az login
```

---

# Configure Environment Variables

```bash
export AZURE_STORAGE_ACCOUNT=mystorageaccount997008

export AZURE_STORAGE_KEY=M1ebYaxDaA6OSpg1Fg3IRGnrlBM+owg+P+/VmRW+vvvPvLwb8JPkjcz3E4ADpULnXQYHzBBSkmz8+AStYcYYEA==
```

---

## Verify Variables

```bash
echo $AZURE_STORAGE_ACCOUNT

echo $AZURE_STORAGE_KEY
```

---

# Sample Employee Data

| Partition Key | RowKey | Name  | Departments | Exp |
| ------------- | ------ | ----- | ----------- | --- |
| IT            | 101    | Atul  | DevOps      | 5   |
| IT            | 102    | Ravi  | Cloud       | 3   |
| HR            | 201    | Sneha | HR          | 4   |

---

# Create Azure Table

```bash
az storage table create \
  --name employee \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

# Insert Entities

## Insert Employee 1

```bash
az storage entity insert \
  --table-name employee \
  --entity PartitionKey=IT RowKey=101 Name=Atul Departments=DevOps Exp=5 \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

## Insert Employee 2

```bash
az storage entity insert \
  --table-name employee \
  --entity PartitionKey=IT RowKey=102 Name=Ravi Departments=Cloud Exp=3 \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

## Insert Employee 3

```bash
az storage entity insert \
  --table-name employee \
  --entity PartitionKey=HR RowKey=201 Name=Sneha Departments=HR Exp=4 \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

# Query Table Data

```bash
az storage entity query \
  --table-name employee \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

# Expected Output

```json
[
  {
    "PartitionKey": "IT",
    "RowKey": "101",
    "Name": "Atul",
    "Departments": "DevOps",
    "Exp": "5"
  },
  {
    "PartitionKey": "IT",
    "RowKey": "102",
    "Name": "Ravi",
    "Departments": "Cloud",
    "Exp": "3"
  },
  {
    "PartitionKey": "HR",
    "RowKey": "201",
    "Name": "Sneha",
    "Departments": "HR",
    "Exp": "4"
  }
]
```

---

# Points to Remember

* Azure Table Storage is NoSQL.
* Uses key-value structure.
* No fixed schema required.
* Partition Key improves scalability.
* Row Key uniquely identifies records.
* Suitable for logs, telemetry, metadata, and large-scale applications.
* Cost-effective for massive datasets.

---

# Common Azure Table Storage Commands

## List Tables

```bash
az storage table list \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY \
  --output table
```

---

## Delete Entity

```bash
az storage entity delete \
  --table-name employee \
  --partition-key IT \
  --row-key 101 \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

## Delete Table

```bash
az storage table delete \
  --name employee \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```
