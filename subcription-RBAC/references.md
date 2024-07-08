**Creating a custom Azure RBAC (Role-Based Access Control) role, follow these steps:**
-------------------------------
1.  **Determine Permissions Needed**:
    
    *   Look at existing built-in roles.
        
    *   List the Azure services you want to grant access to.
        
    *   Determine the resource providers that map to the Azure services.
        
2.  **Choose How to Start**:
    
    *   Clone an existing role (if it closely matches your requirements).
        
    *   Start from scratch.
        
    *   Use a JSON file as a template.
        
3.  **Create the Custom Role**:
    
    *   In the Azure portal, open the management group, subscription, or resource group where you want the custom role to be assignable.
        
    *   Open “Access control (IAM).”
        
    *   Choose either cloning or starting from scratch.
        
4.  **Test the Custom Role**:
    
    *   Assign the role to a resource within the subscription.
        
    *   Review and validate its behavior.

Key differences between **Azure RBAC roles** and **Microsoft Entra ID roles**:
------------------------------------------------------------------------------

1.  **Azure RBAC Roles**:
    
    *   Govern access to resources deployed within Azure (e.g., virtual networks, machines, resource groups).
        
    *   Role assignments can be made at various scopes (subscription, management group, resource group, or resource).
        
    *   Focus on permissions for managing specific Azure resources.
        
2.  **Microsoft Entra ID Roles**:
    
    *   Control access to Microsoft Entra resources (such as users, groups, and applications) using the Microsoft Graph API.
        
    *   Operate at the **tenant level**, impacting users’ abilities within that specific tenant.

    **Format of the Azure RBAC JSON file**
```json
{
  "Name": "CustomRoleName",
  "Id": "UniqueRoleId",
  "IsCustom": true,
  "Description": "Description of the custom role",
  "Actions": [],
  "NotActions": [],
  "DataActions": [],
  "NotDataActions": [],
  "AssignableScopes": []
}
```

**Azure Blueprints**:

1.  **Definition**:
    
    *   Azure Blueprints allow cloud architects and IT groups to define a repeatable set of Azure resources that adhere to an organization’s standards, patterns, and requirements.
        
    *   [Think of it like an architectural blueprint that sketches out the design parameters for your Azure environment](https://learn.microsoft.com/en-us/azure/governance/blueprints/overview)[1](https://learn.microsoft.com/en-us/azure/governance/blueprints/overview)[2](https://blog.hensongroup.com/what-is-azure-blueprints/).
        
2.  **Purpose**:
    
    *   **Consistency**: Blueprints ensure consistent deployments by packaging key artifacts (e.g., Azure Resource Manager templates, role assignments, policies) together.
        
    *   **Compliance**: They help maintain compliance with organizational standards.
        
    *   **Speed**: Development teams can rapidly create new environments while staying within compliance boundaries.
        
    *   [**Versioning**: Fine-tune control and management through versioning](https://azure.microsoft.com/en-us/products/blueprints/)[3](https://azure.microsoft.com/en-us/products/blueprints/).
        
3.  **Archiving**:
    
    *   When a blueprint is no longer needed, it can be **archived**. [This preserves its configuration and associated data for historical analysis](https://www.theknowledgeacademy.com/blog/azure-blueprints/)[4](https://www.theknowledgeacademy.com/blog/azure-blueprints/).
