## Creating New CF disk for T68KRC
### Install CP/M-68K in new CF track 1
- Insert a CF disk in the adapter. WARNING: the content of the CF will be erased.
- clear the memory from 0x15000 to 0x20000 with the program “[clrcpmmem.s68](software/t68krc_rev01_software_clrcpmmem.zip)”. Use the “send text file” command of your terminal program to upload. This program will auto-execute when file loading is finished. When program execution is completed it will display “S record execution completed” and prompt for more inputs. Please note that source & listing are included in the zip file, only upload the file with .s68 extension.
- upload “CPM15000.s68 ”. This is the CP/M-68K CCP and BDOS. Wait for the input prompt after about 15 seconds.
- upload “T68KBIOS.s68 ”. This is the BIOS specific to the T68KRC. The current revision is rev 1
- lastly upload “writeBoot.s68 ”. This will write CCP, BDOS, and BIOS into track1 of CF disk.
### Load CP/M-68K distribution files in drive E:
Now CP/M68K BIOS/CCP/BDOS are installed in CF drive, the next step is to load the CP/M68K distribution files in RAM drive (drive E:).

Send the file T68KRCRAM.S68. This will take about 15 minutes. When the file load is completed, execute the monitor 'bo' command. This will copy the software in track 1 to memory starting at 0x15000 and then jump to it. A checksum will be displayed which should be '0C0F1FBA' and CP/M 'A>' prompt should be displayed. A CPM 'DIR' command may display random data because there are no meaningful directory structure in the CF at this time. When 'DIR' command is executing, the tiny red LED on the 44-pin CF adapter should flicker indicating access to CF.
