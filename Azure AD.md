* Azure Active Directory (Azure AD) is a cloud-based identity and access management service.
  
* Tenant refers to single instance of Azure Active Directory (Azure AD) which is a platform for managing users, groups and the permissions.

* Azure AD authenticate and authorizes security principles (users, groups, devices, appliation) against Azure Services.

* Each Azure subscription can only trust a single Azure Active directory.

* One or more Azure subscriptions can establish a trust relationship with an instance of Azure Active Directory. But we cannot have a multiple Azure AD in one Azure subscription.
priya@tpriya7799gmail.onmicrosoft.com

* When the account is created we get an azure active directory instance with a primary domain name *.onmicrosoft.com

Who uses Azure AD
------------------
* IT admins
* App developers
* Microsoft 365, Office 365, Azure, or Dynamics CRM Online subscribers

classic subscription administrative roles.
------------------------------------------
* Account Administrator
* Service Administrator
* Co- Adiministartor

Azure roles
-----------
* Owner
* Contributor
* Reader
* User Access Administration

Azure AD roles
--------------
* GLobal Administration
* User Administration
* Billing Administration

* Single tenant:	Azure tenants that access other services in a dedicated environment are considered single tenant.
* Multi-tenant:	Azure tenants that access other services in a shared environment, across multiple organizations, are considered multi-tenant.

Ways to assign access rights:
----------------------------
* Direct assignment:
  * The resource owner directly assigns the user to the resource.
* Group assignment:
  *  The resource owner assigns an Azure AD group to the resource, which automatically gives all of the group members access to the resource.
  *  Group membership is managed by both the group owner and the resource owner.
* Rule-based assignment:
  *  The resource owner creates a group and uses a rule to define which users are assigned to a specific resource. 
  *  The rule is based on attributes that are assigned to individual users.
* External authority assignment:
  *  Access comes from an external source, such as an on-premises directory or a SaaS app.


What are the Azure AD licenses
------------------------------
* Azure Active Directory Free
* Azure Active Directory Premium P1
* Azure Active Directory Premium P2
* "Pay as you go" feature licenses
  
* The core of Azure AD is a directory of users. Each User has an identity thats comprised of
  * User ID
  * password
  * Other Properties 

* The UserID and Password are used to authenticate the user and roles are used for authorization to perform certain activities on Azure AD.

Azure Active Directory authentication:
--------------------------------------
* Azure AD authentication includes the following components:
    * Self-service password reset:
      * Password change
      * Password Reset
      * Account unlock
    * Azure AD Multi-Factor Authentication:
      * Azure AD Multi-Factor Authentication works by requiring two or more of the following authentication methods:
        * Something you know, typically a password.
        * Something you have, such as a trusted device that is not easily duplicated, like a phone or hardware key.
        * Something you are - biometrics like a fingerprint or face scan.
    * Hybrid integration to write password changes back to on-premises environment
    * Hybrid integration to enforce password protection policies for an on-premises environment
    * Passwordless authentication:
      * credentials are provided by using methods like biometrics.

Group and membership types:
---------------------------
* Group types:
  * Security
  * Microsoft 365
* Membership types:
  * Assigned
  * Dynamic user
  * Dynamic device

Role definition:
---------------
* It is a collection of permissions.
* lists the actions that can be performed, such as read, write, and delete. 
* It can also list the actions that are excluded from allowed actions or actions related to underlying data.
* Name/roleName:	
  * The display name of the role.
* Id/name:	
  * The unique ID of the role. Built-in roles have the same role ID across clouds.
* IsCustom/roleType:	
  * Indicates whether this is a custom role. Set to "true" or CustomRole for custom roles. Set to "false" or BuiltInRole for built-in roles.
* Description/description:	
  * The description of the role.
* Actions/actions:	
  * An array of strings that specifies the control plane actions that the role allows to be performed.
* NotActions/notActions:	
  * An array of strings that specifies the control plane actions that are excluded from the allowed Actions.
* DataActions/dataActions:	
  * An array of strings that specifies the data plane actions that the role allows to be performed to your data within that object.
* NotDataActions/notDataActions:	
  * An array of strings that specifies the data plane actions that are excluded from the allowed DataActions.
* AssignableScopes/assignableScopes:	
  * An array of strings that specifies the scopes that the role is available for assignment.

Actions format:
---------------
* Actions are specified with strings that have the following format:
```
{Company}.{ProviderName}/{resourceType}/{action}
```

* Azure has the following capabilites:
  * Act as Identity Provider for your applicatons: Azure AD B2C
  * Act as Guest Identity and Access Management Solution: Azure AD B2B

AD has different Directory Services:
------------------------------------
* Active Directory Domain Services (AD DS)
* Active Directory Light Weight Directory Services (AD LDS)
* Active Directory Certificate Services (AD CS)
* Active Directory Federation Services (AD FS)

* To communicate with your Azure Active Directory Domain Services (Azure AD DS) managed domain, the Lightweight Directory Access Protocol (LDAP) is used.
* By default, the LDAP traffic isn't encrypted, which is a security concern for many environments.
* With Azure AD DS, you can configure the managed domain to use secure Lightweight Directory Access Protocol (LDAPS). When you use secure LDAP, the traffic is encrypted. 
* Secure LDAP is also known as LDAP over Secure Sockets Layer (SSL) / Transport Layer Security (TLS).
* 