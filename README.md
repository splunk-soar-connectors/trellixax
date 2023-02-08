[comment]: # "Auto-generated SOAR connector documentation"
# Trellix AX

Publisher: Robert Drouin  
Connector Version: 1\.0\.1  
Product Vendor: Trellix  
Product Name: Advanced Malware Analysis  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.9\.39220  

Previously FireEyeAx.
This app provides connectivity to the Trellix Advanced Malware Analysis tool.

[comment]: # " File: readme.md"
[comment]: # ""
[comment]: # "  Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
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
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Advanced Malware Analysis asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Base URL for the console, i\.e\., https\://<console IP or FQDN>
**username** |  required  | string | Username to log into the console
**password** |  required  | password | Password for the username

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[detonate file](#action-detonate-file) - Run a file in the sandbox and retrieve the analysis results  
[detonate url](#action-detonate-url) - Run a URL in the sandbox  
[get report](#action-get-report) - Get results of an already completed detonation  
[save artifacts](#action-save-artifacts) - Save a ZIP file of the detonation report to the Vault  
[get status](#action-get-status) - Gets the status of a detonation report
[get profiles](#action-get-profiles) - Gets the avaliable analysis profiles

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'detonate file'
Run a file in the sandbox and retrieve the analysis results

Type: **generic**  
Read only: **False**

Detonate a file in the AX console\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**vault\_id** |  required  | Vault ID of the file to detonate | string |  `pe file`  `pdf`  `flash`  `apk`  `jar`  `doc`  `xls`  `ppt` 
**priority** |  required  | Sets the analysis priority, default is Normal | string | 
**analysis\_type** |  required  | Specifies the analysis mode | string | 
**force** |  optional  | Perform an analysis on the file even if the file exactly matches an analysis that has already been performed on this file | boolean | 
**prefetch** |  optional  | Determine the file target based on an internal determination rather than browsing to the target location | boolean | 
**enable\_vnc** |  optional  | Enable VNC while submitting on a Malware Analysis appliance, default is False | boolean | 
**profile** |  required  | Select the Malware Analysis profile to use for analysis | string | 
**application** |  required  | Specifies the ID of the application to be used for the analysis | string | 
**timeout** |  required  | Specifies the timeout period for the analysis in seconds | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.vault\_id | string |  `pe file`  `pdf`  `flash`  `apk`  `jar`  `doc`  `xls`  `ppt` 
action\_result\.parameter\.priority | string | 
action\_result\.parameter\.analysis\_type | string | 
action\_result\.parameter\.force | boolean | 
action\_result\.parameter\.prefetch | boolean | 
action\_result\.parameter\.enable\_vnc | boolean | 
action\_result\.parameter\.profile | string | 
action\_result\.parameter\.application | string | 
action\_result\.parameter\.timeout | numeric | 
action\_result\.data\.\*\.submission\_details\.\*\.id | string |  `fireeyeax submission id` 
action\_result\.data\.\*\.submission\_details\.\*\.job\_ids | string | 
action\_result\.data\.\*\.submission\_details\.\*\.uuid | string |  `fireeyeax submission uuid` 
action\_result\.data\.\*\.submission\_details\.\*\.vnc\_port | numeric | 
action\_result\.data\.\*\.id | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

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
**profile** |  required  | Select the Malware Analysis profile to use for analysis | string | 
**application** |  required  | Specifies the ID of the application to be used for the analysis | string | 
**timeout** |  required  | Specifies the timeout period for the analysis in seconds | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.urls | string |  `url` 
action\_result\.parameter\.priority | string | 
action\_result\.parameter\.analysis\_type | string | 
action\_result\.parameter\.force | boolean | 
action\_result\.parameter\.prefetch | boolean | 
action\_result\.parameter\.enable\_vnc | boolean | 
action\_result\.parameter\.profile | string | 
action\_result\.parameter\.application | string | 
action\_result\.parameter\.timeout | numeric | 
action\_result\.data\.\*\.submission\_details\.\*\.id | string |  `fireeyeax submission id` 
action\_result\.data\.\*\.submission\_details\.\*\.job\_ids | string | 
action\_result\.data\.\*\.submission\_details\.\*\.uuid | string |  `fireeyeax submission uuid` 
action\_result\.data\.\*\.submission\_details\.\*\.vnc\_port | numeric | 
action\_result\.data\.\*\.id | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

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
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `fireeyeax submission id` 
action\_result\.parameter\.extended | boolean | 
action\_result\.data\.\*\.alert\.\*\.malicious | string | 
action\_result\.data\.\*\.alert\.\*\.severity | string | 
action\_result\.data\.\*\.alert\.\*\.uuid | string |  `fireeyeax submission uuid` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

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
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.uuid | string |  `fireeyeax submission uuid` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get status'
Gets the status of a detonation report

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Submission ID of the detonation report to get the status of | string |  `fireeyeax submission id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `fireeyeax submission id` 
action\_result\.data\.\*\.analysisStatus | string | 
action\_result\.data\.\*\.submissionStatus | string | 
action\_result\.data\.\*\.verdict | string | 
action\_result\.data\.\*\.submission\_details\.\*\.vnc\_port | numeric | 
action\_result\.data\.\*\.submission\_details\.\*\.job\_ids | string | 
action\_result\.data\.\*\.submission\_details\.\*\.uuid | string |  `fireeyeax submission uuid` 
action\_result\.data\.\*\.submission\_details\.\*\.id | string |  `fireeyeax submission id` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |

## action: 'get profiles'
Read only: **True**
  
### Action Parameters
No parameters are required for this action
  
### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.data\.\*\.entity\.sensors\.\*\.profiles\.\*\.name
