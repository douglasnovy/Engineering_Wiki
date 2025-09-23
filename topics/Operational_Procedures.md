---
title: Operational_Procedures
consolidated: true
sources: 1
conflicts: 0
confidence: 1.00
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_CopyReportsrsscripter_RSScripterProceduredocx_b431424a.md']  # This would be a timestamp
---

---
author: Brian Perlov
created: 2020-05-28 23:43:00+00:00
modified: 2020-05-28 23:49:00+00:00
source_hash: a5ac1c1ceb7175e9c17f51a2ad8eedc976314520c58e59dd2cb6d322fd055925
source_path: ..\engineering_white_papers\White Papers\Copy Reports rsscripter\RSScripter
  Procedure.docx
title: Standards for Redundant Systemsdoc_type: tool_utility
---

PURPOSE:
To detail the procedure for using RSScripter.exe to transfer reports from one database to another or copy reports from one source to another.
KEY CONSIDERATIONS:
Server will need .NET 3.5 features enabled. This can be done through server manager and should already be done if the SQL and StackVision are on the same server.
RSScripter.exe must be run on the SQL report server in cases of split servers.
ISSUE:
Reports are created on a test server and need to be transferred to a production server.
Reports are created from one unit and the same reports are needed on other units.
IMPLEMENTATION DETAILS:
Launch RSScripter.exe from RSScripter folder
Click “Options” and change “Report” options to below:
Change Report Server to latest version in the drop-down list (Typically does not need to match actual SQL version on server unless unable to retrieve catalog).
Click “Get Catalog”
Expand the folder full of linked reports and select reports you want to script out
Change output to desired folder
Click “Script”
Navigate to output folder and edit “RS Scripter Load All Items.cmd” in notepad
Type in the file path on “SET SCRIPTLOCATION=” to the path where the “RS Scripter Load All Items.cmd” file is located
Type in the file path of “SET RS=” to the path where RS.EXE is located on the server. You may have to search through a few folders to find RS.EXE. The executable should be located in <Drive>:Program Files\Microsoft SQL Server\*Typically highest number in folder (usually around 100)*\Tools\Binn folder
If copying reports from one unit to another, change report source name in any of the “.rss” files as desired using find and replace.
Run “RS Scripter Load All Items.bat” on the server the reports need to be moved to.
Check “RS Scripter Load Log.txt” to make sure all commands completed successfully.
TROUBLESHOOTING:
Check the “RS Scripter Load Log.txt” file for errors. Typical errors involve not being able to find the file path. Double check the SET SCRIPTLOCATION in step 10.
Do NOT use the em dash “—“ or en dash “–“ in the titles for any reports. Use hyphen “-“ instead. Using the em dash or en dash results in the batch file not functioning as the .rss files cannot be found.
REVISION HISTORY: