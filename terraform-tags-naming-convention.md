
- **businessunit**: Abbreviated name of the business unit (e.g. `fin`, `hr`)  
- **application**: Identifier for the application / workload  
- **environment**: `dev`, `qa`, `stage`, `prod`  
- **region**: Azure region code, e.g. `eastus`, `westeurope`  
- **resourcetype**: Standard abbreviations (see below)  
- **instance**: Sequential numeric identifier (e.g. `01`, `001`)  

### Naming Rules & Restrictions

- Use only lowercase letters, numbers, and hyphens (`-`) unless a resource disallows hyphens.  
- No spaces, special characters (unless explicitly allowed)  
- Each resource type has specific length and character constraints.  
- Naming must consider uniqueness scopes (global, resource group, resource level)  
- Do **not** use `#` in resource names.

### Resource Abbreviations

We adopt the official Azure abbreviations (or internal abbreviations) for resource types. For example:  
- `vm` for virtual machines  
- `rg` for resource groups  
- `st` or `storage` for storage accounts  
- `vnet` for virtual networks  
- etc.  
(Refer to Azure’s abbreviation list: Microsoft catalog) 

---

## Tagging Strategy

### Purpose of Tags

Tags allow us to attach metadata to resources, enabling cost tracking, governance, and operational context. Unlike resource names, tags can be modified after resource creation.  

### Standard Tag Keys

Here is a set of **mandatory** tags that must be applied to all Azure resources:

| Tag Key        | Description                          | Example Value           |
|----------------|--------------------------------------|--------------------------|
| `environment`  | Deployment environment               | `prod`, `dev`, `qa`      |
| `business_unit`| Business unit or cost center code    | `finance`, `hr`, `ops`   |
| `application`  | Application or workload name         | `payroll`, `crm`         |
| `owner`        | Person or team responsible           | `alice`, `team-cloud`    |
| `cost_center`  | Accounting cost center code          | `CC1234`                 |

Optional tags may include: `data_classification`, `sla`, `backup_schedule`, `created_by`, `create_date`, etc.

> Tag names must be **case-sensitive exact** (so stick to one casing style).  
> Tag names **cannot** include characters such as `<, >, %, &, ?, /` or spaces. :contentReference[oaicite:24]{index=24}  

### Terraform Implementation

We use a shared local map for common tags and merge in resource-specific tags:

```hcl
locals {
  common_tags = {
    environment   = var.environment
    business_unit = var.business_unit
    application   = var.application
    owner          = var.owner
    cost_center    = var.cost_center
  }
}

resource "azurerm_resource_group" "rg" {
  name     = format("rg-%s-%s-%s", var.business_unit, var.application, var.environment)
  location = var.location

  tags = merge(
    local.common_tags,
    {
      role = "infrastructure"
    }
  )
}


Tag Enforcement & Governance

Use Azure Policy to require certain tags at resource creation or update. 
Microsoft Learn

Regularly audit tag compliance across the environment

Automate tag population where possible to reduce human error

Examples

hr-payroll-prod-eastus-vm-01 (virtual machine)

fin-crm-dev-westeurope-sql-001 (SQL database)

For both, tags would include environment = prod, business_unit = hr (or fin), application = payroll (or crm), etc.