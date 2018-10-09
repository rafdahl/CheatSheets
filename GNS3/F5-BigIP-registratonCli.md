1. Fill out to get Registration Key from F5

(https://downloads.f5.com/trial/)

2. Log into F5 BIG-IP using cli
```
User:root
PW: default
```

3. Run dossier command to get output hash

`> get_dossier -b ABCDE-ABCDE-ABCDE-ABCDE-ABCDEFG   <-- use reg key mailed to you for trial`

4. Cut the output from the dossier command

5. Log into F5 license website and paste the dossier output

(https://activate.f5.com/license)

Select NEXT

6. Copy the activation output

7. Now need to create the bigip.license file with the activation code

`> vi /config/bigip.license`

- Press "i" for insert mode
- Paste activation output into new the new file

NOTE: Make sure now empty lines on top or bottom of text

- Press <SHIFT>+ZZ   <- This will save and close the newly created file

8. Reload the license

`> reloadlic`


Now the output of the line should say "Active:Standalone"
