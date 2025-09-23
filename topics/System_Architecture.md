---
title: System_Architecture
consolidated: true
sources: 1
conflicts: 0
confidence: 1.00
generated: ['data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_CemRC_System_Resourcespdf_fd5a76aa.md']  # This would be a timestamp
---

---
author: Gloria Borum
created: '2025-08-11T10:26:58.678131'
modified: '2023-06-06T11:20:01'
source_hash: 906aee25774fe0c4d883b3af518d2550d38fc4525648f7904fac3a67bc0d0188
source_path: C:\Users\dnovy\OneDrive - ESC\Training Materials\Reference Documents\Cem.RC_System_Resources.pdf
title: "E-DAS EMR for Windows User\u2019s Guide (Part 75/NBP)"doc_type: tool_utility
---

User’s Guide
Appendix A System Resources
System Resources
Why are System Resources provided?
System resources are used to customize system operations to meet the specific requirements of a
particular site. Additionally, when operational changes occur at a site, it may become necessary to
change the value of a resource variable to reflect the new operational environment.
What are System Resources?
System resources are variables that are defined in the system’s cem.rc file. They are accessed by
many of the programs in the EMR system, most often at times when configuration information is
required.
How to configure System Resources
Resource variables are specified in resource files that are located in the config directory. To con-
figure a resource variable you would change the value of the variable in the appropriate resource
file. The file Basic.cem.rc is provided in the misc folder as a resource template file to facilitate
this process.
WARNING
Resources should only be changed in consultation with ESC because chang-
ing them may have unforeseen consequences on the EMR software.
A resource can be either a “system resource” (of system-wide scope, affecting every user) or a
“user resource” (affecting a particular user only). A system resource is specified in the resource
file named cem.rc. A user resource is specified in resource files that have names of the form
<login_name>.rc.
Resource files can be edited/created using a text editor, such as Microsoft Wordpad and Winvi32.
Only the DAS manager (System Administrator) is authorized to modify these files, and as indi-
cated above, this should only be done in consultation with ESC.
WARNING
Microsoft Notepad is not suitable for editing resource files.
From the Main Menu, choose one of the Main Menu paths below.
Part 60 Only Users:
System Administration J System Configuration J Resource Configuration Editors J Edit
misc/Basic.cem.rc Resources (OSR5 Only)
System Administration J System Configuration J Resource Configuration Editors J Edit
config/cem.rc Resources (OSR5 Only)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-3
User’s Guide
Appendix A System Resources
OR
Part 60 Add-on Users: Configuration J Resource Configuration Editors J Edit
misc/Basic.cem.rc Resources (OSR5 Only)
Configuration J Resource Configuration Editors J Edit config/cem.rc Resources (OSR5
Only)
When a resource is defined in both the system resource file and a user resource file, the user re-
source file overrides the system resource file. Within one resource file, if a variable is defined
more than once, the last definition is used.
A resource variable is considered to be “commented-out” if the first column of the resource speci-
fication line is the # character. For example, in the resource specification line:
#ALM_ACK_PASSWORD_REQUIRED=TRUE
the ALM_ACK_PASSWORD_REQUIRED resource variable has been “commented-out.” Com-
mented-out variable specification lines are ignored by the system. They are present in the re-
source file for documentation purposes and to facilitate making a change to the resource value at
a later time. If a program finds that its resource variable is not commented-out, it will use the re-
source variable. If a program’s resource variable is commented-out, it will ignore the resource
variable and use its own defaults. Program defaults for the various resource variables are docu-
mented later in this section where the various resource variables available are presented.
Some resource variables are configured with default values. If you want to use a value other than
the default, make a copy of the line that currently specifies the variable value and make the de-
sired change to this copied resource variable line. Comment out the original resource definition
line, thereby retaining the original variable-specification line to document the original definition).
Some resource variables are already commented out. To activate a commented-out resource vari-
able, make a copy of the line that that is currently commented out and then remove the # charac-
ter from the copied line.
System Resources
System resource variables are global (are of system-wide scope, affecting every user). This cate-
gory of resources includes variables for customizing the system in areas such as system configu-
ration, polling/data logger operations, alarms, hourly data validation, data editors, EDR genera-
tion, BAF configuration, graphing, math pack configuration, missing data substitution, daily re-
cord utilities, reports, Postscript printers, Appendix D and E, and 40 CFR 60 software.
The System Resources are categorized and described below, including example settings and pro-
gram defaults that apply if the resource variable is missing or commented out. Note that some of
these resources are no longer applicable in the current release of the software but have been re-
tained in this document for historical purposes in support of users who may have configured them
for use in a past release of the software. Therefore, before you change any system resource, you
should first consult all related user’s guide chapters that describe functions that potentially make
use of the resource. These chapters will contain the current instructions relative to configuration
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-4
User’s Guide
Appendix A System Resources
of appropriate resources for the function. Since a single resource can be employed by multiple
functions, it is recommended that resources only be changed in consultation with ESC.
System Configuration Resources
These resource variables define various aspects of system configuration. It is recommended that
these variables not be commented-out because they provide vital configuration values that are re-
lated to system performance.
Resource syntax/example
Resource description
Used by
Default, if ap-
plicable
CFG_DISK_MARGIN =
C:20,D:15
Configures which filesystems are
checked for disk space and the % of
free space at which alarm messages
will be dispatched to warn users that
the disk is approaching capacity. If a
margin is specified without a file
system specification, the resource
will be ignored and no disk-full
warnings will occur.
In the example, disk-full warning
messages will be dispatched when
the C: file system is at 80% capacity
or when the D: file system is at 85%
capacity.
The resource is used by the Kernel
Supervisor (ksuper).
• Kernel Supervisor (ksu-
per)
No filesystems
are checked and
no alarms are
dispatched rela-
tive to disk ca-
pacity
CFG_QUEUE_IDLE_MIN =
Configures the number of idle min-
utes on a message queue before the
kernel supervisor (ksuper) deems it
in need of removal.
• Kernel Supervisor (ksu-
per)
CFG_QUEUE_MARGIN =
Configures the maximum allocation
of bytes per message queue that is
allowed before notification of a
queue filling up.
The resource is used by the Kernel
Supervisor (ksuper).
• Kernel Supervisor (ksu-
per)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-5
User’s Guide
Appendix A System Resources
Polling/Logger Resources
These resource variables configure different aspects related to the polling subsystem.
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
DFL_FPOLL_EVENTS =
<data types>
Example:
DFL_FPOLL_EVENTS =
AUX,MIN,HR,ILS
Configures the data types to be
polled by the fast poll manager
when CemStart is invoked.
See chapter “Polling/Logger Opera-
tions” (Part 4) for details.
• Kernel Startup (Cem-
Start)
The MIN, AUX,
HR, ILS polling
events
CATCHUP_LIMIT = <num-
ber of commands>
Example:
CATCHUP_LIMIT = 5
Configures the polling break, i.e.,
the maximum number of manual or
automatic poll commands that can
be handled at one pass before check-
ing for and allowing higher-priority
polls to be processed. It should be a
low number for optimum system
performance, i.e., a low number will
make possible the catch-up and
manual polling of large blocks of
data. Note that this variable should
be configured if you would attain
maximum system performance.
See “Polling/Logger Operations” for
details.
• Polling Task (polltsk)
POLL_MAX_RETRY =
<number of retries>
Example:
POLL_MAX_RETRY = 3
Configures the number of retries for
data polling before an error message
is generated and the logger interface
attempt is aborted. Each retry takes
about 5 seconds.
See “Polling/Logger Operations” for
details.
• Polling Task (polltsk)
LOAD_MAX_RETRY =
<number of retries>
Example:
LOAD_MAX_RETRY = 5
Configures the same usage as
POLL_MAX_RETRY except that
this resource is only used for table
downloading to a logger.
See “Polling/Logger Operations” for
details.
• Polling Task (polltsk)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-6
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
COM_ERROR_
SHUTDOWN = <maximum
errors>
Example:
COM_ERROR_
SHUTDOWN = 15
When communication errors occur
in a polling line, the other polling
lines are influenced and tend to slow
down when the system tries to poll
again. If a communication error
occurs in normal situations (and is
detected by the user), the user can
immediately investigate and resolve
the problem and polling can resume.
In some instances, however, e.g.,
over a weekend, communication
errors occur when no one is avail-
able to handle the problem right
away.
To alleviate this type of problem, a
resource called COM_ERROR_
SHUTDOWN is available that al-
lows users to set up the number of
communication errors allowed be-
fore polling goes into hibernation
mode. If the number of communica-
tion errors for a polling line be-
comes equal to or exceeds the re-
source value, polling for the logger
will be suspended for five minutes.
After this five-minute suspension,
the system will recheck the commu-
nication condition by attempting to
poll again. If polling is still unsuc-
cessful, the system will suspend
polling again and the wait time will
be increased by five minutes, i.e.,
polling will be attempted again in 10
minutes. Each time communication
fails, five minutes will be added to
the wait time. To force a polling
retry, the E-DAS kernel must be
stopped and restarted.
In some cases, this polling hiberna-
tion mode may not be adequate, e.g.,
during troubleshooting for a com-
munication line. In these situations,
communication failure and retry are
expected and desired so that the
problem can be resolved as soon as
possible. To prevent polling from
going into hibernation mode, the
resource value should be set to an
extremely large number, e.g.,
See “Polling/Logger Operations” for
details.
• Polling Task (polltsk)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-7
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
RC_STARTUP = <reason
code for data bearing the
startup data mask (i.e., data
collected during unit
startup)>
Example:
RC_STARTUP = 01
For polled data, this variable, which
is usually commented-out, config-
ures a system-wide reason code to
be automatically applied to polled
data values that bear the startup data
mask.
In the Minute to Hour Calculation
Tool, if STARTUP flag is set on any
minute data that is used in the
hourly calculation, this resource
may be used to specify the reason
code to be stored on the hourly data.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold))
• Hourly Rolling Average
Tool (hrrolavg)
• Minute to Hour Calcula-
tion Tool (m2hr)
No reason code
will be auto-
matically ap-
plied to data
RC_SHUTDOWN = <reason
code for invalid and ex-
ceedance data bearing the
shutdown data mask (i.e.,
data collected during unit
shutdown)>
Example:
RC_SHUTDOWN = 02
For polled data, this variable, which
is usually commented-out, config-
ures a system-wide reason code to
be automatically applied to polled
data values that bear the shutdown
data mask.
In the Minute to Hour Calculation
Tool, if SHUTDOWN flag is set on
any minute data that is used in the
hourly calculation, this resource
may be used to specify the reason
code to be stored on the hourly data.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
• Hourly Rolling Average
Tool (hrrolavg)
• Minute-to-Hour Calcu-
lation Tool (m2hr)
No reason code
will be auto-
matically ap-
plied to data
RC_CALIBRATION = <rea-
son code for data bearing the
calibration logger flag>
Example:
RC_CALIBRATION = 12
This variable, which is usually
commented-out, configures a sys-
tem-wide reason code to be auto-
matically applied to polled data
values that bear calibration logger
flag.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
• Minute-to-Hour Calcu-
lation Tool (m2hr)
No reason code
will be auto-
matically ap-
plied to data
RC_PROCESSDOWN =
<reason code for invalid data
collected while the unit is
down>
Example:
RC_PROCESSDOWN = 03
This variable, which is usually
commented-out, configures a sys-
tem-wide reason code to be auto-
matically applied to polled data
values for invalid data collected
while the unit is down.
If the resource is defined, the con-
figured reason code will be applied
automatically to data bearing the
“F” (boiler offline) data logger flag.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
• Minute-to-Hour Calcu-
lation Tool (m2hr)
No reason code
will be auto-
matically ap-
plied to data
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-8
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
AC_STARTUP = <action
code for data bearing the
startup data mask (i.e., data
collected during unit
startup)>
Example:
AC_STARTUP = 01
This variable, which is usually
commented-out, configures a sys-
tem-wide action code to be auto-
matically applied to polled data
values that bear the startup data
mask.
In the Minute to Hour Calculation
Tool, if STARTUP flag is set on any
minute data that is used in the
hourly calculation, this resource
may be used to specify the action
code to be stored on the hourly data.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
• Hourly Rolling Average
Tool (hrrolavg)
• Minute-to-Hour Calcu-
lation Tool (m2hr)
No action code
will be auto-
matically ap-
plied to data
AC_SHUTDOWN = <action
code for invalid and ex-
ceedance data bearing the
shutdown data mask (i.e.,
data collected during unit
shutdown)>
Example:
AC_SHUTDOWN = 02
This variable, which is usually
commented-out, configures a sys-
tem-wide action code to be auto-
matically applied to polled data
values that bear the shutdown data
mask.
In the Minute to Hour Calculation
Tool, if SHUTDOWN flag is set on
any minute data that is used in the
hourly calculation, this resource
may be used to specify the action
code to be stored on the hourly data.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
• Hourly Rolling Average
Tool (hrrolavg)
• Minute-to-Hour Calcu-
lation Tool (m2hr)
No action code
will be auto-
matically ap-
plied to data
AC_CALIBRATION = <ac-
tion code for data bearing the
calibration logger flag>
Example:
AC_CALIBRATION = 08
This variable, which is usually
commented-out, configures a sys-
tem-wide action code to be auto-
matically applied to polled data
bearing the calibration logger flag.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
• Minute-to-Hour Calcu-
lation Tool (m2hr)
No action code
will be auto-
matically ap-
plied to data
AC_PROCESSDOWN =
<action code for invalid data
collected while the unit is
down>
Example:
AC_PROCESSDOWN = 04
This variable, which is usually
commented-out, configures a sys-
tem-wide action code to be auto-
matically applied to polled data
values code for invalid data col-
lected while the unit is down.
If the resource is defined the config-
ured action code will be applied
automatically to data bearing the
“F” (boiler offline) data logger flag.
See “Polling/Logger Operations” for
details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
• Minute-to-Hour Calcu-
lation Tool (m2hr)
No action code
will be auto-
matically ap-
plied to data
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-9
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
AC_STARTUP_INVALID =
<action code for invalid data
collected during unit startup>
Example:
AC_STARTUP_INVALID =
This variable, which is usually
commented-out, configures a sys-
tem-wide action code to be auto-
matically applied to polled data
values for invalid data collected
during unit startup.
See chapter “Polling/Logger Opera-
tions” for more details.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
No action code
will be auto-
matically ap-
plied to data
AC_SHUTDOWN_
INVALID = <action code for
invalid data collected during
unit shutdown>
Example:
AC_SHUTDOWN_
INVALID = 06
This variable, which is usually
commented-out, configures a sys-
tem-wide action code to be auto-
matically applied to polled data
values for invalid data collected
during unit shutdown.
• Database Update Man-
ager (dbsupdmgr)
• Process Old Response
Files (procold)
No action code
will be auto-
matically ap-
plied to data
CEM_OPTS_STMIN =
<minutes>
where minutes is 0, 1, or 2
Example:
CEM_OPTS_STMIN = 2
Configure how minute data is to be
stored. If 0, no minute data will be
stored. If 1, only dbs data will be
stored. If 2, both dbs data and
rawdbs data will be stored.
See Part 7 of this user’s guide for
details.
• Database Update Man-
ager (dbsupdmgr)
• Auxiliary Data Editor
(auxdatedt)
will be stored)
ILS_WRITE_TO_DBS =
{TRUE | FALSE}
Example:
ILS_WRITE_TO_DBS =
FALSE
Input Line Status Change: Because
the ILS database files often contain
unnecessary information, resources
are available that will allow the user
to control what information is stored
in the ILS database. If this resource
is set to FALSE, no ILS data polled
will be stored in the database.
• Database Update Man-
ager (dbsupdmgr)
TRUE
ILS_DONT_SAVE_
<loggername> = <line num-
ber list>
or
ILS_DONT_SAVE = <line
number list>
Example:
ILS_DONT_SAVE_LOG01
= 11,12,13
Input Line Status Change: Because
the ILS database files often contain
unnecessary information, resources
are available that will allow the user
to control what information is stored
in the ILS database. If the
ILS_WRITE_TO_DBS resource is
not set to FALSE, this logger-
specific resource (or generic re-
source if no logger-specific resource
is defined) will be read to get the list
of ILS line numbers that should
NOT have status changes stored in
the ILS database.
• Database Update Man-
ager (dbsupdmgr)
None
CEM_OPTS_DBASE = <da-
tabase option>
Example:
CEM_OPTS_DBASE = 2
Configure database option. If 0, data
will be in the dbs directory only. Set
to 2 if using a dual database system
(both rawdbs and dbs). See “Poll-
ing/Logger Operations” for details.
• Database Update Man-
ager (dbsupdmgr)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-10
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
TIME_SYNC_LOGGER =
{TRUE | FALSE}
TIME_SYNC_LOGGER_
<data logger> = {TRUE |
FALSE}
Example:
TIME_SYNC_LOGGER_LO
G01 = FALSE
By default, before downloading any
table, the central system will syn-
chronize the central and data logger
times. If, for some reason, the clocks
should not be synchronized, this
resource can be set to turn off time
synchronization. The time will NOT
be synchronized if the resource is
set to FALSE.
See “Polling/Logger Operations” for
details.
• Logger Tables Down-
loading (dldriver)
TRUE (the
times WILL be
synchronized)
CEM_MSITES_PER_
LOGGER = {TRUE | FALSE}
Example:
CEM_MSITES_PER_
LOGGER = TRUE
Configure this resource to TRUE if
there are multiple sites using one
data logger and you want the load-
table program to download the site
name with each channel download.
See “Polling/Logger Operations” for
details.
NOTE: If this is TRUE, all equations
must have parameters fully speci-
fied. E.g., STACKON:UNIT1 in-
stead of just STACKON.
• Logger Tables
Downloading (loadta-
ble)
FALSE (there is
no need to send
the site name to
the logger so
spaces are sent)
TBL_LOAD_WAIT =
<seconds to wait>
Example:
TBL_LOAD_WAIT = 15
When “Download all Tables” is
executed, data logger memory must
be defragmented after some tables
are downloaded. When the data
logger is defragmenting memory,
the loadtable program must pause
for a few seconds to allow the log-
ger to reboot. This resource can be
used to configure the number of
seconds to wait for logger reboot.
See “Polling/Logger Operations” for
details.
• Logger Tables
Downloading (loadta-
ble)
CLIENTLOGGERACCESS
Examples:
CLIENTLOGGERACCESS
= das
CLIENTLOGGERACCESS
= das, opr1
CLIENTLOGGERACCESS
= ALL
Used to specify which user(s) have
access to the following data logger
functions from the Client software:
logger enabling/ disabling, tables
downloading, emulation, clock syn-
chronization, and memory defrag-
mentation.
Also controls which users can
stop/start the kernel.
Only the das user can access the
logger and kernel control functions
(default).
Only das and opr1 users can access
logger and kernel control functions.
All users can access the logger and
kernel control functions from the
Client.
• Data Logger Tool Box
(vbloggertb)
• Kernel Control Tool
Box (vbkerneltb)
das
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-11
User’s Guide
Appendix A System Resources
Hourly Data Validation Resources
Resource syntax/example
Resource description
Used By
Default, if
applicable
HR_VAL_NORC = {TRUE | FALSE}
HR_VAL_NOAC = {TRUE |
FALSE}
If configured to be TRUE, the
hourly data reason/action
codes are selected by looking
at the codes assigned to the
minute data. If configured to
be FALSE, the codes are
whatever the Data Logger
sends.
• Hourly Data
Validation
Tool (hrdatval)
-- Padep
• Minute-to-
Hour Tool
(mintohr) --
Padep
• Minute-to-
Hour Tool
(mintohour) --
TVA
TRUE
HR_VAL_PERCENT = <percent-
age>
Example:
HR_VAL_PERCENT = 75
Configure percentage of good
minute data required to make
a valid hour.
• Hourly Data
Validation
Tool (hrdatval)
--Padep
• Minute-to-
Hour Tool
(mintohr) --
Padep
• Minute-to-
Hour Tool
(mintohour) --
TVA
Command Line Interface Resources
Resource syntax/example
Resource description
Used By
Default, if
applicable
VBCLI_FILTERSELECTEDPARMS
= {TRUE | FALSE}
Example:
VBCLI_FILTERSELECTEDPARMS
= TRUE
Indicates whether only the
parameters passed in on the
command line, should be
shown in the Parameter Pick-
list. This resource is only
considered when a PLF is
passed in by the command
line.
•
vbcli
FALSE
VBCLI_PLFTYPES = <file type list>
Examples:
VBCLI_PLFTYPES = *.p, * P*
VBCLI_PLFTYPES = *.*
File types to be shown when
Select Parameter List File is
chosen from the vbcli menu.
Allows wildcards. May use a
comma-delimited list of file
types.
•
vbcli
*.p
Graph Resources
Resource syntax/
example
Resource description
Used By
Default, if ap-
plicable
GRAPH_POLL_
DELAY = <number_ of_seconds>
Example:
GRAPH_POLL_
DELAY = 20
Configure the number of sec-
onds after the top of the min-
ute to “look” for new data. In
heavily configured systems, it
may be necessary to set this as
high as 59 seconds.
• E-DAS API
• E-DAS to PI
Interface
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-12
User’s Guide
Appendix A System Resources
Data Editor Resources
These resource variables are used to configure access to the monthly, daily, hourly, auxiliary,
seconds, and calibration data through the Data Editors.
Resource syntax/example
Resource description
Used By
Default, if appli-
cable
DATA_EDITOR_
PRECISION = {TRUE | FALSE}
Example:
DATA_EDITOR_
PRECISION = TRUE
A setting of TRUE allows the
“Decimal Position” field in the
Site/Parameter file to be used to
determine precision when displaying
values for a parameter. If this re-
source is FALSE or not configured,
the precision of displayed values
defaults to 4. This precision is used
by the query option’s relational
operators.
See the “Data Editors” chapter for
details.
• Hourly Data
Editor (hrdat-
edt)
FALSE. The
Hourly Data Editor
will display values
with four-decimal
precision.
Advanced Custom Report Tool Resource
Resource syntax/example
Resource description
Used by
Default, if appli-
cable
EDITOR
Specifies which text editor to use
when editing an advanced custom
report driver file.
•
Advanced
Custom Report
Tool
winvi32
Alarm Resources
These resource variables configure aspects of the alarm subsystem such as how the alarm ac-
knowledger works, the content of alarm messages, and reason and action code defaults for differ-
ent alarms. See the “Alarm System” chapter in Part 4 of this user’s guide for details.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-13
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Used by
Default, if ap-
plicable
ALM_FORMAT_ACKER =
<format>
ALM_FORMAT_ALMSTAT
= <format>
ALM_FORMAT_
OCRIBBON = <format>
ALM_FORMAT_EVENT =
<format>
where “format” is defined
according to the section below
entitled “Alarm Message
Format Designators”
Examples:
See section below entitled
“Alarm Message Format Des-
ignators.”
Configure the format of alarm mes-
sages displayed by the alarm ac-
knowledgement utility (unacknow-
ledged alarms)
or
the Outstanding Alarm Status Dis-
play (the display in the Real-Time
Data Menu of alarms that have not
returned to normal) or in the graphi-
cal main menu window
or
the operator console ribbon and at
the bottom of the screen
or
the alarm manager (alarmmgr).
• Alarm Acknowledgers
(Xalarmack, alarmack)
• Outstanding Alarm
Status Display (Xalm-
stat)
• Historical Hourly Data
Graphics (graphhist)
• Real-Time (Minute)
Trending Graphics
(graphrt)
• Menu Drivers (xw_
mnudrv, mnudrv)
• Alarm Manager
(alarmmgr)
See section be-
low entitled
“Alarm Message
Format Designa-
tors”
ALM_ACK_PASSWORD_
REQUIRED = {TRUE |
FALSE}
Example:
ALM_ACK_PASSWORD_
REQUIRED = TRUE
Configure whether a user must enter
a password to acknowledge alarms.
This resource is used when a user
selects the Acknowledge button. If
this variable is TRUE, users will be
prompted to enter their password
when they invoke the alarm ac-
knowledgement function.
• X Windows Menu
Driver (xw_mnudrv)
FALSE (users
will not be
prompted to
enter their pass-
word when they
invoke the alarm
acknowledege-
ment function).
ALM_ACK_RTNS = {TRUE
| FALSE}
Example:
ALM_ACK_RTNS = TRUE
ALM_ACK_RTNS, if set to TRUE,
allows you to acknowledge return-
to-normal events as well as alarm
events.
NOTE: Because the ALM_ACK_RTN
resource affects a kernel process
(alarmmgr), changing it to TRUE
without first resolving all alarms
and restarting the kernel will result
in unresolvable alarm records.
• Alarm Acknowledgers
(Xalarmack, alarmack)
• Archived Alarm Log
Report (almarcrpt)
• Alarm Database Utility
(almdbsctl)
• Alarm Record Report
(almrecrpt)
• Alarm Export Tool
(almexport)
FALSE (return-
to-normal events
do not require
acknowledge-
ment).
ALM_MAINTENANCE =
{TRUE | FALSE}
Example:
ALM_MAINTENANCE =
FALSE
Set to FALSE if you do not want
alarms during maintenance periods.
• Database Update Man-
ager (dbsupdmgr)
TRUE (get
alarms during
maintenance
periods)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-14
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used by
plicable
ALARM_DURING_CAL =
{TRUE | FALSE}
Example:
ALARM_DURING_CAL =
TRUE
Configure whether a parameter will
have alarms occur during calibra-
tions.
NOTE: Because the
ALARM_DURING_CAL resource
affects a kernel process
(dbsupdmgr), changing it to TRUE
will not have any effect until the
kernel is restarted.
• Database Update Man-
ager (dbsupdmgr)
FALSE (alarms
will not be gen-
erated while the
parameter is in
calibration)
ALM_NOTIFY_TYPE =
{OUT, NACK}
Specify whether the alarm notifica-
tion will be based on Outstanding
(“OUT”) or Not Acknowledged
(“NACK”) alarms.
This setting applies system-wide to
all E-DAS applications that provide
alarm notification (e.g., Alarm Tool
Box, System Monitor, E-DAS Menu
as well as the OMP). Some applica-
tions provide a flashing alarm rib-
bon or box with alarm statistics;
others provide audible notification
via bells and/or a popup alarm mes-
sage. See the related chapters for
details on how each application
provides alarm notification, and how
the resource setting will affect the
alarm notification.
• All E-DAS applications
that provide alarm noti-
fication (e.g., Alarm
Tool Box, System
Monitor, E-DAS Menu,
and OMP).
OUT (notifica-
tion will be
provided for
Outstanding
alarms)
RC_EXCEEDENCE = <list
of valid reason codes for ac-
knowledging exceedence
alarms separated by commas>
OR
RC_EXCEEDANCE = <list
of valid reason codes for ac-
knowledging exceedance
alarms separated by commas>
AC_EXCEEDENCE = <list
of valid action codes for ac-
knowledging exceedence
alarms separated by commas>
OR
AC_EXCEEDANCE = <list
of valid action codes for ac-
knowledging exceedance
alarms separated by commas>
RC_INVALID = <list of
valid reason codes for ac-
knowledging invalid alarms
separated by commas>
Configure a list of valid reason and
action codes that can be used during
alarm acknowledgment for an ex-
ceedance, invalid data, out of con-
trol data, suspect data, missing data,
or maintenance data alarm event.
If the user selects one, and only one,
such alarm to acknowledge, this list
of reason codes will be displayed
and only a code from this list can be
entered.
Note: For the “exceedance”(or
“exceedance”) resources to work,
user-defined alarms must be named
so that the letters "EXC" appear
somewhere in the alarm name. Oth-
erwise, the alarm will be treated as
any other alarm; i.e., this ex-
ceedance resource will be ignored
for alarms of that name.
• Alarm Acknowledgers
All reason and
action codes will
be displayed and
can be entered.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-15
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used by
plicable
AC_INVALID = <list of
valid action codes for ac-
knowledging invalid alarms
separated by commas>
RC_OUT_OF_CONTROL =
<list of valid reason codes for
acknowledging out-of-control
alarms separated by commas>
AC_OUT_OF_CONTROL =
<list of valid action codes for
acknowledging out-of-control
alarms>
RC_SUSPECT = <list of
valid reason codes for ac-
knowledging suspect alarms
separated by commas>
AC_SUSPECT = <list of
valid action codes for ac-
knowledging suspect alarms
separated by commas>
RC_MISSING = <list of valid
reason codes for acknowledg-
ing missing alarms separated
by commas>
AC_MISSING = <list of valid
action codes for acknowledg-
ing missing alarms separated
by commas>
RC_MAINTENANCE = <list
of valid reason codes for ac-
knowledging maintenance
alarms separated by commas>
AC_MAINTENANCE = <list
of valid action codes for ac-
knowledging maintenance
alarms separated by commas>
Examples:
RC_EXCEEDENCE =
AC_EXCEEDENCE =
ALARM_2K = <TRUE |
FALSE>
Example:
ALARM_2K = FALSE
Set to True to enable ATC; other-
wise pre-ATC alarm triggering is
used.
• CemStop
• Database Update Man-
ager (dbsupdmgr)
FALSE
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-16
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used by
plicable
ATC_ALM_EMAIL_FORM
AT
Example:
ATC_ALM_EMAIL_FORM
AT <format>
where “format” is defined
according to the section below
entitled “Alarm Message
Format Designators”
Configure the format of Alarm
Status Display as it will appear in
email messages sent by the ATC
system.
• Database Update Man-
ager (dbsupdmgr)
ATC_ALM_EM
AIL_FORMAT
= %r
%M/%D/%Y
%h:%m %S
%P %i %d
%N %T
ALL_COMALM
Example:
ALL_COMALM = TRUE
COM alarms are normally limited to
one COM alarm for one site per
hour. Setting this resource to TRUE
will cause COM alarms to occur
every minute.
• Alarm Manager
(alarmmgr)
FALSE
Alarm Message Format Designators
The format designators for the “ALM_FORMAT…” resources are defined below. When an alarm
is to be printed according to the defined “ALM_FORMAT…” resource variable, the format des-
ignators are replaced with the corresponding field from the alarm record.
Designator
Description
Status
%R
Return-to-normal status, where RTN=returned to normal and OUT=outstanding
alarm
%r
Short return-to-normal status, where R=returned to normal and O=outstanding
alarm
%A
Acknowledgment status, where ACK=acknowledged alarm and NAK=not-
acknowledged alarm
%a
Short acknowledgment status, where A=acknowledged and N=not-acknowledged
alarm
Date
%D
Two-digit day of the alarm
%M
Two-digit month of the alarm
%O
Three-character abbreviation for the month of the alarm
%Y
Two-digit year of the alarm
%w
Two-digit event month, where the event month is the month of the alarm or the
month the alarm returned to normal
%o
Three-character event month, where the event month is the month of the alarm or
the month the alarm returned to normal
%x
Two-digit event day, where the event day is the day of the alarm or the day the
alarm returned to normal
%y
Two-digit event year, where the event year is the year of the alarm or the year the
alarm returned to normal
Time
%h
Two-digit hour of the alarm, in military format
%m
Two-digit minute of the alarm
%u
Event hour, where the event hour is the hour of the alarm or the hour the alarm
returned to normal
%v
Event minute, where the event minute is the minute of the alarm or the minute the
alarm returned to normal
Affected Data
%S
Site name of data associated with alarm
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-17
User’s Guide
Appendix A System Resources
%P
Parameter name of data associated with alarm
%N
Alarm name
%i
Average interval of data associated with alarm
%d
Data value associated with alarm
%f
Data logger flags on data associated with alarm (four flags maximum)
%E
Event description, where ALM=alarm event and RTN=alarm has returned-to-
normal event
%T
Alarm message; should always be the last designator when used
Miscellaneous
%%
Percent sign
It is strongly recommended that %T be the last designator when it is used in a
format string because it is the only designator that is replaced with a character
string of varying length.
For example, the program default format for all alarm messages is:
Default = %R %A %M/%D/%Y %h:%m %S %P %i %d %N %T
which configures alarm messages in the form of:
RTN_status ACK_status month/day/year_of_alarm hour:minute site
parameter interval data_value alarm_name alarm_message
such that an alarm message might read:
OUT NAK 11/11/93 14:15 SITE#1 SO2PPM 1m 14.5900 SUSPALM Data value
is suspect.
The default definitions for each variable are:
ALM_FORMAT_ACKER=%r %M/%D/%Y %h:%m %S %P %i %d %N %T
ALM_FORMAT_ALMSTAT=%a %M/%D/%Y %h:%m %S %P %i %d %N %T
ALM_FORMAT_OCRIBBON=%r %M/%D/%Y %h:%m %S %P %i %d %N %T
Main Menu Resources
Resource syntax/example
Resource description
Used by
Default, if ap-
plicable
MAINMENU =
<filename>
Example (Part 60 only us-
ers):
MAINMENU = main-
menu.part60
This resource dictates which
“mainmenu” file should be used to
display as the main menu for use by
the CUI (character-based) Main
Menu (mnudrv). If this resource
exists (as well as the file that is ref-
erenced), mnudrv will use this file as
the main menu file.
NOTE: <filename> will assume the
file is in the config directory. This
resource may be specified in cem.rc
for all users, or in individual
$LOGNAME.rc files for specific
users.
• Menu Drivers
(xw_mnudrv, mnudrv)
If the resource
(or the file it
references) does
not exist, the
standard main-
menu file will
always be used
(misc/ main-
menu).
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-18
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used by
plicable
VBMAINMENU = <file-
name>
Example (Part 60 only us-
ers):
VBMAINMENU =
vbmainmenu.part60
This resource dictates which file
should be used to display as the
main menu for use by the GUI
(Windows-based) Main Menu. If
this resource exists (as well as the
file that is referenced), the GUI
Main Menu will use this file as the
main menu file.
NOTE: <filename> will assume the
file is in the misc directory.
• Menu Drivers
(xw_mnudrv, mnudrv)
If the resource
(or the file it
references) does
not exist, the
standard
vbmainmenu
file will always
be used (misc/
vbmainmenu).
Math Pack Resources
Resource syntax/example
Resource description
Used by
Default, if ap-
plicable
MATHPACK_
CASCADE = {TRUE |
FALSE}
Example:
MATHPACK_
CASCADE = FALSE
This resource variable controls recur-
sion of math pack calculations. By
default, any calculation or missing
data substitution triggers a “cascade”
procedure to recalculate all affected
parameters. This can consume system
time in some cases, and it may be
necessary to set this resource to
FALSE and manually handle any
dependencies.
• All programs that run
mathpack
TRUE (do cas-
cading)
MP_CROSS_SITE_
CASCADE ={TRUE |
FALSE}
Example:
MP_CROSS_SITE_
CASCADE = FALSE
This resource variable forces recalcu-
lation of dependent parameters to be
of the same site; that is, it forces math
pack recursion to be site-specific.
NOTE: When running the Math Pack
utility from the command line (e.g., in
the Task Scheduler or a custom
menu), you can also turn off math
pack cascade by using the "-O" op-
tion in the mpcalcparm command.
• All programs that run
mathpack
TRUE (means
that automatic
recalculation of
dependent pa-
rameters will
occur across
sites (cascade is
globally ap-
plied)).
MP_NO_CALC_
PARMS =
<parameter:site>
Example:
MP_NO_CALC_
PARMS = SO2PPM:SITE01
This resource variable allows you to
exclude from math pack any parame-
ters that are calculated at the logger
and should never be recalculated at
central. Full specification of <pa-
rameter>:<site> is required, as shown
in the example to the left.
• All programs that run
mathpack
MP_PROP_AS_QA = <list
of parameters separated by
commas>
MP_PROP_AS_QA_
<site> = <list of parameters
separated by commas>
Example:
MP_PROP_AS_QA =
CO2C,SO2PPMC,NOXPPM
C,FLOWSCFH
Configure control for propagation of
missing/non-QA values. For those
who apportion their fuel factors based
upon heat input. If a constituent of
fuel factor is missing, then fuel factor
will be missing. This would then
cause NOx lb to be missing. This
resource will cause the fuel factor (or
any other parameter you include in
the list) to propagate as QA/non-
missing. The parameter will still be
listed in the database as missing,
however.
• All programs that run
mathpack
None
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-19
User’s Guide
Appendix A System Resources
Real-Time Tabular Data Displays Resources
Resource syntax/example
Resource description
Used by
Default, if ap-
plicable
DLFLAGS_PRIORITY =
"<list_of_data_
logger_flags_in_
priority”>
Example:
DLFLAGS_PRIORITY =
"MBDLCHPF<>"
If you want to change the sorting
priority of the data logger flags on
character-based real-time displays,
you can use this resource. (Up to five
logger flags can be displayed in
rmtdsp3 if the FLAGS ON command
is used in the rmtdsp3 configuration
file.)
NOTE: You can change the flag prior-
ity and colors of a custom Real-Time
Display by using the Priority feature
of the screen design editor. See
“Real-Time Data Displays,” in Part 4,
for more information.
• Real-Time Data Dis-
plays (rmtdsp, rmtdsp2,
rmtdsp3)
The default
sorting priority
for showing
flags on values
is as follows:
< P D F T B C
M O U A + - R
H h L l J j t p f
V W X Y Z >
RDT_AGEDMINUTES_
MINDATA
Example:
RDT_AGEDMINUTES_
MINDATA=2
Provided to extend the period minute
data will wait before being consid-
ered aged, by time interval
• Real-Time Data Dis-
plays (rmtdsp, rmtdsp2,
rmtdsp3)
RDT_AGEDMINUTES_
AUXDATA
Example:
RDT_AGEDMINUTES_
AUXDATA=3
Provided to extend the period auxil-
iary data will wait before being con-
sidered aged, by time interval
• Real-Time Data Dis-
plays (rmtdsp, rmtdsp2,
rmtdsp3)
RDT_AGEDMINUTES_
HRDATA
Example:
RDT_AGEDMINUTES_
HRDATA=5
Provided to extend the period hourly
data will wait before being consid-
ered aged, by time interval
• Real-Time Data Dis-
plays (rmtdsp, rmtdsp2,
rmtdsp3)
RDT_AGEDMINUTES_
DAYDATA
Example:
RDT_AGEDMINUTES_
DAYDATA=30
Provided to extend the period daily
data will wait before being consid-
ered aged, by time interval
• Real-Time Data Dis-
plays (rmtdsp, rmtdsp2,
rmtdsp3)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-20
User’s Guide
Appendix A System Resources
Daily Reports Resources
Resource syntax/example
Resource description
Used by
Default, if ap-
plicable
RPT_UNIT_OFF_
DATA_<site> = {TRUE |
FALSE}
OR
RPT_UNIT_OFF_
DATA = {TRUE | FALSE}
Example:
RPT_UNIT_OFF_
DATA = TRUE
This resource variable indicates
whether data will be reported for
units that are not operating during an
hour. If TRUE, all data will be re-
ported regardless of whether the unit
was operating that hour.
Daily reports using this variable are:
Unit Operating Report, SO2 Emis-
sions and Flow Report, NOx and
CO2 Emissions Report, and General
Average Report.
• General Average Report
(gnlavgrpt)
• Excess Emission Dura-
tion Report (exemisrpt)
• Excluded Data Duration
Report (exemisrpt)
FALSE (a blank
line will appear
in the daily re-
ports for a par-
ticular hour if
the unit was not
operating).
Calibration System Resources
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
CAL_MLIMIT_<site>_<par
ameter> = <limit>
where limit can be a specific
value such as 5 or a percent-
age such as 45%
Example:
CAL_MLIMIT_
SITE04_SO2PPMC = 60%
Configure the calibration mainte-
nance limit to a specific value or a
percentage (percentage ends with %).
If configured as a specific value, the
calibration error is reported as
MAINT. LIMIT if the percent error
is greater than the specified value. If
configured as a percentage, the cali-
bration error is reported as MAINT.
LIMIT if the percent error is greater
than the defined percentage of the
error limit. See the “Calibration Sys-
tem” chapter for details.
• General Daily Calibra-
tion Report (gencalrpt)
• Daily Calibration
Glance Report (pa-
calrpt)
SHOW_CAL_MLIMIT =
{TRUE | FALSE}
Example:
SHOW_CAL_MLIMIT =
TRUE
If set to TRUE, MAINT will be re-
ported for the calibration error. If
FALSE or not defined, only PASS or
FAIL will be reported for the calibra-
tion error.
Example:
SHOW_CAL_MLIMIT = TRUE
• General Daily Calibra-
tion Report (gencalrpt)
FALSE
EDF_CAL_LEN_
<site>_<parameter> =
<calibration duration in
minutes>
Example:
EDF_CAL_LEN_
SITE01_CO2C = 20
Configuration of calibration duration
in minutes. This resource is also used
by the Add Calibration Data Tool to
determine calibration end time. The
calibration duration is important
when determining if the hour of a
good calibration should be included
in the out-of-control hour count.
• Add Calibration Data
Tool (caldbsadd)
If not defined,
the Add Calibra-
tion Data utility
sets the calibra-
tion end time to
be the start time.
The hour in
which the good
cal is performed
is always in-
cluded in the
out-of-control
hour total.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-21
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
GAS_EXPIRATION_
DATE_REQUIRED =
<TRUE|FALSE>
Example:
GAS_EXPIRATION_
DATE_REQUIRED =
TRUE
Determines whether the expiration
date should be a required field in the
Linearity Check Editor (linchk), the
Calibration Expected Values Editor
(cfcalexp), and the Calibration Con-
figuration Editor (cfcal8816).
• Linearity Check Editor
(linchk)
• Calibration Expected
Values Editor (cfcalexp)
• Calibration Configura-
tion Editor (cfcal8816)
False
SIGNED_CAL_ERRORS_
<site>_<parameter> =
{TRUE | FALSE}
SIGNED_CAL_ERRORS_
<site> = {TRUE | FALSE}
SIGNED_CAL_ERRORS =
{TRUE | FALSE}
Example:
SIGNED_CAL_ERRORS_
SITE04_SO2PPMC = TRUE
When set to TRUE, the signed value
instead of the absolute value of (R-A)
will be used when calculating the
calibration error. When the resource
is missing, or set to FALSE, the cali-
bration error computations will use
the absolute value of (R-A).
If you have purchased the optional
Alberta Reporting Module, additional
information about this resource and
how it is used is available in the Al-
berta Reporting Module documenta-
tion.
• General Daily Calibra-
tion Report (gencalrpt)
• Daily Calibration
Glance Report (pa-
calrpt)
• Daily Calibration Error
Report (calerrrpt)
False
Daily Matrix Opacity Report Resource
Resource syntax/example
Resource description
Used by
Default, if ap-
plicable
OPACOPHR_<site>_
<opacity_parameter> =
<opacity_time_online_ pa-
rameter>
Example:
OPACOPHR_SITE01_
OPAC = OPACOPHR
If multiple opacity parameters are
configured for a single site, this re-
source lets you associate the <opac-
ity_parameter> with its opacity oper-
ating time parameter.
This resource is also used by the
Summary Report (40CFR60 Report).
• Daily Matrix Opacity
Report (dmopacrpt)
• Summary Report (sum-
maryrpt)
The time online
parameter with
the OPACOPHR
report name will
be used.
General Average Report Resources
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
RPT_DATA_PROBLEM_
TYPE = {TRUE | FALSE}
Example:
RPT_DATA_PROBLEM_
TYPE = TRUE
This resource variable, if defined as
TRUE, will clarify problem data
values in the General Average Report
(and also in the Daily Matrix Opacity
Report). If TRUE, instead of an as-
terisk, these identifying letters will be
used: M=missing data, I=invalid
data, O=out-of-control,
E=exceedance, and S=suspect data.
• General Average Report
(gnlavgrpt)
• Daily Matrix Opacity
Report (dmopacrpt)
Hourly Summary Report
(dhlysumrpt)
FALSE
(An asterisk (*)
will indicate
exceptional data
values.)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-22
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
RPT_MISSING_DATA=
{TRUE | FALSE}
Example:
RPT_MISSING_
DATA = FALSE
This resource variable provides a
way to not report any missing data to
state agencies. If FALSE, blanks will
be reported for missing substituted
data, and this data will NOT be in-
cluded in average calculations.
• General Average Report
(gnlavgrpt)
TRUE
(The data calcu-
lated by the
missing data
routine will be
reported with a
flag “U” in the
General Aver-
age Report, and
the data will be
included in av-
erage calcula-
tions.)
RPT_GEOMETRIC_
AVG = {TRUE | FALSE}
Example:
RPT_GEOMETRIC_
AVG = TRUE
If this resource variable is set to
True, the geometric average will be
reported at the bottom of the report.
• General Average Report
(gnlavgrpt)
FALSE
(No geometric
average will be
reported.)
GNLAVG_VALID_
FLAGS = <valid flags> =
<valid data flags>
GNLAVG_VALID_
FLAGS_<site> =
<valid flags> = MOIS
Example:
GNLAVG_VALID_
FLAGS_SITE01 = OS
The data flags M, O, I, and S nor-
mally indicate invalid data. Config-
ure which of these flags should be
considered to be valid flags in the
General Average Report. The re-
source value needs to be a subset of
MOIS where:
M = Missing
O = Out-of-control
I = Invalid
S = Suspect
• General Average Report
(gnlavgrpt)
Data flags M, O,
I, and S are
considered to be
invalid in the
General Aver-
age Report.
Data Exception Report Resources
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
RPT_RETURN_TO_
NORMAL = {TRUE |
FALSE}
Example:
RPT_RETURN_TO_
NORMAL = TRUE
If set to TRUE, report 11:00 return to
normal time for a 1 hour exception
that started at 10:00.
• Exception Reports
(ctrexprpt)
FALSE
(Report 10:00
ending time for
a 1 hour excep-
tion that started
at 10:00.)
Data Export Resources
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
CSV_DELIMITER = <de-
limiter>
NOTE: This was formerly
variable LOTUS_
DELIMITER
Configure the character to be used to
separate fields in an export data file.
See the “Data Export Tools” chapter
in Part 4 for details.
• CSV Export Tool
csvexport)
• CSV Import Tool
(csvimport)
Comma
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-23
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
CSV_QUOTES = {TRUE |
FALSE}
NOTE: This was formerly
variable LOTUS_
QUOTES
Configure whether text strings in an
export data file are enclosed in dou-
ble quotes. If FALSE, text strings are
unquoted. See the “Data Export
Tools” chapter in Part 4 for details.
• CSV Export Tool
csvexport)
• CSV Import Tool
(csvimport)
TRUE (text
strings appear in
double quotes)
DATAEXPORT_
DELIMITER = <delimiter>
Example:
DATAEXPORT_
DELIMITER = ,
Configure the character to be used to
separate fields in an export data file.
See the “Data Export Tools” chapter
in Part 4 for details.
• Data Export Average
Data Tool
(dataexport)
<space>
DATAEXPORT_ QUOTES
= {TRUE | FALSE}
Example:
DATAEXPORT_ QUOTES
= FALSE
This resource has a TRUE or FALSE
value. If TRUE, text strings appear in
double quotes. If FALSE, text strings
are unquoted. See the “Data Export
Tools” chapter in Part 4 for details.
• Data Export Average
Data Tool
(dataexport)
TRUE
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
ALLOW_EXEMPTION
Examples:
ALLOW_EXEMPTION =
Example:
ALLOW_EXEMPTION =
This resource defines the list of rea-
son codes for 6-minute opacity ex-
emptions. If defined, only the listed
reason codes are eligible for the
above-the-normal-limit-but-below-
the-exceptional-limit exemption.
• Excess Emission Report
(exemisrpt1)
• Summary Report (sum-
maryrpt)
None
CFR60_OPMINS_
PER_OPHR =
<number of minutes>
OR
CFR60_OPMINS_
PER_OPHR_<site> =
<number of minutes>
OR
CFR60_OPMINS_
PER_OPHR_<site>_<param
eter> = <number of min-
utes>
Examples:
CFR60_OPMINS_
PER_OPHR = 1
CFR60_OPMINS_
PER_OPHR_SITE1 = 30
Configure number of operating min-
utes required for a valid operating
hour.
• Hourly Rolling Average
Tool (hrrolavg)
• Daily Rolling Average
Tool (dayrolavg)
• Monitor Availability
Reports (monavailrpt &
monavlrpt)
• 30-Day Information
Report (thirtydayrpt)
• 30-Day Rolling Aver-
age Exceedance Report
(thirtydayavgrpt)
• Daily Data Duration
Reports (dayexcrpt)
• Daily Rolling Average
Report (drolavgrpt)
• Block Summary Report
(blksummaryrpt)
• Insufficient Data Report
(hstinsuf)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-24
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
VALID_DAY_
HOURS = <number of
hours>
OR
VALID_DAY_
HOURS_<site> = <number
of hours>
OR
VALID_DAY_
HOURS_<site>_<parameter
> = <number of hours>
Examples:
VALID_DAY_
HOURS = 18
VALID_DAY_
HOURS_SITE1 = 1
Configure number of operating hours
needed to constitute an operating
day.
NOTE: The resources CFR60_ OP-
MINS_PER_OPHR and VALID_
DAY_HOURS are used to define a
valid boiler operating day. Once it is
verified that a day is a valid boiler
operating day, the reports (daily roll-
ing average) will check if a daily
average is valid. The valid daily av-
erage is defined as a minimum of
boiler is operating.
• Daily Rolling Average
Tool (dayrolavg)
• 30-Day Information
Report (thirtydayrpt)
• 30-Day Rolling Aver-
age Exceedance Report
(thirtydayavgrpt)
• Daily Data Duration
Reports (dayexcrpt)
• Block Summary Report
(blksummaryrpt)
• Daily Rolling Average
Report (drolavgrpt)
• Monitor Availability
Report (monavailrpt)
• Santee Cooper Event
Utilities and Report
(scemisutil)
HR_EXCLUDE_
CENTRAL_<site>_
<parm>
OR
HR_EXCLUDE_
CENTRAL_<site>
OR
HR_EXCLUDE_CENTRAL
Example:
HR_EXCLUDE_CENTRAL
= TH
List of Central flags to be excluded
from the multi-hour average, one or
more of the following:
E = EXCEEDANCE
S = SUSPECT
N = MAINTENANCE
T = STARTUP
H = SHUTDOWN
U = OURANGE
• Hourly Rolling Average
Tool (hrrolavg)
None
HR_AVG_VALID_
OPHRS_<site>_
<parameter>
or
HR_AVG_VALID_
OPHRS_<site>
or
HR_AVG_VALID_
OPHRS
List of average intervals whose
values should be based on the last
n valid operating hours instead of
the last n calendar hours.
• Hourly Rolling Average
Tool (hrrolavg)
None
HR_AVG_LAST_INT_
OPHRS_<site>_<parm>
or
HR_AVG_LAST_INT_
OPHRS_<site>
or
HR_AVG_LAST_INT_
OPHRS
List of average intervals whose val-
ues should be based on the last n
operating hours instead of the last n
calendar hours.
• Hourly Rolling Average
Tool (hrrolavg)
None
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-25
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
MULTI_HOUR_
ALARM_FRONT_
TAG_<site>_
<parameter>
or
MULTI_HOUR_
ALARM_FRONT_
TAG_<site>
or
MULTI_HOUR_
ALARM_FRONT_TAG
If one of these resources is set to
TRUE for a site/parameter, an ex-
ceedance or invalid data alarm for
multi-hour values will be front time-
tagged. For example, a 3-hour aver-
age exceedance stored in the database
for 02:00 will have an alarm time-
tagged at 00:00.
• Hourly Rolling Average
Tool (hrrolavg)
False
MULTI_HOUR_ALARM
_FRONT_TAG_<site>_
<parameter>
or
MULTI_HOUR_ALARM
_FRONT_TAG_<site>
or
MULTI_HOUR_ALARM
_FRONT_TAG
If one of these resources is set to
TRUE for a site/parameter, an ex-
ceedance or invalid data alarm for
multi-hour values will be front time-
tagged. For example, a 3-hour aver-
age exceedance stored in the database
for 02:00 will have an alarm time-
tagged at 00:00.
• Hourly Rolling Average
Tool (hrrolavg)
False
OP_TIME_PREC =
<fractional value>
OR
OP_TIME_PREC_<site>
Example:
OP_TIME_PREC = 10
The portion of the hour that the stack
was operating is expressed in incre-
ments defined by the OP_TIME_
PREC resource (used in conjunction
with the OP_TIME_EFFE resource.
For example, if quarter-hour decimal
increments are used, 0.00 means the
stack was not operating, 0.25 means
the stack was operating for 1 to 15
minutes, 0.50 represents 16 to 30
minutes, 0.75 represents 31 to 45
minutes, and 1.00 means the stack
was operating the full hour (46 to 60
minutes). The value is determined by
the number of minutes recorded and
accepted for the QA parameter with
the report name UNITOPHR.
See chapter “Daily Record Informa-
tion” in Part 4 for details.
• Daily Rolling Average
Tool (dayrolavg)
source does not
exist, quarter-
hour decimal
increments are
used.)
OP_TIME_EFFE = <qyy>
OR
OP_TIME_EFFE_<site>
Example:
OPAC_TIME_EFFE = 200
Configure the quarter when the
OP_TIME_PREC operating time
precision became effective. For any
period before this quarter, the normal
quarter-hour logic would be used.
• Daily Rolling Average
Tool (dayrolavg)
Use OP_
TIME_PREC
for any time
period that the
program is run.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-26
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
RC_OPAC_EE = <comma
separated reason code list>
RC_OPAC_
DOWNTIME = <comma
separated reason code list>
RC_FLOW_EE = <comma
separated reason code list>
RC_FLOW_
DOWNTIME = <comma
separated reason code list>
RC_GAS_EE = <comma
separated reason code list>
RC_GAS_
DOWNTIME = <comma
separated reason code list>
Examples:
RC_OPAC_EE =
RC_OPAC_
DOWNTIME = 13,14
RC_GAS_EE = 01,02,03
RC_GAS_
DOWNTIME = 10,12
Summary Report “Option 1” re-
sources. Configure which reason
codes that are associated with mes-
sages will be reported.
• Summary Report (sum-
maryrpt)
• Block Summary Report
(blksummaryrpt)
If an excess
emission re-
source is not
configured, all
reason codes
from 01-50 con-
figured with
messages will be
reported.
If a downtime
resource is not
configured, all
reason codes
from 51-59 con-
figured with
messages will be
reported.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-27
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
SUM_ EE_LABEL_A =
<first excess emission cate-
gory label>
SUM_ EE_LABEL_B =
<second excess emission
category label
SUM_ EE_RCODES_ A =
<excess emission category A
comma separated reason
code list>
SUM_ EE_RCODES_ B =
<excess emission category B
comma separated reason
code list>
SUM_ DT_LABEL_A =
<first downtime category
label>
SUM_ DT _LABEL_ B =
<second downtime category
label
SUM_DT_RCODES_ A = <
downtime category A
comma separated reason
code list>
SUM_DT_RCODES_B =
<downtime category B
comma separated reason
code list>
Examples:
SUM_EE_LABEL_A =
Startup/Shutdown
SUM_EE_LABEL_B =
Process Problems
SUM_EE_RCODES_A =
SUM_EE_RCODES_B =
Summary Report “Option 2” re-
sources. Configure excess emission
and downtime category labels and
reason codes.
• Summary Report (sum-
maryrpt)
• Block Summary Report
(blksummaryrpt)
SUM_SUBTOTAL_EE_
CATEGORIES_?
Where ? is a number 1-20
Examples:
SUM_SUBTOTAL_EE_
CATEGORIES_1 = ABC
SUM_SUBTOTAL_EE_
CATEGORIES_2 = DE
List of excess emission categories
to include in one subtotal.
• Summary Report (sum-
maryrpt)
None
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-28
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
SUM_SUBTOTAL_EE_
LABEL_?
Where ? is a number 1-20
Examples:
SUM_SUBTOTAL_EE_
LABEL_1 = Subtotal
Exempt
SUM_SUBTOTAL_EE_
LABEL_2 = Subtotal
Non-Exempt
Excess emission subtotal group
label
• Summary Report (sum-
maryrpt)
None
SUM_SUBTOTAL_DT_
CATEGORIES_?
Where ? is a number 1-20
Examples:
SUM_SUBTOTAL_DT_
CATEGORIES_1 = ABC
SUM_SUBTOTAL_DT_
CATEGORIES_2 = DE
List of downtime categories to
include in one subtotal
• Summary Report (sum-
maryrpt)
None
SUM_SUBTOTAL_DT_
LABEL_?
Where ? is a number 1-20
Examples:
SUM_SUBTOTAL_DT_
LABEL_1 = Subtotal
Exempt
SUM_SUBTOTAL_DT_
LABEL_2 = Subtotal
Non-Exempt
Downtime subtotal group label
• Summary Report (sum-
maryrpt)
None
PCT_BY_VALID_
HOURS = {TRUE | FALSE}
Example:
PCT_BY_VALID_
HOURS = TRUE
Configure to TRUE if excess emis-
sion percentages must be based on
valid monitor hours instead of total
operating hours.
• Summary Report (sum-
maryrpt)
• Block Summary Report
(blksummaryrpt)
FALSE
RPT_MONITOR_
TIME = {TRUE | FALSE}
Example:
RPT_MONITOR_
TIME = TRUE
If set to TRUE, the following infor-
mation be shown in the report header
beneath the Emission Limit:
“Total Source Monitored Time in
Report Period n Hrs”
n is the number of hours during the
report period that were not downtime
hours.
• Summary Report (sum-
maryrpt)
• Block Summary Report
(blksummaryrpt)
FALSE
MAX_EXEMPT = <number
of exemptions allowed>
Example:
MAX_EXEMPT = 4
Controls the number of 6-minute
exemptions that can be claimed per
day (24-hours).
• Excess Emission Report
(exemisrpt1)
• Summary Report (sum-
maryrpt)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-29
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
EXEMISRPT_HD_
NOTE
This resource is checked only when
the –R option is included. This re-
source can be configured with a note
to be included in the report heading.
• Excess Emission Report
(exemisrpt1)
• Excess Emission Dura-
tion Report (exemisrpt)
• Downtime Duration
Report (exemisrpt)
“Note: All
times based on
start of inter-
val.” (Default
applies only
when –R op-
tion is in-
cluded.)
EXEMPT_
DOWNTIME = <reason
code list>
Example:
EXEMPT_DOWNTIME =
Reason codes that should be ex-
cluded from the downtime even if
they are marked as missing. If this
resource exists, occurrences of these
reason codes will be totaled together
and shown at the bottom of the report
as “Exempt Monitor Downtime.”
• Summary Report (sum-
maryrpt)
• Block Summary Report
(blksummaryrpt)
None
SUM_SUBTOTALS
Example:
SUM_SUBTOTALS = BCE
Values for categories “B”,
“C”, and “E” will be
summed to determine the
total exceedances reported.
Defines the categories to include in
the reported exceedance total.
This resource is valid ONLY when
the SUM_EE_LABEL_?
SUM_EE_RCODES_? resources are
used.
• Summary Report (sum-
maryrpt)
None
ALLOW_
EXEMPTION
Example:
ALLOW_
EXEMPTION=01,02,08
If defined, only the listed reason
codes are eligible for the above-the-
normal-limit-but-below-the-
exceptional-limit exemption.
• Excess Emission Report
(exemisrpt1)
• Summary Report (sum-
maryrpt)
None
RC_EXCEED = <comma
separated reason code list>
Example:
RC_EXCEED =
List of exceedance reason codes.
• Excess Emission Dura-
tion Report (exemisrpt)
• Daily Excess Emission
Duration Report (day-
excrpt)
None
RC_DOWNTIME =
<comma separated reason
code list>
Example:
RC_DOWNTIME =
List of downtime data reason codes.
• Downtime Duration
Report (exemisrpt)
• Daily Downtime Dura-
tion Report (dayexcrpt)
None
RC_EXCLUDED = <comma
separated reason code list>
Example:
RC_EXCLUDED = 06,07,08
List of excluded data reason codes.
• Excluded Data Duration
Report (exemisrpt)
• Daily Excluded Data
Duration Report (day-
excrpt)
None
RPT_ENDING_TIME =
{TRUE | FALSE}
Example:
RPT_ENDING_TIME=
TRUE
If set to TRUE, the END time of the
downtime duration will be reported
(i.e., the start time of the next period
that is not downtime). When this
resource is set, any downtime period
will be closed out at the end of the
report time.
• Excess Emission Dura-
tion Report (exemisrpt)
• Downtime Data Dura-
tion Report (exemisrpt)
• Excluded Data Duration
Report (exemisrpt)
FALSE
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-30
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
MN_STDLMT_
<site>_<parameter>
Example:
MN_STDLMT_
UNIT01_OPAC= 20
Standard limit to use if not found in
the 40CFR60 configuration file.
• Excess Emission Dura-
tion Report (exemisrpt)
None
MN_EXCLMT_<site>_
<parameter>
Example:
MN_EXCLMT_
UNIT01_OPAC=27
Exceptional limit to use if not found
in the 40CFR60 configuration file.
• Excess Emission Dura-
tion Report (exemisrpt)
None
CALEN-
DAR_DAY_AVGS_
<site>_<parameter>
CALEN-
DAR_DAY_AVGS_ <site>
CALENDAR_DAY_AVGS
Example:
CALENDAR_DAY_AVGS
= 30,365
List of daily average intervals that
should be based on consecutive cal-
endar days, not operating days only.
• Daily Rolling Average
Tool (dayrolavg)
None
DAY_EXCLUDE_
CENTRAL_<site>_
<parameter>
DAY_EXCLUDE_
CENTRAL_<site>
DAY_EXCLUDE_
CENTRAL
Example:
DAY_EXCLUDE_
CENTRAL = TH
A list of data flags that will exempt
an hourly value from being included
in the calculation of a 1-day value for
the site and parameter in the resource
name. The excluded 1-hour value
will be considered invalid. 1-day data
with these flags will be excluded
from multi-day calculations. Possible
flags are E, S, N, T, H, and U.
where:
E = EXCEEDANCE
S = SUSPECT
N = MAINTENANCE
T = STARTUP
H = SHUTDOWN
U = OURANGE
• Daily Rolling Average
Tool (dayrolavg)
None
CHKOOC_USE_
ABORTED_CALS = {TRUE
| FALSE}
Example:
CHKOOC_USE_
ABORTED_CALS = TRUE
If set to TRUE, aborted calibrations
will be used when determining OOC
status.
• Check Out-of-Control
Tool (chkooc60)
FALSE
RPT_EXCE_PARMS
Example:
RPT_EXCE_PARMS =
PARM1,PARM2,
PARM3
A list of up to 3 parameters whose
values should be reported when a
parameter’s exceedance is reported
for the site.
• Excess Emission Report
(exemisrpt1)
None
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-31
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
P60_AUDIT_DATE_
SOURCE_<site>_<parm
>
Or
P60_AUDIT_DATE_
SOURCE_<site>
Or
P60_AUDIT_DATE_
SOURCE
If defined, user may specify the
date to use for the “Date of Latest
CMS Certification or Audit” (the
Cer./CEA (date) field of the re-
port header). Resource should be
set to one of the following:
RATA - Obtain date
of most re-
cent RATA
LINEARITY - Obtain date
of most re-
cent linearity
CERT - Use the cer-
tification
date
MOST_RECENT - Use the
most recent
of RATA,
linearity, or
certification
dates
MMDDYYYY - Where
“MM” is the
month,
“DD” is the
day of the
month, and
“YYYY” is
the year of
certification
• Summary Reports
CERT
MEMO_DATA_
REQUIRED
If memo comments are specified in
the memo database, the Excess Emis-
sion Duration report will pick it up
when run with the –M option. To use
this feature, the
MEMO_DATA_REQUIRED =
True resource must be specified in
the cem.rc file.
• Downtime Duration
Report (exemisrpt)
• Excess Emission Dura-
tion Report (exemisrpt)
FALSE
DAYEXCRPT_HD_
NOTE
This resource is checked only
when the –R option is included.
This resource can be configured
with a note to be included in the
report heading.
• Daily Data Duration
Reports (dayexcrpt)
“Note: All
times based on
start of inter-
val.” (Default
applies only
when –R op-
tion is in-
cluded.)
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-32
User’s Guide
Appendix A System Resources
Minute to Hour Calculation Tool Resources
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
M2HR_VAL_
PERCENT
Example:
M2HR_VAL_
PERCENT = 80
Defines the percentage of valid 1-
minute values required for a 1-hour
value to be valid.
• Minute-to-Hour Calcu-
lation Tool (m2hr)
M2HR_EXCLUDE_
CENTRAL_<site>_
<parameter>
OR
M2HR_EXCLUDE_
CENTRAL_<site>
OR
M2HR_EXCLUDE_
CENTRAL
Example:
M2HR_EXCLUDE_
CENTRAL_UNIT03_
NOXPPM = MOIN
List of Central flags, one or more of
the following:
M = MISSING
O = OUT-OF-CONTROL
I = INVALID
E = EXCEEDANCE
S = SUSPECT
N = MAINTENANCE
T = STARTUP
H = SHUTDOWN
U = OURANGE
• Minute-to-Hour Calcu-
lation Tool (m2hr)
MISSING,
INVALID,
and
OUT-OF-
CONTROL
M2HR_EXCLUDE_
<site>_<parameter>
OR
M2HR_EXCLUDE_
<site>
OR
M2HR_EXCLUDE
Example:
M2HR_EXCLUDE_UNIT0
List of Data Logger flags to exclude
from processing.
• Minute-to-Hour Calcu-
lation Tool (m2hr)
None
M2HR_ASSIGN_LAST_
SS_OP_RC_<site>_
<parameter>
OR
M2HR_ASSIGN_LAST_
SS_OP_RC_<site>
OR
M2HR_ASSIGN_LAST_
SS_OP_RC
Example:
M2HR_ASSIGN_LAST_
SS_OP_RC_UNIT03 = F
Used to override the normal assign-
ment of startup or shutdown reason
code during hours in which both
startup and shutdown minutes have
occurred and one of the reason codes
would have normally been assigned
based on normal processing (i.e.,
using the RCAC_PRIORITY re-
source). The operational status of the
last minute of the hour will determine
the reason code to be assigned to the
hour. If the last minute was operat-
ing, the RC_STARTUP reason code
and action codes will be used. If the
last minute was not operating, the
RC_SHUTDOWN reason and action
codes will be used.
• Minute-to-Hour Cal-
culation Tool (m2hr)
FALSE
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-33
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
M2HR_PROPAGATE_SS
When resource value is set to TRUE,
and the M2HR_EXCLUDE_ CEN-
TRAL_<site>_<parameter> resource
does not include T or H, propagate
the startup or shutdown flags, if pre-
sent on any minute (valid or not), to
the hourly data record.
• Minute-to-Hour Cal-
culation Tool (m2hr)
FALSE
RCAC_PRIORITY
Example:
RCAC_PRIORITY = MTH
Used to determine the sorting priority
of the central flags to determine
which reason code and action code to
place on the hourly data.
• Minute-to-Hour Calcu-
lation Tool (m2hr)
Missing, Inva-
lid, Suspect,
Startup, Shut-
down, Mainte-
nance
IGNORE_BOILER_ OFF-
LINE = {TRUE | FALSE}
Example:
IGNORE_BOILER_ OFF-
LINE = TRUE
Used to determine if boiler offline
flagged minutes are to be used in the
hourly data calculation. When
TRUE, boiler offline minutes are
included in valid hour calculations.
• Minute-to-Hour Calcu-
lation Tool (m2hr)
FALSE
STARTUP_VALID =
{TRUE | FALSE}
Example:
STARTUP_VALID = TRUE
When set to TRUE, hour(s) marked
as startup will be considered as valid;
however, the data value will NOT be
used in the multi-hour average.
Also used by the Hourly Rolling
Average Tool and the Daily Rolling
Average Tool.
• Minute-to-Hour Calcu-
lation Tool (m2hr)
FALSE
SHUTDOWN_ VALID =
{TRUE | FALSE}
Example:
SHUTDOWN_ VALID =
TRUE
When set to TRUE, hour(s) marked
as shutdown will be considered as
valid; however, the data value will
NOT be used in the multi-hour aver-
age.
Also used by the Hourly Rolling
Average Tool and the Daily Rolling
Average Tool.
• Minute-to-Hour Calcu-
lation Tool (m2hr)
FALSE
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-34
User’s Guide
Appendix A System Resources
Startup/Shutdown Tool Resources
Resource syntax/example
Resource description
Used By
Default, if ap-
plicable
STARTUP_MINS = <num-
ber of minutes>
Example:
STARTUP_MINS = 15
Number of continuous minutes to be
flagged as startup.
• Startup/Shutdown Tool
(startupshutdown)
SHUTDOWN_MINS =
<number of minutes>
Example:
SHUTDOWN_MINS = 20
Number of minutes to be flagged as
shutdown.
• Startup/Shutdown Tool
(startupshutdown)
STARTUP_FUEL_TOL_
<site> = <TOL parameter>
OR
STARTUP_FUEL_TOL =
<TOL parameter>
Example:
STARTUP_FUEL_
TOL = STKOPHR
Parameter to use as TOL parameter
for startup. Startup data flagging will
begin with initial data change from 0
to 1.
• Startup/Shutdown Tool
(startupshutdown)
None
STARTUP_SYNC_TOL_
<site> = <TOL parameter>
OR
STARTUP_SYNC_TOL =
<TOL parameter>
Example:
STARTUP_SYNC_TOL =
UNITON
Parameter to use as TOL synchroni-
zation parameter for startup. Count of
STARTUP_MINS begins with initial
data change from 0 to 1. NOTE: If this
resource is not set, counting begins
with data change of STARTUP_
FUEL_TOL resource.
• Startup/Shutdown Tool
(startupshutdown)
None
SHUTDOWN_FUEL_
TOL_<site> = <TOL pa-
rameter>
OR
SHUTDOWN_FUEL_TOL
= <TOL parameter>
Example:
SHUTDOWN_FUEL_TOL
= STKOPHR
Parameter to use as TOL parameter
for shutdown. Shutdown data flag-
ging will END with data change from
• Startup/Shutdown Tool
(startupshutdown)
None
SHUT-
DOWN_SYNC_TOL_
<site> = <TOL parameter>
OR
SHUTDOWN_SYNC_TOL
= <TOL parameter>
Example:
SHUTDOWN_SYNC_TOL
=
UNITON
Parameter to use as TOL synchroni-
zation parameter for shutdown.
Count of SHUTDOWN_ MINS ends
with data change from 1 to 0. (Data is
flagged from this point BACK-
WARD SHUTDOWN_MINS min-
utes.) NOTE: If this resource is not
set, counting ends with data change
of SHUTDOWN_FUEL_TOL re-
source.
• Startup/Shutdown Tool
(startupshutdown)
None
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-35
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if ap-
Used By
plicable
STARTUP_FLAGS_
<site>_<parm> = <flags>
OR
STARTUP_FLAGS_
<site> = <flags>
OR
STARTUP_FLAGS =
<flags>
Example:
STARTUP_FLAGS_
SITE2_CO2 = MN
Additional flags to set when flagging
data as startup (valid flags are any
subset of MOISEN)
where:
M = MISSING
O = OUT-OF-CONTROL
I = INVALIDS = SUSPECT
E = EXCEEDANCE
N = MAINTENANCE
• Startup/Shutdown Tool
(startupshutdown)
None
SHUTDOWN_FLAGS_
<site>_
<parm> = <flags>
OR
SHUTDOWN_FLAGS_
<site> = <flags>
OR
SHUTDOWN_FLAGS =
<flags>
Example:
SHUTDOWN_FLAGS_
SITE01_SO2PPM = SN
Additional flags to set when flagging
data as shutdown (valid flags are any
subset of MOISEN)
where:
M = MISSING
O = OUT-OF-CONTROL
I = INVALID
S = SUSPECT
E = EXCEEDANCE
N = MAINTENANCE
• Startup/Shutdown Tool
(startupshutdown)
None
Database Lock/Unlock Tools
Resource syn-
tax/example
Resource description
Used By
Default, if
applicable
HRLOCK_PARMS_
<site> = <comma delim-
ited list of parameters>
OR
HRLOCK_PARMS_
DEFAULT = <comma
delimited list of parame-
ters>
Example:
HRLOCK_PARMS_
SITE01 = CO2C,
SO2PPMC, NOXPPMC
If one of these resources is de-
fined, only the parameters listed
by the resource will be processed
when locking or unlocking data if
ALL parameters are selected.
• Database Lock/ Un-
lock Tool (dbslock)
None
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-36
User’s Guide
Appendix A System Resources
Client Resources
A “Client resource” is specified in resource files that are local to the E-DAS Client computer.
Client resources contain information specific to an individual Client machine. These resources are
different from the Server-wide resources defined in the cem.rc file. At this time, the following
files can be used to specify Client resources:
¾ edas.ini, which is installed on each Client machine in your Windows (or winnt) directory
¾ edassystemportrange.reg, which is not installed by default on the Client
¾ edasuserportrange.reg, which is not installed by default on the Client
See the sections below for more information on these files.
edas.ini Settings
The edas.ini file uses a Windows INI file format; i.e., each group of related resources is listed un-
der a header enclosed in brackets. For example, the settings for printing, used by the vbspl pro-
gram, would be listed as follows:
[SPL]
LANDSCAPESTANDARDFONT=10
LANDSCAPECOMPRESSEDFONT=8
Some resources can be configured as printer-specific or user-specific or global to the entire Client
machine, and the more specific resource, if configured, will take precedence. The “Resource De-
scription” column in the “Printing Resources” section provided below indicates which resources
perform this way.
The default (template) edas.ini file will be installed in the misc directory, and will be updated
with each software release to include the latest settings.
The information provided in the following section describes the default user ini settings used by
ESC’s software, along with a description of the resource and default. NOTE: The edas.ini file
MUST be located in the Windows directory.
Printing Resources
The printing resources in the edas.ini file are used to configure settings for the printing program,
vbspl, when executed on a particular Client machine. These settings should be specified under the
general heading, “[SPL],”for all printers, or a printer-specific heading, “[SPL <printer name>].”
Resource syntax/example
Resource description
Used by
Default, if
applicable
FONTNAME=<font name>
Informs all (printed) reports which
font to use.
Courier New
STANDARDFONT=<numeric font
size>
Informs all reports which font size
to use for printing of portrait reports
only.
COMPRESSEDFONT=<numeric font
size>
Informs all reports which font size
to use for printing of portrait com-
pressed reports only.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-37
User’s Guide
Appendix A System Resources
Resource syntax/example
Resource description
Default, if
Used by
applicable
LANDSCAPESTANDARDFONT=
<numeric font size>
Informs all reports which font size
to use for printing of landscape
standard font reports only.
LANDSCAPECOMPRESSEDFONT=
<numeric font size>
Informs all reports which font size
to use for printing of landscape
compressed font reports only.
LEFTSPACES=<number of spaces>
Informs all reports the number of
blank spaces to allow in the left
margin for portrait reports.
TOPSPACES=<number of spaces>
Informs all reports the number of
blank spaces (lines) to allow in the
top margin for portrait reports.
LANDSCAPELEFTSPACES=<number
of spaces>
Informs all reports the number of
blank spaces to allow in the left
margin for landscape reports.
LANDSCAPETOPSPACES=<number
of spaces>
Informs all reports the number of
blank spaces (lines) to allow in the
top margin for landscape reports.
Advanced Custom Report Tool Resources
The table below describes Client resources for the Advanced Custom Report Tool that can be
configured in the edas.ini file. These settings should be specified under the general heading,
“[ADVANCED CUSTOM REPORT TOOL],” for all Client users on the machine, or under a
user-specific heading, “[ADVANCED CUSTOM REPORT TOOL <user>],” for that user only.
Resource syntax/example
Resource description
Used by
Default, if
applicable
EDITOR=<editor program name>
Example:
EDITOR=C:\Program Files\Windows
NT\Accessories\wordpad
Specify which text editor to use
when editing an advanced custom
report driver file. Make sure that
editor is accessible vis $PATH envi-
ronment variable or specify full
path.
Advanced
Custom
Report Tool
(Client ver-
sion)
Winvi32.exe,
which is a
feature-rich
text editor that
is installed
with the Client
software
edassystemportrange.reg and edasuserportrange.reg Port Range Settings
The edassystemportrange.reg file or the edasuserportrange.reg file may be used to set the port
range settings to be used by the E-DAS software for all users on a machine or for one specific
user on a machine. The default (template) versions of these files are installed in the script direc-
tory on the Server, and will be updated with each software release to include the latest settings.
¾ The edassystemportrange.reg file contains settings that may be applied to Windows system
environment variables. This text file uses a format that can be imported to the Windows reg-
istry as a system environment variable.
¾ The edasuserportrange.reg file contains settings that may be applied to Windows user envi-
ronment variables. This text file uses a format that can be imported to the Windows registry
as a user-specific environment variable.
In most cases, the port range settings need to be applied to all users on a particular Client ma-
chine, which would involve using the edassystemportrange.reg file.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-38
User’s Guide
Appendix A System Resources
Settings in these files should first be edited in a text editor and then applied to the Windows sys-
tem environment variables by double clicking on the file. CAUTION! Do not double-click on this
file in an attempt to edit it; this action will install the file to the Windows registry.
The information provided in the following table describes the default settings used by ESC’s
software, along with a description of the setting and default.
Resource syntax/example
Resource description
Used by
Default, if
applicable
“EDAS_RPC_LOW_PORT”= “<port
number>”
Example:
“EDAS_RPC_LOW_PORT”=“10000”
Set up the minimum allowable port
to be used for E-DAS Client/Server
communications
E-DAS
Client/
Server RPC
communica-
tions soft-
ware
E-DAS API
E-DAS to PI
Interface
E-DAS OPC
Link
“EDAS_RPC_LOW_PORT”= “<port
number>”
Example:
“EDAS_RPC_HIGH_PORT”=“10500”
Set up the maximum allowable port
to be used for E-DAS Client/Server
communications
E-DAS
Client/
Server RPC
communica-
tions soft-
ware
E-DAS API
E-DAS to PI
Interface
E-DAS OPC
Link
Hints for the User:
¾ Note that unlike the resources in cem.rc and edas.ini files, the resources in these “.reg” files
require the use of quotes (“”) around both the resource name and the value.
¾ Once the resource settings in a .reg file are applied by double-clicking on the file, they will
appear in the Windows system- or user-specific-environment variables, as appropriate, and
can be edited from there in the future.
See the section, “Securing Ports for Client/Server Communication” in Part 7⎯System Manage-
ment for more information.
E-DAS EMR for Windows, Part 60
Appendix A—System Resources • A-39

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_ControlCharts_Lowman_CS4_CO2_Control_Chartxls_4cd21ddb.xls](../tools/engineering_white_papers_WhitePapers_ControlCharts_Lowman_CS4_CO2_Control_Chartxls_4cd21ddb.xls)** (0.15 MB)
- **[engineering_white_papers_WhitePapers_DualRangeAnalogOutputs_DualRangeAnalogOuputExamplexlsm_d35a5a7b.xlsm](../tools/engineering_white_papers_WhitePapers_DualRangeAnalogOutputs_DualRangeAnalogOuputExamplexlsm_d35a5a7b.xlsm)** (0.65 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Calibration]] - • Database Update Man-
ager (dbsupdmgr)
• Process ...
- [[Calibration]] - • Database Update Man-
ager (dbsupdmgr)
• Process ...
- [[Calibration]] - • E-DAS API
• E-DAS to PI
Interface
E-DAS EMR for ...
- [[Calibration]] - Calibration System Resources
Resource syntax/examp...
- [[Calibration]] - If configured as a specific value, the
calibration...
- [[Calibration]] - • General Daily Calibra-
tion Report (gencalrpt)
•...
- [[Calibration]] - Example:
SHOW_CAL_MLIMIT = TRUE
• General Daily Ca...
- [[Calibration]] - This resource is also used
by the Add Calibration ...
- [[Calibration]] - The
calibration duration is important
when determi...
- [[Calibration]] - • Add Calibration Data
Tool (caldbsadd)
If not def...
- [[Calibration]] - E-DAS EMR for Windows, Part 60
Appendix A—System R...
- [[Calibration]] - • Linearity Check Editor
(linchk)
• Calibration Ex...
- [[Calibration]] - • General Daily Calibra-
tion Report (gencalrpt)
•...
