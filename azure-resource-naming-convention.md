# Azure Resource Naming Conventions

## 🎯 Purpose

To establish a consistent and scalable naming convention across all Azure resources that ensures clarity, manageability, and adherence to Azure constraints.

---

## ⚙️ General Naming Rules

|        Rule       |                              Description                                 |
|-------------------|--------------------------------------------------------------------------|
| Character Set     | Use letters (a–z), numbers (0–9), and hyphens (-)                        |
| Separator         | Hyphen (-) only                                                          |
| Disallowed        | No special characters (e.g., `!@#$%^&*()`), no underscores (_) or spaces |
| Case              | Use lowercase consistently across all resources                          |
| Length            | Maximum 90 characters (resource-specific limits apply)                   |
| Start/End         | Must start and end with a letter or number                               |
| Global Uniqueness | Required for certain services (e.g., Storage, SQL Server, Function App)  |

---

## 🧱 Standard Naming Pattern

```
<environment>-<project-name>-<region>-<resource-type>
```

### Example:
```
dev-platformeng-eu-rg
```

---

## 🔤 Component Definitions

|    Component    |                Description               |      Example    |
|-----------------|------------------------------------------|-----------------|
| `environment`   | Deployment environment                   | dev, test, prod |
| `project-name`  | Functional area, application, or service | platformeng     |
| `region`        | Azure region abbreviation                | eastus, weu     |
| `resource-type` | Abbreviated resource identifier          | rg, sa, sqlsvr  |

---

## 🌍 Region Abbreviations (Examples)

| Region Name       | Abbreviation |
|-------------------|--------------|
| East US           | eus          |
| West Europe       | weu          |
| Central India     | incentral    |
| Australia East    | ause         |

---

## 🗂 Resource-Specific Naming Rules

### 🏗 Resource Group

- **Pattern**: `<env>-<project>-<region>-rg`

