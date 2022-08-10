# Windows Advanced Audit Policy Configuration Recommendations

| Category           	| Sub-Category                                 	| CIS Control         	|                     	| Microsoft Control   	|                     	|                     	|
|--------------------	|----------------------------------------------	|---------------------	|---------------------	|---------------------	|---------------------	|---------------------	|
|                    	|                                              	| Domain Controller   	| Member Server       	| Domain Controller   	| Member Server       	| Workstation         	|
| Account Logon      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Credential Validation                  	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Kerberos Authentication Service        	| Success and Failure 	| N/A                 	| Success and Failure 	| N/A                 	| N/A                 	|
|                    	| Audit Kerberos Service Ticket Operations     	| Success and Failure 	| N/A                 	| Success and Failure 	| N/A                 	| N/A                 	|
|                    	| Audit Other Account Logon Events             	| No Auditing         	| No Auditing         	| No Auditing         	| No Auditing         	| No Auditing         	|
| Account Management 	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Application Group Management           	| Success and Failure 	| Success and Failure 	| N/A                 	| N/A                 	| N/A                 	|
|                    	| Audit Computer Account Management            	| Success             	| N/A                 	| Success             	| N/A                 	| N/A                 	|
|                    	| Audit Distribution Group Management          	| Success             	| N/A                 	| Success             	| N/A                 	| N/A                 	|
|                    	| Audit Other Account Management Events        	| Success             	| N/A                 	| Success             	| N/A                 	| N/A                 	|
|                    	| Audit Security Group Management              	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit User Account Management                	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
| Detailed Tracking  	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit DPAPI Activity                         	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit PNP Activity                           	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Process Creation                       	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Process Termination                    	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit RPC Events                             	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Token Right Adjusted                   	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
| DS Access          	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Detailed Directory Service Replication 	| N/A                 	| N/A                 	| No Auditing         	| N/A                 	| N/A                 	|
|                    	| Audit Directory Service Access               	| Failure             	| N/A                 	| Failure             	| N/A                 	| N/A                 	|
|                    	| Audit Directory Service Changes              	| Success             	| N/A                 	| Success             	| N/A                 	| N/A                 	|
|                    	| Audit Directory Service Replication          	| N/A                 	| N/A                 	| No Auditing         	| N/A                 	| N/A                 	|
| Logon/Logoff       	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Account Lockout                        	| Failure             	| Failure             	| Failure             	| Failure             	| Failure             	|
|                    	| Audit User/Device Claims                     	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit IPsec Extended Mode                    	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Group Membership                       	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit IPsec Main Mode                        	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit IPsec Quick Mode                       	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Logoff                                 	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Logon                                  	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Network Policy Server                  	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Other Logon/Logoff Events              	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Special Logon                          	| Success             	| Success             	| Success             	| Success             	| Success             	|
| Object Access      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Application Generated                  	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Certification Services                 	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Detailed File Share                    	| Failure             	| Failure             	| Failure             	| Failure             	| Failure             	|
|                    	| Audit File Share                             	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit File System                            	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Filtering Platform Connection          	| N/A                 	| N/A                 	| Failure             	| Failure             	| Failure             	|
|                    	| Audit Filtering Platform Packet Drop         	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Handle Manipulation                    	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Kernel Object                          	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Other Object Access Events             	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Registry                               	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Removable Storage                      	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit SAM                                    	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Central Access Policy Staging          	| N/A                 	| N/A                 	| Failure             	| Failure             	| Failure             	|
| Policy Change      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Audit Policy Change                    	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Authentication Policy Change           	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Authorization Policy Change            	| Success             	| Success             	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Filtering Platform Policy Change       	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit MPSSVC Rule-Level Policy Change        	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Other Policy Change Events             	| Failure             	| Failure             	| Failure             	| Failure             	| Failure             	|
| Privilege Use      	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit Non-Sensitive Privilege Use            	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Sensitive Privilege Use                	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Other Privilege Use Events             	| N/A                 	| N/A                 	| No Auditing         	| No Auditing         	| No Auditing         	|
| System             	|                                              	|                     	|                     	|                     	|                     	|                     	|
|                    	| Audit IPsec Driver                           	| Success and Failure 	| Success and Failure 	| No Auditing         	| No Auditing         	| No Auditing         	|
|                    	| Audit Other System Events                    	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
|                    	| Audit Security State Change                  	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit Security System Extension              	| Success             	| Success             	| Success             	| Success             	| Success             	|
|                    	| Audit System Integrity                       	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	| Success and Failure 	|
