[comment]: # "Auto-generated SOAR connector documentation"
# Trellix Malware Analysis

Publisher: Splunk Community  
Connector Version: 1\.0\.2  
Product Vendor: Trellix  
Product Name: Malware Analysis  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 5\.4\.0  

This app provides connectivity to the Trellix Advanced Malware Analysis tool

[comment]: # "File: README.md"
[comment]: # "Copyright (c) 2023 Splunk Inc."
[comment]: # ""
[comment]: # "Licensed under the Apache License, Version 2.0 (the 'License');"
[comment]: # "you may not use this file except in compliance with the License."
[comment]: # "You may obtain a copy of the License at"
[comment]: # ""
[comment]: # "    http://www.apache.org/licenses/LICENSE-2.0"
[comment]: # ""
[comment]: # "Unless required by applicable law or agreed to in writing, software distributed under"
[comment]: # "the License is distributed on an 'AS IS' BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,"
[comment]: # "either express or implied. See the License for the specific language governing permissions"
[comment]: # "and limitations under the License."
[comment]: # ""
This app is used for detonating files and URLs on a Trellix AX (Malware Analysis) console.

**Permissions**

To submit API requests from a remote system, you need a valid API user account on the appliance
where you will run the Web Services API. Create one of the following API user accounts:

-   api_analyst
-   api_monitor

The following tables show the breakdown of the user access and what actions they can perform.

