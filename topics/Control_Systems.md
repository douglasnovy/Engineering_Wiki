---
title: Control_Systems
consolidated: true
sources: 1
conflicts: 0
confidence: 1.00
generated: ['data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_Controllertools2021pdf_6f884cca.md']  # This would be a timestamp
---

---
author: Mark Astudillo
created: '2025-08-11T10:26:58.152947'
modified: '2023-02-24T15:41:58'
source_hash: 52b6c976093c4a763403c5f1c45e59a797e7c67b4c997996c7df592ddc2613d5
source_path: C:\Users\dnovy\OneDrive - ESC\Training Materials\A_Job Aids\Controller
  tools 2021.pdf
title: ''doc_type: tool_utility
---

StackVision Quick Reference
Controller Tools
Copyright 2021©, All rights reserved.
Controller Tools
The Controller Tools feature allows you to review data controller polling status and perform download, control, and data
retrieval tasks.
Data controllers are usually stationed at remote areas, often quite a distance from the StackVision polling computer. The
StackVision Controller Tools feature provides a convenient method of communicating with and configuring data controllers
using the standard client application.
Controller Tools feature can be launched from:
Tools-Controller Tools
Right clicking on the selected data
controller
link in the properties panel of the selected
data controller
Double clicking the Communications Status
icon
Controller Tools also provides
the following polling and data
controller operations from the
StackVision client computer:

Configuration Backup
(XML)

Clock synchronization

Controller console
emulation

Calibration control

Manual retrieval of
average and calibration
data

Controller tables
StackVision Quick Reference
Controller Tools
Copyright 2021©, All rights reserved.
Controller Tools - Downloading Configuration Changes
The Download tab in the Controller Tools feature provides a way of sending parameter configuration information to a data
controller, without having to physically go to the site and manually type in the information in the data controller.
You can select all tables or multiple tables to download to multiple controllers at once. The following configuration types can
be downloaded:
•
Digital Inputs
•
Digital Outputs
•
Math Constants
•
Parameters
•
Calibration Sequences
•
Average Alarms
•
Digital Events
•
Analog Outputs
•
Calibration Alarms
•
Digitally Triggered Events
•
Parameter Average Validation
•
GSI Command Strings
•
Modbus Configuration (This feature requires 8864 data controller firmware version 5.01 or later.)
To start a download, simply check the boxes for the items you would like to download, and click the Download button, as
shown in the example screen below. If you want to download only certain Math Constants, Parameters, and/or Calibration
Sequences, you can click the plus sign to expand those items and select individual items beneath them.