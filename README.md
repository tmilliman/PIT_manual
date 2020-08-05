# Instruction for PhenoCam Installation Tool
PhenoCam Installation Tool (PIT) is a set of scripts for Linux/Mac OSX and Windows taking care of the settings as needed by cameras installed by or associated with the [PhenoCam Network](http://phenocam.sr.unh.edu/). We try to explain this in few simple steps as follows.

## Software Prerequisites
For the script to run successfully you will need a `Telnet` client. `Telnet` is not installed by default on recent updates of MacOS or Windows machines but can still be manually installed. For instructions on how to enable `Telnet` check out the following links for different operating systems:

- **Windows 7**: See this article to [Enable Telnet in Windows 7 from WikiHow](https://www.wikihow.com/Activate-Telnet-in-Windows-7)
- **Windows 10**: See this article to [Enable Telnet in Windows 10 from Miscrosft](https://social.technet.microsoft.com/wiki/contents/articles/38433.windows-10-enabling-telnet-client.aspx)
- **Mac OS**: You can install telnet using the Homebrew framework using the following commands (skip the first if you have brew running).
```{shell}
# install brew (this might take a while)
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# install telnet
brew install telnet
```

## Download the PIT
The first step to download the PIT as a zip file from [here](https://github.com/khufkens/phenocam-installation-tool/zipball/master). 
Once the zip file was downloaded, extract the file take a note where the extracted directory is located on your machine. You will need this for the next step

## Use the PIT
The installation script runs within a terminal on all platforms. To open a terminal search for “Terminal” in OSX spotlight or “Command Prompt” in the program search field (under the Start button) in Windows. The installation requires you to have a working internet connection on the camera. Make sure the camera and the computer are on the same network. *Note:* Do not connect the camera directly to the computer. 

1. Open the `Terminal` or the `Command Prompt` and change the directory to where you extracted the zip file using the `cd` command. e.g.
```{shell}
cd ~/Downloads/khufkens-phenocam-installation-tool-53553a6/
```

2. Enter the `PIT` command as described by examples below:
**On Windows:**  
```{shell}
PIT.bat IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```

**On Linux / Mac OS:** 
```{shell}
sh PIT.sh IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```
or
```{shell}
./PIT.sh IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```

with the following parameters:

| Parameter | Description |
| ----------- | ----------- |
| IP | IP address of the camera |
| USER | Username (default: admin) |
| PASSWORD | User password (default: admin, update if the password has changed) |
| CAMERA | the name of the camera / site |
| TIME_OFFSET | difference in hours from UTC of the time zone in which the camera resides (always use + or - signs to denote differences from UTC) |
| TZ | a text string corresponding to the local time zone (e.g. EST) |
| CRON_START | first hour of the scheduled image acquisitions (e.g. 4 in the morning) |
| CRON_END | last hour of the scheduled image acquisitions (e.g. ten at night, so 22 in 24-h notation) |
| CRON_INT | interval at which to take pictures (e.g. 15, every 15 minutes - default phenocam setting is 30) |
| FTP_MODE | active or passive (default = passive) |


An example of our test camera configuration:
```{shell}
./PIT.sh 140.247.89.xx admin admin testcam3 -5 EST 4 22 30 passive
```