|         Attribute        |                  Limitation / Rule                  |
|--------------------------|-----------------------------------------------------|
| Character Set            | Letters (uppercase/lowercase), numbers, hyphens (-) |
| Disallowed Characters    | No special characters (e.g., `!@#$%^&*()_+=[]{})    |
| Separator                | Only hyphens (-) allowed                            |
| Case Sensitivity         | Case-insensitive, lowercase recommended             |
| Length                   | Maximum 90 characters                               |
| Start/End Rule           | Must start and end with a letter or number          |
| Uniqueness Scope         | Unique within the Azure subscription                |
| Terraform Recommendation | Use locals/variables for dynamic generation         |

```
dev-platformeng-eus-rg
```

---

### 💾 Storage Account

- **Pattern**: `<env><project><region>sa`

|         Attribute        |                     Limitation / Rule                    |
|--------------------------|----------------------------------------------------------|
| Character Set            | Lowercase letters and numbers only                       |
| Disallowed Characters    | No uppercase letters, hyphens (-), or special characters |
| Separator                | No separators allowed                                    |
| Case Sensitivity         | Must be lowercase only                                   |
| Length                   | 3 to 24 characters                                       |
| Start/End Rule           | Must start and end with a letter or number               |
| Uniqueness Scope         | Globally unique                                          |
| Terraform Recommendation | Use `random_string` for uniqueness                       |

```
devplatformengeussa
```

---

### 🔐 Key Vault

- **Pattern**: `<env>-<project>-<region>-kv`

|        Attribute         |                   Limitation / Rule                      |
|--------------------------|----------------------------------------------------------|
| Character Set            | Lowercase letters, numbers, hyphens (-)                  |
| Disallowed Characters    | No uppercase, underscores, spaces, or special characters |
| Separator                | Hyphens allowed, but not consecutively                   |
| Case Sensitivity         | Must be lowercase only                                   |
| Length                   | 3 to 24 characters                                       |
| Start/End Rule           | Must start and end with a letter or number               |
| Uniqueness Scope         | Globally unique                                          |
| Terraform Recommendation | Ensure DNS-compliant names using validation              |

```
dev-platformeng-eus-kv
```

---

### ⚙ Function App

- **Pattern**: `<env>-<project>-<region>-fa`

|         Attribute        |                  Limitation / Rule                 |
|--------------------------|----------------------------------------------------|
| Character Set            | Lowercase letters, numbers, and hyphens (-)        |
| Disallowed Characters    | No special characters, underscores, or spaces      |
| Separator                | Hyphens (-) allowed                                |
| Case Sensitivity         | Must be lowercase only                             |
| Length                   | 2 to 60 characters                                 |
| Start/End Rule           | Must start and end with a letter or number         |
| Uniqueness Scope         | Globally unique                                    |
| Terraform Recommendation | Include environment/project context for uniqueness |

```
dev-platformeng-eus-fa
```

---

### 🗃 SQL Server and Database

#### SQL Server

- **Pattern**: `<env>-<project>-<region>-sqlsvr`

|         Attribute        |                Limitation / Rule              |
|--------------------------|-----------------------------------------------|
| Character Set            | Letters, numbers, and hyphens (-)             |
| Disallowed Characters    | No special characters, underscores, or spaces |
| Separator                | Hyphens (-) allowed                           |
| Case Sensitivity         | Case-insensitive                              |
| Length                   | 3 to 63 characters                            |
| Start/End Rule           | Must start and end with a letter or number    |
| Uniqueness Scope         | Globally unique                               |
| Terraform Recommendation | Add suffix or random component for uniqueness |

```
dev-platformeng-eus-sqlsvr
```

#### SQL Database

- **Pattern**: `<env>-<project>-<region>-sqldb`

|         Attribute        |              Limitation / Rule             |
|--------------------------|--------------------------------------------|
| Character Set            | Letters, numbers, and hyphens (-)          |
| Disallowed Characters    | No special characters or underscores       |
| Separator                | Hyphens (-) allowed                        |
| Case Sensitivity         | Case-insensitive                           |
| Length                   | 1 to 128 characters                        |
| Start/End Rule           | Must start and end with a letter or number |
| Uniqueness Scope         | Unique within SQL Server instance          |
| Terraform Recommendation | Use structured name patterns for clarity   |

```
test-integration-eus-sqldb
```

---

### 🌐 App Service

- **Pattern**: `<env>-<project>-<region>-as`

|         Attribute        |                 Limitation / Rule               |
|--------------------------|-------------------------------------------------|
| Character Set            | Lowercase letters, numbers, and hyphens (-)     |
| Disallowed Characters    | No special characters or underscores            |
| Separator                | Hyphens (-) allowed                             |
| Case Sensitivity         | Must be lowercase only                          |
| Length                   | 1 to 60 characters                              |
| Start/End Rule           | Must start and end with a letter or number      |
| Uniqueness Scope         | Globally unique                                 |
| Terraform Recommendation | Include environment in name to avoid collisions |

```
dev-platformeng-eus-as
```

---

### 🧱 App Service Plan

- **Pattern**: `<env>-<project>-<region>-asp`

|         Attribute        |                Limitation / Rule              |
|--------------------------|-----------------------------------------------|
| Character Set            | Letters, numbers, and hyphens (-)             |
| Disallowed Characters    | No special characters, underscores, or spaces |
| Separator                | Hyphens (-) allowed                           |
| Case Sensitivity         | Lowercase recommended                         |
| Length                   | 1 to 40 characters                            |
| Start/End Rule           | Must start and end with a letter or number    |
| Uniqueness Scope         | Unique within Resource Group                  |
| Terraform Recommendation | Follow pattern for shared resource naming     |

```
dev-platformeng-eus-asp
```

---

### 📦 Azure Container Registry (ACR)

- **Pattern**: `<env>-<project>-<region>-acr`

|         Attribute        |                 Limitation / Rule                |
|--------------------------|--------------------------------------------------|
| Character Set            | Letters, numbers, and hyphens (-)                |
| Disallowed Characters    | No special characters, underscores, or spaces    |
| Separator                | Hyphens (-) allowed                              |
| Case Sensitivity         | Lowercase recommended                            | 
| Length                   | 5 to 50 characters                               |
| Start/End Rule           | Must start and end with a letter or number       |
| Uniqueness Scope         | Globally unique                                  |
| Terraform Recommendation | Use `random_id` or suffix strategy in automation |

```
dev-platformeng-eus-acr
```

---

### 🔥 Databricks

- **Pattern**: `<env>-<project>-<region>-dbx`

|         Attribute        |                Limitation / Rule                |
|--------------------------|-------------------------------------------------|
| Character Set            | Letters, numbers, and hyphens (-)               |
| Disallowed Characters    | No special characters or underscores            |
| Separator                | Hyphens (-) allowed                             |
| Case Sensitivity         | Lowercase recommended                           |
| Length                   | 1 to 50 characters (name), up to 128 (resource) |
| Start/End Rule           | Must start and end with a letter or number      |
| Uniqueness Scope         | Unique within Subscription/Region               |
| Terraform Recommendation | Use consistent patterns per workspace           |

```
dev-platformeng-eus-dbx
```

---

### 🔄 Logic App

- **Pattern**: `<env>-<project>-<region>-la`

|         Attribute        |                  Limitation / Rule               |
|--------------------------|--------------------------------------------------|
| Character Set            | Letters, numbers, and hyphens (-)                |
| Disallowed Characters    | No special characters, underscores, or spaces    |
| Separator                | Hyphens (-) allowed                              |
| Case Sensitivity         | Lowercase recommended                            |
| Length                   | 1 to 80 characters                               |
| Start/End Rule           | Must start and end with a letter or number       |
| Uniqueness Scope         | Globally unique                                  | 
| Terraform Recommendation | Use `random_id` or suffix strategy in automation |

```
dev-platformeng-eus-la
```

---

### 🌐 Web Service

- **Pattern**: `<env>-<project>-<region>-ws`

|         Attribute        |                Limitation / Rule              |
|--------------------------|-----------------------------------------------|
| Character Set            | Lowercase letters, numbers, and hyphens (-)   |
| Disallowed Characters    | No special characters, underscores, or spaces |
| Separator                | Hyphens (-) allowed                           |
| Case Sensitivity         | Must be lowercase only                        |
| Length                   | 2 to 60 characters                            | 
| Start/End Rule           | Must start and end with a letter or number    |
| Uniqueness Scope         | Globally unique                               |
| Terraform Recommendation | Use deterministic patterns to avoid overlap   |

```
dev-platformeng-eus-ws
```

---

### 🧰 Web Service Plan

- **Pattern**: `<env>-<project>-<region>-wsp`

|          Attribute       |                 Limitation / Rule                |
|--------------------------|--------------------------------------------------|
| Character Set            | Lowercase letters, numbers, and hyphens (-)      |
| Disallowed Characters    | No special characters, underscores, or spaces    |
| Separator                | Hyphens (-) allowed                              |
| Case Sensitivity         | Lowercase recommended                            |
| Length                   | 1 to 60 characters                               | 
| Start/End Rule           | Must start and end with a letter or number       |
| Uniqueness Scope         | Globally unique                                  |
| Terraform Recommendation | Use `random_id` or suffix strategy in automation |

```
dev-platformeng-eus-wsp
```

---

## 🛠 Terraform Best Practices

- **Use `locals` and `variables`** to generate names dynamically.
- **Abstract naming logic** in reusable modules.
- **Enforce naming rules** with validation functions (`regex`, `length`, etc.).
- **Use descriptive suffixes** (e.g., `-sqlsvr`, `-dbx`) for resource-type clarity.
- **Ensure global uniqueness** via random suffixes when necessary (e.g., for Storage Accounts).

---

## 📜 Change Log

| Date       | Change Summary                         |
|------------|----------------------------------------|
| 2025-05-13 | Initial version with full structure    |

---
