sfpowerkit
==========

[![Build status](https://dev.azure.com/azlamsalam/sfpowerkit/_apis/build/status/sfpowerkit-CI)](https://dev.azure.com/azlamsalam/sfpowerkit/_build/latest?definitionId=1)


Salesforce DevOps Helper Extensions


## `sfpowerkit org:connectedapp:create`

Creates a connected app in the target org for JWT based authentication, Please note it only creates Connected App with All users may self authorize option, You would need to manually edit the policies to enable admin users are pre-approved and add your profile to this connected app

```
USAGE
  $ sfdx sfpowerkit:org:connectedapp:create -n <string> -c <filepath> -e <email> [-u <string>] [--apiversion 
  <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -c, --pathtocertificate=pathtocertificate       (required) Filepath to the private certificate for the connected app
                                                  to be created

  -e, --email=email                               (required) Email of the connected app to be created

  -n, --name=name                                 (required) Name of the connected app to be created

  -u, --targetusername=targetusername             username or alias for the target org; overrides default target org

  --apiversion=apiversion                         override the api version used for api requests made by this command

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this command invocation

EXAMPLE
  $ sfdx  sfpowerkit:org:connectedapp:create -u myOrg@example.com -n AzurePipelines -c id_rsa -e 
  azlam.salamm@invalid.com
     Created Connected App AzurePipelines in Target Org
```

_See code: [src\commands\sfpowerkit\org\connectedapp\create.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\org\connectedapp\create.ts)_



## `sfpowerkit org:connectedapp:retrieve`

Useful if you want to retreive a connected app key especially for the CI/CD system after a sandbox refresh. Pass the username and password of the target environment from which the sandbox was cloned. 

```
USAGE
  $ sfdx sfpowerkit:org:connectedapp:retrieve -n <string> -u <string> -p <string> [-s
  <string>] [-r <url>] [--json] [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -n, --name=name                                 (required) Name of the connected app to be
                                                  retreived

  -p, --password=password                         (required) Password for the org

  -r, --url=url                                   Security Token for the org

  -s, --securitytoken=securitytoken               Security Token for the org

  -u, --username=username                         (required) Username for the org

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this
                                                  command invocation

EXAMPLE
  $ sfdx  sfpowerkit:org:connectedapp:retrieve -u azlam@sfdc.com -p Xasdax2w2 -n
  AzurePipelines
     Retrived AzurePipelines Consumer Key : XSD21Sd23123w21321
```

_See code: [src\commands\sfpowerkit\org\connectedapp\retrieve.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\org\connectedapp\retrieve.ts)_


## `sfpowerkit:org:duplicaterule:deactivate`

Deactivates a duplicate rule in the target org

```
USAGE
  $ sfdx sfpowerkit:org:duplicaterule:deactivate -n <string> [-u <string>] [--apiversion <string>] [--json] [--loglevel
  trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS
  -n, --name=name                                 (required) Name of the duplicate rule

  -u, --targetusername=targetusername              username or alias for the target org; overrides default target org

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this
                                                  command invocation

EXAMPLE
    $ sfdx  sfpowerkit:org:duplicaterule:deactivate -n Account.CRM_Account_Rule_1 -u sandbox
       Polling for Retrieval Status
       Retrieved Duplicate Rule  with label : CRM Account Rule 2
       Preparing Deactivation
       Deploying Deactivated Rule with ID  0Af4Y000003OdTWSA0
       Polling for Deployment Status
       Polling for Deployment Status
       Duplicate Rule CRM Account Rule 2 deactivated
```

_See code: [src\commands\sfpowerkit\org\duplicaterule\deactivate.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.9.9/src\commands\sfpowerkit\org\duplicaterule\deactivate.ts)_

## `sfpowerkit:org:matchingrule:deactivate`

Deactivates a matching rule in the target org, Please ensure all duplicate rules are deactivated before using this

```
USAGE
  $ sfdx sfpowerkit:org:matchingrule:deactivate -n <string> [-u <string>] [--apiversion <string>] [--json] [--loglevel
  trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS
  -n, --name=name                                 (required) Name of the object
  -u, --targetusername=targetusername              username or alias for the target org; overrides default target org

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this
                                                  command invocation

EXAMPLE
    $ sfdx  sfpowerkit:org:matchingrule:deactivate -n Account -u sandbox
       Polling for Retrieval Status
       Retrieved Matching Rule  for Object : Account
       Preparing Deactivation
       Deploying Deactivated Matching Rule with ID  0Af4Y000003OePkSAK
       Polling for Deployment Status
       Polling for Deployment Status
       Matching Rule for Account deactivated
```

_See code: [src\commands\sfpowerkit\org\matchingrule\deactivate.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.9.9/src\commands\sfpowerkit\org\matchingrule\deactivate.ts)_


## `sfpowerkit:org:trigger:deactivate`

Deactivates a trigger in the target org

```
USAGE
  $ sfdx sfpowerkit:org:trigger:deactivate -n <string> [-u <string>] [--apiversion <string>] [--json] [--loglevel
  trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS
  -n, --name=name                                 (required) Name of the ApexTrigger
  -u, --targetusername=targetusername              username or alias for the target org; overrides default target org

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this
                                                  command invocation

EXAMPLE
    $ sfdx  sfpowerkit:org:trigger:deactivate -n AccountTrigger -u sandbox
    Polling for Retrieval Status
    Preparing Deactivation
    Deploying Deactivated ApexTrigger with ID  0Af4Y000003Q7GySAK
    Polling for Deployment Status
    Polling for Deployment Status
    ApexTrigger AccountTrigger deactivated
```

_See code: [src\commands\sfpowerkit\org\trigger\deactivate.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.9.11/src\commands\sfpowerkit\org\trigger\deactivate.ts)_

## `sfpowerkit:org:trigger:activate`

Activates a trigger in the target org

```
USAGE
  $ sfdx sfpowerkit:org:trigger:activate -n <string> [-u <string>] [--apiversion <string>] [--json] [--loglevel
  trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS
  -n, --name=name                                 (required) Name of the ApexTrigger
  -u, --targetusername=targetusername              username or alias for the target org; overrides default target org

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this
                                                  command invocation

EXAMPLE
    $ sfdx  sfpowerkit:org:trigger:deactivate -n AccountTrigger -u sandbox
    Polling for Retrieval Status
    Preparing Activation
    Deploying Activated ApexTrigger with ID  0Af4Y000003Q7GySAK
    Polling for Deployment Status
    Polling for Deployment Status
    ApexTrigger AccountTrigger Ativated
```

_See code: [src\commands\sfpowerkit\org\trigger\activate.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.9.11/src\commands\sfpowerkit\org\trigger\activate.ts)_



## `sfpowerkit:org:healthcheck`

Gets the  health details of an org against the Salesforce baseline

```
USAGE
  $ sfdx sfpowerkit:org:healthcheck [-u <string>] [--apiversion <string>] [--json] [--loglevel 
  trace|debug|info|warn|error|fatal]

OPTIONS
  -u, --targetusername=targetusername             username or alias for the target org; overrides default target org
  --apiversion=apiversion                         override the api version used for api requests made by this command
  --json                                          format output as json
  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this command invocation

EXAMPLE
  $ sfdx sfpowerkit:org:healthcheck  -u myOrg@example.com
     Successfully Retrived the healthstatus of the org
```

_See code: [src\commands\sfpowerkit\org\healthcheck.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\org\healthcheck.ts)_

## `sfpowerkit:org:orgcoverage`

Gets the apex tests coverage of an org

```
USAGE
  $ sfdx sfpowerkit:org:orgcoverage [-u <string>] [--apiversion <string>] [--json] [--loglevel 
  trace|debug|info|warn|error|fatal]

OPTIONS
  -u, --targetusername=targetusername             username or alias for the target org; 
  --apiversion=apiversion                         override the api version used for api requests made by this command
  --json                                          format output as json
  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this command invocation

EXAMPLE
  $ sfdx sfpowerkit:org:orgcoverage  -u myOrg@example.com
     Successfully Retrieved the Apex Test Coverage of the org 00D0k000000DmdpEAC
     coverage:85
```

_See code: [src\commands\sfpowerkit\org\orgcoverage.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\org\orgcoverage.ts)_


## `sfpowerkit:org:sandbox:create`

Creates a sandbox using the tooling api, ensure the user has the required permissions before using this command

```
USAGE
  $ sfdx sfpowerkit:org:sandbox:create -n <string> -d <string> -l <string> [-a <string>] [-f <string>] [-v 
  <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -a, --apexclass=apexclass                               A reference to the ID of an Apex class that runs after each
                                                          copy of the sandbox

  -d, --description=description                           (required) Description of the sandbox

  -f, --clonefrom=clonefrom                               A reference to the ID of a SandboxInfo that serves as the
                                                          source org for a cloned sandbox.

  -l, --licensetype=DEVELOPER|DEVELOPER_PRO|PARTIAL|FULL  (required) Type of the sandbox. Valid values are
                                                          DEVELOPER,DEVELOPER_PRO,PARTIAL,FULL

  -n, --name=name                                         (required) Name of the sandbox

  -v, --targetdevhubusername=targetdevhubusername         (required) username or alias for the dev hub org; overrides default dev hub org

  --apiversion=apiversion                                 override the api version used for api requests made by this
                                                          command

  --json                                                  format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)          [default: warn] logging level for this command invocation

EXAMPLE
  $ sfdx sfpowerkit:org:sandbox:create -d Testsandbox -l DEVELOPER -n test2 -v myOrg@example.com
     Successfully Enqueued Creation of Sandbox
```

_See code: [src\commands\sfpowerkit\org\sandbox\create.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\org\sandbox\create.ts)_

## ` sfpowerkit:org:sandbox:info`

Gets the status of a sandbox

```
USAGE
  $ sfdx sfpowerkit:org:sandbox:info -n <string> [-s] [-v <string>] [--apiversion <string>] [--json] [--loglevel 
  trace|debug|info|warn|error|fatal]

OPTIONS
  -n, --name=name                                 (required) Name of the sandbox
  -s, --showonlylatest                            Shows only the latest info of the sandbox record
  -v, --targetdevhubusername=targetdevhubusername (required) username or alias for the dev hub org; overrides default dev hub org
  --apiversion=apiversion                         override the api version used for api requests made by this command
  --json                                          format output as json
  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this command invocation

EXAMPLE
  $ sfdx sfpowerkit:org:sandbox:info -n test2  -u myOrg@example.com
     Successfully Enqueued Refresh of Sandbox
```

_See code: [src\commands\sfpowerkit\org\sandbox\info.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\org\sandbox\info.ts)_

## `sfpowerkit:org:sandbox:refresh`

Refresh a sandbox using the tooling api, ensure the user has the required permissions before using this command

```
USAGE
  $ sfdx sfpowerkit:org:sandbox:refresh -n <string> [-f <string>] [-v <string>] [--apiversion <string>] [--json] 
  [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -f, --clonefrom=clonefrom                       A reference to the ID of a SandboxInfo that serves as the source org
                                                  for a cloned sandbox.

  -n, --name=name                                 (required) Name of the sandbox

  -v, --targetdevhubusername=targetdevhubusername  (required) username or alias for the dev hub org; overrides default dev hub org

  --apiversion=apiversion                         override the api version used for api requests made by this command

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this command invocation

EXAMPLE
  $ sfdx sfpowerkit:org:sandbox:refresh -n test2  -f sitSandbox -u myOrg@example.com
     Successfully Enqueued Refresh of Sandbox
```

_See code: [src\commands\sfpowerkit\org\sandbox\refresh.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\org\sandbox\refresh.ts)_


## `sfpowerkit:org:scratchorg:usage`

Gets the active count of scratch org by users in a devhub, Ensure you have valid permissions 

```
USAGE
  $ sfdx sfpowerkit:org:scratchorg:usage -v <string> 
  [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -v, --targetdevhubusername=targetdevhubusername  (required) username or alias for the dev hub org; overrides default dev hub org


EXAMPLE
  $ sfdx sfpowerkit:org:scratchorg:usage -v devhub
    Active Scratch Orgs Remaining: 42 out of 100
    Daily Scratch Orgs Remaining: 171 out of 200

    IN_USE             SIGNUPEMAIL
    ─────────────────  ─────────────────
    2                  XYZ@KYZ.COM
    2                  JFK@KYZ.COM
    Total number of records retrieved: 4.
```

_See code: [src\commands\sfpowerkit\org\scratchorg\usage.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.9.16/src\commands\sfpowerkit\org\scratchorg\usage.ts)_


## `sfpowerkit:org:scratchorg:delete`

Delete the scratch org for a paritcular user.  Ensure you have valid permissions 

```
USAGE
  $ sfdx sfpowerkit:org:scratchorg:delete -v <string>  -e <string>
  [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -v, --targetdevhubusername=targetdevhubusername  (required) username or alias for the dev hub org; overrides default dev hub org
  
  -e, --email=email                                (required) Email of the user account's whose scratch org to be deleted


EXAMPLE
  $ sfdx sfpowerkit:org:scratchorg:delete  -e xyz@kyz.com -v devhub
    Found Scratch Org Ids for user xyz@kyz.com
    2AS6F000000XbxVWAS
    Deleting Scratch Orgs
    Deleted Scratch Org 2AS6F000000XbxVWAS
```

_See code: [src\commands\sfpowerkit\org\scratchorg\usage.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.9.16/src\commands\sfpowerkit\org\scratchorg\usage.ts)_


## `sfpowerkit:package:dependencies:install`

Install dependencies of a package

```
USAGE
  $ sfdx sfpowerkit:package:dependencies:install [-p <string>] [-k <string>] [-b <string>] [-w <string>] [-r] [-v 
  <string>] [-u <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -b, --branch=branch                              the package version’s branch

  -k, --installationkeys=installationkeys          installation key for key-protected packages (format is
                                                   1:MyPackage1Key 2: 3:MyPackage3Key... to allow some packages without
                                                   installation key)

  -p, --individualpackage=individualpackage        Installs a specific package especially for upgrade scenario

  -r, --noprompt                                   allow Remote Site Settings and Content Security Policy websites to
                                                   send or receive data without confirmation

  -u, --targetusername=targetusername              username or alias for the target org; overrides default target org

  -v, --targetdevhubusername=targetdevhubusername  username or alias for the dev hub org; overrides default dev hub org

  -w, --wait=wait                                  number of minutes to wait for installation status (also used for
                                                   publishwait). Default is 10

  --apiversion=apiversion                          override the api version used for api requests made by this command

  --json                                           format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)   [default: warn] logging level for this command invocation

EXAMPLE
  $ sfpowerkit package:dependencies:install -u MyScratchOrg -v MyDevHub -k "1:MyPackage1Key 2: 3:MyPackage3Key" -b "DEV"
```

_See code: [src\commands\sfpowerkit\package\dependencies\install.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\package\dependencies\install.ts)_

## `sfpowerkit:package:valid`

Validates a package to check whether it only contains valid metadata as per metadata coverage

```
USAGE
  $ sfdx sfpowerkit:package:valid [-n <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal]

OPTIONS
  -n, --package=package                           the package to analyze
  --json                                          format output as json
  --loglevel=(trace|debug|info|warn|error|fatal)  [default: warn] logging level for this command invocation

EXAMPLE
  $ sfdx sfpowerkit:package:valid -n testPackage
     Now analyzing inspections
  Converting package testPackage
  Source was successfully converted to Metadata API format and written to the location: 
  D:projects	estPackage	emp_sfpowerkitmdapi
  Elements supported included in your package testPackage are
  [
     "AuraDefinitionBundle",
     "CustomApplication",
     "ApexClass",
     "ContentAsset",
     "WorkflowRule"
  ]
```

_See code: [src\commands\sfpowerkit\package\valid.ts](https://github.com/azlamsalam/sfpowerkit/blob/v1.5.0/src\commands\sfpowerkit\package\valid.ts)_