| Permissions                        | api_analyst | api_monitor | admin |
|------------------------------------|-------------|-------------|-------|
| Read Alerts                        | Yes         | Yes         | Yes   |
| Update Alerts (Central Management) | Yes         | No          | Yes   |
| Read Reports                       | Yes         | Yes         | Yes   |
| Read Stats (Central Management)    | Yes         | No          | Yes   |
| Submit Object                      | Yes         | No          | Yes   |
| Submit URL (other appliances)      | Yes         | No          | Yes   |


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Malware Analysis asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Base URL for the console, i\.e\., https\://<console IP or FQDN>
**username** |  required  | string | Username to log into the console
**password** |  required  | password | Password for the username

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[get profiles](#action-get-profiles) - Return available operating system profiles from Trellix console  
[detonate file](#action-detonate-file) - Run a file in the sandbox and retrieve the analysis results  
[detonate url](#action-detonate-url) - Run a URL in the sandbox  
[get report](#action-get-report) - Get results of an already completed detonation  
[save artifacts](#action-save-artifacts) - Save a ZIP file of the detonation report to the Vault  
[get status](#action-get-status) - Gets the status of a detonation report  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'get profiles'
Return available operating system profiles from Trellix console

Type: **generic**  
Read only: **False**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action\_result\.data\.\*\.entity\.sensors\.\*\.profiles\.\*\.name | string |  |  
action\_result\.status | string |  |  
action\_result\.message | string |  |  
action\_result\.summary | string |  |  
summary\.total\_objects | numeric |  |   1 
summary\.total\_objects\_successful | numeric |  |   1   

## action: 'detonate file'
Run a file in the sandbox and retrieve the analysis results

Type: **generic**  
Read only: **False**

Detonate a file in the AX console\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**vault\_id** |  required  | Vault ID of the file to detonate | string |  `pe file`  `pdf`  `flash`  `apk`  `jar`  `doc`  `xls`  `ppt`  `vault id` 
**priority** |  required  | Sets the analysis priority, default is Normal | string | 
**analysis\_type** |  required  | Specifies the analysis mode | string | 
**force** |  optional  | Perform an analysis on the file even if the file exactly matches an analysis that has already been performed on this file | boolean | 
**prefetch** |  optional  | Determine the file target based on an internal determination rather than browsing to the target location | boolean | 
**enable\_vnc** |  optional  | Enable VNC while submitting on a Malware Analysis appliance, default is False | boolean | 
**profile** |  required  | Input the Malware Analysis profile to use for analysis | string | 
**custom\_profile** |  optional  | Manually input the Malware Analysis profile to use for analysis\. Please use get profiles action for available options | string | 
**application** |  required  | Specifies the ID of the application to be used for the analysis | string | 
**timeout** |  required  | Specifies the timeout period for the analysis in seconds | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action\_result\.parameter\.vault\_id | string |  `pe file`  `pdf`  `flash`  `apk`  `jar`  `doc`  `xls`  `ppt`  `vault id`  |  
action\_result\.parameter\.priority | string |  |  
action\_result\.parameter\.analysis\_type | string |  |  
action\_result\.parameter\.force | boolean |  |   True  False 
action\_result\.parameter\.prefetch | boolean |  |   True  False 
action\_result\.parameter\.enable\_vnc | boolean |  |   True  False 
action\_result\.parameter\.profile | string |  |   win7\-sp1 
action\_result\.parameter\.custom\_profile | string |  |  
action\_result\.parameter\.application | string |  |   Adobe Reader 10\.0 
action\_result\.parameter\.timeout | numeric |  |   1 
action\_result\.data\.\*\.submission\_details\.\*\.id | numeric |  `fireeyeax submission id`  |  
action\_result\.data\.\*\.submission\_details\.\*\.uuid | string |  `fireeyeax submission uuid`  |  
action\_result\.data\.\*\.submission\_details\.\*\.vnc\_port | numeric |  |   8080 
action\_result\.data\.\*\.id | numeric |  |  
action\_result\.status | string |  |   success  failed 
action\_result\.message | string |  |  
action\_result\.summary | string |  |  
summary\.total\_objects | numeric |  |   1 
summary\.total\_objects\_successful | numeric |  |   1   

## action: 'detonate url'
Run a URL in the sandbox

Type: **generic**  
Read only: **False**

Detonate a URL in the AX console\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**urls** |  required  | URL\(s\) to detonate\. Comma\-separated list allowed | string |  `url` 
**priority** |  required  | Sets the analysis priority, default is Normal | string | 
**analysis\_type** |  required  | Specifies the analysis mode | string | 
**force** |  optional  | Perform an analysis on the file even if the file exactly matches an analysis that has already been performed on this file | boolean | 
**prefetch** |  optional  | Determine the file target based on an internal determination rather than browsing to the target location | boolean | 
**enable\_vnc** |  optional  | Enable VNC while submitting on a Malware Analysis appliance, default is False | boolean | 
**profile** |  required  | Input the Malware Analysis profile to use for analysis\. Please use get profiles action for available options | string | 
**custom\_profile** |  optional  | Manually input the Malware Analysis profile to use for analysis\. Please use get profiles action for available options | string | 
**application** |  required  | Specifies the ID of the application to be used for the analysis | string | 
**timeout** |  required  | Specifies the timeout period for the analysis in seconds | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action\_result\.parameter\.urls | string |  `url`  |  
action\_result\.parameter\.priority | string |  |  
action\_result\.parameter\.analysis\_type | string |  |  
action\_result\.parameter\.force | boolean |  |   True  False 
action\_result\.parameter\.prefetch | boolean |  |   True  False 
action\_result\.parameter\.enable\_vnc | boolean |  |   True  False 
action\_result\.parameter\.profile | string |  |   win7\-sp1 
action\_result\.parameter\.custom\_profile | string |  |  
action\_result\.parameter\.application | string |  |   Adobe Reader 10\.0 
action\_result\.parameter\.timeout | numeric |  |   1 
action\_result\.data\.\*\.submission\_details\.\*\.id | string |  `fireeyeax submission id`  |  
action\_result\.data\.\*\.submission\_details\.\*\.job\_ids | string |  |  
action\_result\.data\.\*\.submission\_details\.\*\.uuid | string |  `fireeyeax submission uuid`  |  
action\_result\.data\.\*\.submission\_details\.\*\.vnc\_port | numeric |  |   8080 
action\_result\.data\.\*\.id | numeric |  |  
action\_result\.status | string |  |   success  failed 
action\_result\.message | string |  |  
action\_result\.summary | string |  |  
summary\.total\_objects | numeric |  |  
summary\.total\_objects\_successful | numeric |  |    

## action: 'get report'
Get results of an already completed detonation

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Detonation ID to get the report of | string |  `fireeyeax submission id` 
**extended** |  optional  | Get additional information from the console about this report | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action\_result\.parameter\.id | string |  `fireeyeax submission id`  |  
action\_result\.parameter\.extended | boolean |  |   True  False 
action\_result\.data\.\*\.alert\.\*\.malicious | string |  |  
action\_result\.data\.\*\.alert\.\*\.severity | string |  |  
action\_result\.data\.\*\.alert\.\*\.uuid | string |  `fireeyeax submission uuid`  |  
action\_result\.status | string |  |   success  failed 
action\_result\.message | string |  |  
action\_result\.summary | string |  |  
summary\.total\_objects | numeric |  |   1 
summary\.total\_objects\_successful | numeric |  |   1 
action\_result\.status | string |  |   success  failed 
action\_result\.data\.\*\.alert\.\*\.malicious | string |  |  
action\_result\.data\.\*\.alert\.\*\.explanation\.malwareDetected\.malware\.\*\.sha256 | string |  |  
action\_result\.data\.\*\.alert\.\*\.explanation\.malwareDetected\.malware\.1\.original | string |  |    

## action: 'save artifacts'
Save a ZIP file of the detonation report to the Vault

Type: **investigate**  
Read only: **True**

This action downloads all the malware artifacts from a detonation as a ZIP file and adds that file to the vault\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**uuid** |  required  | UUID of detonation to get the results of | string |  `fireeyeax submission uuid` 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action\_result\.parameter\.uuid | string |  `fireeyeax submission uuid`  |  
action\_result\.data | string |  |  
action\_result\.status | string |  |   success  failed 
action\_result\.message | string |  |  
action\_result\.summary | string |  |  
summary\.total\_objects | numeric |  |   1 
summary\.total\_objects\_successful | numeric |  |   1   

## action: 'get status'
Gets the status of a detonation report

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Submission ID of the detonation report to get the status of | string |  `fireeyeax submission id` 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action\_result\.parameter\.id | string |  `fireeyeax submission id`  |   12345 
action\_result\.data\.\*\.analysisStatus | string |  |   In Progress  Done  Submission not found 
action\_result\.data\.\*\.submissionStatus | string |  |   running  done 
action\_result\.data\.\*\.verdict | string |  |   malicious  non\-malicious 
action\_result\.data\.\*\.submission\_details\.\*\.vnc\_port | numeric |  |   8080 
action\_result\.data\.\*\.submission\_details\.\*\.job\_ids | string |  |  
action\_result\.data\.\*\.submission\_details\.\*\.uuid | string |  `fireeyeax submission uuid`  |  
action\_result\.data\.\*\.submission\_details\.\*\.id | string |  `fireeyeax submission id`  |   12345 
action\_result\.status | string |  |   success  failed 
action\_result\.message | string |  |  
action\_result\.summary | string |  |  
summary\.total\_objects | numeric |  |   1 
summary\.total\_objects\_successful | numeric |  |   1 