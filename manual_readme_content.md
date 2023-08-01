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
