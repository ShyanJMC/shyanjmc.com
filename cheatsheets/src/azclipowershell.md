# List users

> az user list 

# Create user

```
az ad user create --display-name
                  --password
                  --user-principal-name
                  [--force-change-password-next-login {false, true}]
                  [--immutable-id]
                  [--mail-nickname]
```

# Delete user

> az ad user delete --id [user]

# Get user member groups

> az ad user get-member-groups --id [user] 

# See user details

> az ad user show --id [user]

# MFA State Users
- https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates

# Usuarios sin MFA
```
securityresources
        | where type == "microsoft.security/assessments"
        | extend source = trim(' ', tolower(tostring(properties.resourceDetails.Source)))
                                          | extend resourceId = trim(' ', tolower(tostring(case(
                                                                                    source =~ "azure", properties.resourceDetails.Id,
                                                                                    source =~ "aws" and isnotempty(tostring(properties.resourceDetails.ConnectorId)), properties.resourceDetails.Id,
                                                                                    source =~ "gcp" and isnotempty(tostring(properties.resourceDetails.ConnectorId)), properties.resourceDetails.Id,
                                                                                    source =~ 'aws', properties.resourceDetails.AzureResourceId,
                                                                                    source =~ 'gcp', properties.resourceDetails.AzureResourceId,
                                                                                    extract('^(.+)/providers/Microsoft.Security/assessments/.+$',1,id)
                                                                                    ))))
        | extend status = trim(" ", tostring(properties.status.code))
        | extend cause = trim(" ", tostring(properties.status.cause))
        | extend assessmentKey = tostring(name)
        | where assessmentKey == "57e98606-6b1e-6193-0e3d-fe621387c16b"
```

# Windows vulnerabilties
# Querys de logs

