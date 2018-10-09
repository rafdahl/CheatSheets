## Title: F5 Register Trial Key by CLI
## Purpose:
Install the registration key using the cli vs the web gui. Using vnc in gns3 can cause issues not being able to cut & paste so its best to just juse the cli as a last resort.

## Information/Overview
Have gns3 up and running and using the F5 appliance with BIGIP VE installed. I have this running and connected to a switch. Also using firefox tiny linux for the GUI access when needed.

## Prerequisites:
- F5 appliance installed
- F5 BIGIP VE installed
- BIGIP running on gns3

## Procedures

**1. Fill out the follwing form to get a Registration Key from F5**

https://downloads.f5.com/trial/

**2. Log into F5 BIG-IP using the cli**
```
User:root
PW: default
```

**3. Run the dossier command to get an output hash**

`> get_dossier -b ABCDE-ABCDE-ABCDE-ABCDE-ABCDEFG   <-- use reg key mailed to you for trial`

**4. Cut the output from the dossier command**

**5. Log into F5 license website and paste the dossier output**

https://activate.f5.com/license

Select NEXT

**6. Copy the activation output**

**7. Now need to create the bigip.license file with the activation code**

`> vi /config/bigip.license`

- Press "i" for insert mode
- Paste activation output into the new file

  NOTE: Make sure now empty lines on top or bottom of text

- Press <SHIFT>+ZZ   <- This will save and close the newly created file

**8. Reload the license**

`> reloadlic`


Now the output of the line should say "Active:Standalone"
