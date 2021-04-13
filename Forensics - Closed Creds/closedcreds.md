## closed-creds

_200 points, 30 solves_

The clues from the camera led you to a mysterious building. Surprisingly, the front door was left unlocked. Unsurprisingly, the computer in the headquarters was not left unlocked. Using the registry files provided, will you be able to crack the password of the Administrator user?

[Files]()


### Approach

Since the hint for the previous and somewhat related challenge (Investigating Windows) was to use regripper, I had a feeling that this would require the use of it too.

Launching regripper, we are able to select a hive file--based on the 5 common Windows hive files, a report file to save the information extracted (override where necessary), as well as a plugin file which contains filters/commonly used characters used in these hives (probably through the use of some regex - I might be wrong and have to do some further reading about this...)

Thereafter, we can press the `Rip` button and leave regripper to do its thing. Once complete, regripper outputs the report file and a corresponding log file which details extracted information and errors if any (more verbose than the GUI).

However, I soon realised that this was unlikely the case. The hint read: `Research dumping hashes from SAM.` Hmm ok so I quickly proceeded to do this and cane across the command 
```
$ samdump2 system SAM
```

which extracts the strings from the SAM hive to a human readable colon demarcated string of hashes of the users on the system.

Thereafter, I proceeded to crack the hashes using https://crackstation.net/ since I was lazy lol... They could probably be cracked with JohnTheRipper and other tools like hashcat but I preferred a GUI-based cracker at this point of the competition. After removing the colons, we get the flag from the second hash, which we just need to wrap in the format. 