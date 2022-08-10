# Windows Advanced Audit Policy Configuration Guide
- [CIS Recommended Controls](https://downloads.cisecurity.org/#/)
- [Microsoft Recommended Controls](https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/advanced-security-audit-policy-settings)

| Category           	| Sub-Category                                 	| CIS Control         	|                     	| Microsoft Control   	|                     	|                     	|
|--------------------	|----------------------------------------------	|---------------------	|---------------------	|---------------------	|---------------------	|---------------------	|
|                    	|                                              	| Domain Controller   	| Member Server       	| Domain Controller   	| Member Server       	| Workstation         	|
| Account Logon      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Credential Validation                  	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Kerberos Authentication Service        	| Success and Failure 	| *Not Applicable*     	| Success and Failure 	| *Not Applicable*     	| *Not Applicable*     	|
|                    	| Audit Kerberos Service Ticket Operations     	| Success and Failure 	| *Not Applicable*     	| Success and Failure 	| *Not Applicable*     	| *Not Applicable*     	|
|                    	| Audit Other Account Logon Events             	| No Auditing         	| No Auditing         	| No Auditing         	| No Auditing         	| No Auditing         	|
| Account Management 	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Application Group Management           	| Success and Failure 	| Success and Failure 	| *Not Available*     	| *Not Available*     	| *Not Available*     	|
|                    	| Audit Computer Account Management            	| Success             	| Not Applicable       	| Success             	| Not Applicable       	| Not Applicable       	|
|                    	| Audit Distribution Group Management          	| Success             	| Not Applicable       	| Success             	| Not Applicable       	| Not Applicable       	|
|                    	| Audit Other Account Management Events        	| Success             	| Not Applicable       	| Success             	| Not Applicable       	| Not Applicable       	|
|                    	| Audit Security Group Management              	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit User Account Management                	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
| Detailed Tracking  	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit DPAPI Activity                         	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit PNP Activity                           	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Process Creation                       	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Process Termination                    	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit RPC Events                             	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Token Right Adjusted                   	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
| DS Access          	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Detailed Directory Service Replication 	| *Not Available*     	| *Not Available*     	| No Auditing         	| *Not Applicable*     	| *Not Applicable*     	|
|                    	| Audit Directory Service Access               	| Failure             	| *Not Applicable*     	| Failure             	| *Not Applicable*     	| *Not Applicable*     	|
|                    	| Audit Directory Service Changes              	| Success             	| *Not Applicable*     	| Success             	| *Not Applicable*     	| *Not Applicable*     	|
|                    	| Audit Directory Service Replication          	| *Not Available*     	| *Not Available*     	| No Auditing         	| *Not Applicable*     	| *Not Applicable*     	|
| Logon/Logoff       	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Account Lockout                        	| Failure             	| Failure             	| Failure             	| Failure             	| Failure             	|
|                    	| Audit User/Device Claims                     	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit IPsec Extended Mode                    	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Group Membership                       	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit IPsec Main Mode                        	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit IPsec Quick Mode                       	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Logoff                                 	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Logon                                  	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Network Policy Server                  	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Other Logon/Logoff Events              	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Special Logon                          	| Success             	| Success             	| Success             	| Success             	| Success             	|
| Object Access      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Application Generated                  	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Certification Services                 	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Detailed File Share                    	| Failure             	| Failure             	| Failure             	| Failure             	| Failure             	|
|                    	| Audit File Share                             	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit File System                            	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Filtering Platform Connection          	| *Not Available*     	| *Not Available*     	| Failure             	| Failure             	| Failure             	|
|                    	| Audit Filtering Platform Packet Drop         	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Handle Manipulation                    	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Kernel Object                          	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Other Object Access Events             	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Registry                               	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Removable Storage                      	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit SAM                                    	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Central Access Policy Staging          	| *Not Available*     	| *Not Available*     	| Failure             	| Failure             	| Failure             	|
| Policy Change      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Audit Policy Change                    	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Authentication Policy Change           	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Authorization Policy Change            	| Success             	| Success             	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Filtering Platform Policy Change       	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit MPSSVC Rule-Level Policy Change        	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Other Policy Change Events             	| Failure             	| Failure             	| Failure             	| Failure             	| Failure             	|
| Privilege Use      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Non-Sensitive Privilege Use            	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Sensitive Privilege Use                	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Other Privilege Use Events             	| *Not Available*     	| *Not Available*     	| No Auditing         	| No Auditing         	| No Auditing         	|
| System             	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit IPsec Driver                           	| Success and Failure 	| Success and Failure 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Other System Events                    	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Security State Change                  	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Security System Extension              	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit System Integrity                       	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