## Ensure 'Do not show feedback notifications is set to enabled'
- Critical
- Registry, Policy Option

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "596d3922-71a7-49ce-b34b-1f5e63ff03da")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Enable insecure guest logons' is set to 'Disabled'
- Critical
- Registry, Policy Option

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "09ed81b2-8dba-4009-84f9-dcfd6009ed0d")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Enable 'Scan removable drives' by setting DisableRemovableDriveScanning (REG_DWORD) to 0
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "081da702-ce92-480f-aa68-af49bf5b94db")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Bypass traverse checking
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "a30f6d7d-f3dc-442c-8a1f-921123c6250c")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Configure 'Access this computer from the network'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "3f2d92c2-5850-4f2d-b245-f5089aa975dd")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Microsoft network server: Digitally sign communications (if client agrees)' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "b625a003-d015-436e-89fb-fb2dfe71ae0f")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Disallow WinRM from storing RunAs credentials' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "5fc2dc21-a630-45ee-a62d-5e3d87a45a84")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Interactive logon: Do not display last user name' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "9e11215f-9b0b-4ca6-ad5b-d1a0c989af36")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Audit Process Creation' is set to 'Success'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "6b3dc518-61f4-4a47-920c-0411674596a0")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Domain: Firewall state' is set to 'On (recommended)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "4a459b04-79c8-4fb3-9ea0-cf4b77ee58d7")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Network access: Do not allow anonymous enumeration of SAM accounts and shares' is set to 'Enabled' (MS only)
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "87822480-3af9-4cf1-b0d2-93ceb957b129")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'System: Specify the maximum log file size (KB)' is set to 'Enabled: 32,768 or greater'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "3e20b64c-0356-4e95-ba4e-2ebd51e10bb9")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Domain: Outbound connections' is set to 'Allow (default)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "68757cac-7589-4ed9-a162-27e5926f2deb")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Network security: LAN Manager authentication level' is set to 'Send NTLMv2 response only. Refuse LM & NTLM'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "315cc7e3-7252-47ce-af2f-9abf243fac16")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Do not allow passwords to be saved' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "0979b47f-fbbf-46ad-8def-768256fa012a")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Public: Settings: Apply local connection security rules' is set to 'Yes'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "10a43735-527c-46f0-a95c-954a8f9594dc")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Microsoft network client: Digitally sign communications (always)' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "41a8be7d-69bd-48f4-ae77-9568cf7b15d1")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'User Account Control: Admin Approval Mode for the Built-in Administrator account' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "967531f7-69cd-4a38-a517-3ebf4e5284cd")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Minimum password length' is set to '14 or more character(s)'
- Critical
- REgistry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "bc9d4fef-9e33-48fc-bcbd-b53e60caf4a2")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'User Account Control: Behavior of the elevation prompt for standard users' is set to 'Automatically deny elevation requests'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "ea132d56-9c29-4d2a-bc92-fc81f616e540")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'User Account Control: Switch to the secure desktop when prompting for elevation' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "21a9a771-ef63-419c-bee4-8619f19a77ff")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Deny log on through Remote Desktop Services' is configured
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "60e0c2c9-0b14-44fe-83d6-2b7095e06674")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Turn off Autoplay' is set to 'Enabled: All drives'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "d0f025af-b24b-49ab-9b75-60f485ed5407")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Deny log on as a batch job' is configured
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "49258884-b2f0-4a4e-b66a-6954bb8473bf")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Include command line in process creation events' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "1648f727-644b-4454-a472-b1a803342e8a")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode' is set to 'Prompt for consent on the secure desktop'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "fc8a4401-ff7a-4a6d-add4-758acce6b76c")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Password must meet complexity requirements' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "299d1595-5ab2-4ef5-b287-6477c0df5178")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Deny log on locally' is configured
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "b7432fc2-51ba-4ddf-83dd-ca7f92e670c1")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Enforce password history' is set to '24 or more password(s)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "dad8097d-db46-4df3-9839-a8504e60c878")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Configure Solicited Remote Assistance' is set to 'Disabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "b17eabc0-5d73-4861-acc8-d5b97bc53f12")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Enable RPC Endpoint Mapper Client Authentication' is set to 'Enabled' (MS only)
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "7983c8b6-ceca-4475-b58c-5b1d7745cde3")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Public: Outbound connections' is set to 'Allow (default)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "753e721c-be46-47f4-9571-8509ca5c1e61")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Setup: Specify the maximum log file size (KB)' is set to 'Enabled: 32,768 or greater'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "5bfb71c2-897f-4ccb-b7d5-7181b1f2527a")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Network security: Minimum session security for NTLM SSP based (including secure RPC) clients' is set to 'Require NTLMv2 session security, Require 128-bit encryption'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "2a074d39-eee4-4bfe-b1e7-4132c033a762")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Require secure RPC communication' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "01d9a108-3379-4c5a-8236-1a724bcccff1")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Audit Removable Storage' is set to 'Success and Failure'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "b88b1d85-5f3c-4235-91ab-6d8b5e767311")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Disallow Autoplay for non-volume devices' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "420cf8af-038e-4d06-89a4-aa8bfaec0191")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Configure 'Allow log on locally'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "051545a4-179e-4c04-9e9b-8f33821ef36f")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Security: Specify the maximum log file size (KB)' is set to 'Enabled: 196,608 or greater'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "c139db2e-8dea-418e-bf7c-372ec0278e31")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Network security: Minimum session security for NTLM SSP based (including secure RPC) servers' is set to 'Require NTLMv2 session security, Require 128-bit encryption'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "6ed9ad58-c9de-4a8b-9512-8fe5421ac8a7")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Public: Firewall state' is set to 'On (recommended)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "5e33a15a-7db0-4a1d-b771-db3764f3a625")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Microsoft network server: Digitally sign communications (always)' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "032b5976-1c4b-4c68-bc5d-0c65e35306b2")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Always prompt for password upon connection' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "d9794f70-e03c-40e5-a812-d2878c0eb6d5")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Application: Specify the maximum log file size (KB)' is set to 'Enabled: 32,768 or greater'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "e7e377d1-d6e0-4acc-a073-75b3243a646e")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Configure 'Deny access to this computer from the network'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "fbe348fd-0402-4e31-8482-66ae9ae82ea2")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Domain: Settings: Apply local connection security rules' is set to 'Yes (default)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "88338d83-a4e2-421b-b3f3-db6bd2c694a0")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Set the default behavior for AutoRun' is set to 'Enabled: Do not execute any autorun commands'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "7869ddef-04ab-4cc5-90f2-5e6fd1540cba")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Private: Firewall state' is set to 'On (recommended)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "c8e1851a-fb32-4197-a1c0-d9da262d37f1")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Disallow Digest authentication' is set to 'Enabled'
- Critical
- REgistry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "34edb7eb-697c-4be9-8830-5aa5b031372e")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Windows Firewall: Private: Outbound connections' is set to 'Allow (default)'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "c98cfb4e-113f-4a25-a080-ab1f7d0f8f38")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```

## Ensure 'Network security: Allow Local System to use computer identity for NTLM' is set to 'Enabled'
- Critical
- Registry, Policy Options

```
SecurityBaseline
| where AnalyzeResult == "Failed" and (BaselineRuleId =~ "e7d5034f-5652-4180-90c8-c49130acb3c6")
| where tolower(SubscriptionId) in ("SUBSCRIPTION", "SUBSCRIPTION") or isempty(SubscriptionId)
| summarize AggregatedValue = dcount(SourceComputerId) by SourceComputerId, Computer
| limit 1000000000
```
