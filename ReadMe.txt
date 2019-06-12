Markus Scholtes, 2018/03/27

There is only one possibility to export and import firewall rules: as a blob
(wfw file) in the firewall console or with a script. If you want to automate
removing or editing a rule from the set there is no (easy) way to do it without
using a third party tool or messing with the registry in dangerous places.

The three scripts ExportFirewallRules.ps1, ImportFirewallRules.ps1 and
RemoveFirewallRules.ps1 export, import and remove complete firewall rule sets in
CSV or JSON file format. When importing existing rules with the same display
name will be overwritten.

Requires Powershell V4 or above.



Export-FirewallRules.ps1 [[-Name] <Object>] [[-CSVFile] <Object>] [-JSON]

Exports firewall rules to a CSV or JSON file.

-Name
Display name of the rules to be processed. Wildcard character * is allowed. Default: *
-CSVFile
Output file. Default: .\Firewall.csv
-JSON
Output in JSON instead of CSV format. Default: $FALSE



Import-FirewallRules.ps1 [[-CSVFile] <Object>] [-JSON]

Imports firewall rules from a CSV or JSON file.

-CSVFile
Input file. Default: .\Firewall.csv
-JSON
Input in JSON instead of CSV format. Default: $FALSE



Remove-FirewallRules.ps1 [[-CSVFile] <Object>] [-JSON]

Remove firewall rules according to the list in a CSV or JSON file.

-CSVFile
Input file. Default: .\Firewall.csv
-JSON
Input in JSON instead of CSV format. Default: $FALSE



Examples

Export all firewall rules to the CSV file FirewallRules.csv in the current directory:

Export-FirewallRules.ps1


Export all SNMP firewall rules to the JSON file SNMPRules.json:

Export-FirewallRules.ps1 snmp* SNMPRules.json -json



Imports all firewall rules in the CSV file FirewallRules.csv in the current directory:

Import-FirewallRules.ps1


Imports all firewall rules in the JSON file WmiRules.json:

Import-FirewallRules.ps1 WmiRules.json -json



Remarks:

There might be issues when importing rules for "metro apps" to another computer
App packet rules are stored as an SID and usually apply only to user accounts
whose SIDs are stored in the export file. Those rules will not work on another
computer since a SID is unique.