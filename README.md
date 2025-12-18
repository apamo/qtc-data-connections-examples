# QTC Data Connections Postman Collection

This repository contains a Postman collection with working examples of **Qlik Talend Cloud Data Integration (QTC) data connection creation** using the `/api/v1/data-connections` REST API.

The collection is designed as a **practical reference** for creating source and target connections for the most commonly used databases and data platforms, including traditional RDBMS and modern cloud data platforms.

---

## Scope and purpose

The main goals of this collection are:

- Demonstrate how to create QTC data connections programmatically
- Provide ready-to-reuse payload patterns for common platforms
- Help customers, partners, and internal teams automate connection provisioning
- Serve as a reference alongside official Qlik documentation

The collection focuses on **connection creation and management only**, not on task creation or pipeline orchestration.

---

## What is included

### Core API operations

- List existing data connections
- Retrieve connection properties by ID
- List available data sources (connectors)
- Retrieve connector API specifications
- Create source and target connections
- Update existing connections using PATCH (for example credential or key rotation)

### Supported platforms

#### RDBMS sources and targets
- MySQL (source and target)
- Microsoft SQL Server (source and target)
- PostgreSQL (source and target)
- Oracle (source and target)

#### Cloud data platforms and storage targets
- Snowflake (target, key-pair authentication)
- Databricks (target, personal access token)
- Google BigQuery (target, service account JSON)
- Azure Data Lake Storage Gen2 (target)
- Amazon S3 (target)
- Google Cloud Storage (target)

---

## Collection structure

The Postman collection is organized into:

1. **Discovery endpoints**
   - List data connections
   - List data sources
   - Retrieve data source API specifications
   - Retrieve connection properties by ID

2. **Connection creation examples**
   - Source connections
   - Target connections
   - Platform-specific payloads

3. **Connection update examples**
   - Update credentials using PATCH

Each request is self-contained and can be executed independently once variables are configured.

---

## Prerequisites

- Access to a Qlik Talend Cloud tenant with Data Integration enabled
- Permissions to create data connections in the target space
- A valid API bearer token (For details, see [Qlik Cloud API key generation](https://help.qlik.com/en-US/cloud-services/Subsystems/Hub/Content/Sense_Hub/Admin/mc-generate-api-keys.htm)
- Postman (desktop or web)

---

## How to use

### 1. Import the collection

- Open Postman
- Import the JSON collection from this repository

### 2. Configure collection variables

The collection uses Postman variables extensively. At minimum, configure:

| Variable | Description |
|--------|------------|
| `hostname` | Qlik Cloud tenant hostname (without protocol) |
| `token` | Bearer token for QTC APIs |
| `spaceId` | Target Qlik Cloud space ID |
| `gatewayId` | Data Movement Gateway ID or managed gateway identifier |

Additional variables are required depending on the connector, for example:

- `rdbmsUsername`, `rdbmsPassword`
- `mssqlUsername`, `mssqlPassword`
- `snowflakeEncodedValue`, `snowflakePassPhrase`
- `bigQueryEncodedValue`
- `databricksToken`
- `adlsclientappid`, `adlsclientappkey`
- `s3accessKey`, `s3secretKey`

All sensitive values should be stored **only in Postman environments** and must never be committed to GitHub.

---

## Recommended execution order

1. **List Connections**  
   Validate authentication and permissions.

2. **List Data Sources**  
   Discover available connectors and IDs.

3. **Retrieve Data Source Properties**  
   Inspect required and optional connection properties.

4. **Create Source or Target Connections**  
   Run the platform-specific creation requests.

After creation, the connection ID is automatically stored in a Postman variable for reuse in subsequent requests.

---

## Authentication

All requests use bearer token authentication:

```http
Authorization: Bearer <TOKEN>
Content-Type: application/json

---

## Relationship to official documentation

This repository complements, but does not replace, official Qlik documentation.

Always cross-check with:

- [Qlik Cloud REST API documentation](https://qlik.dev/apis/rest/#api-reference-documentation)
- [Settings up connections in Qlik Talend Cloud](https://help.qlik.com/en-US/cloud-services/Subsystems/Hub/Content/Sense_Hub/DataIntegration/Introduction/Sources-and-targets.htm)
- [Data Movement Gateway deployment and networking documentation](https://help.qlik.com/en-US/cloud-services/Subsystems/Hub/Content/Sense_Hub/Gateways/replication-gateway.htm)

---

## Contributing

Contributions are welcome:

- Add new connectors
- Add source examples where only targets exist
- Improve variable naming consistency
- Document connector-specific caveats and limitations

Keep examples minimal, focused, and free of sensitive information.

---

## Disclaimer

This repository is provided for reference and automation support purposes only. Not officially supported by Qlik. 
API behavior, required properties, and connector capabilities may change and evolve over time.