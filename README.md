# Instruction for PhenoCam Installation Tool
PhenoCam Installation Tool (PIT) is a command line script which is used to configure a StarDot camera for the [PhenoCam Network](http://phenocam.sr.unh.edu/). There are separate versions for Linux/Mac OSX (PIT.sh) and Windows (PIT.bat). In this document we try to explain how to run the script in a few simple steps.  For a more detailed description refer to the PIT [github page](https://github.com/khufkens/phenocam-installation-tool/zipball/master).

## Software Prerequisites
For the script to run successfully, you will need a `telnet` client. Because `telnet` is a legacy protocol and is not considered secure it is not installed by default on recent versions of most operating systems. It can however still be manually installed. For instructions on how to enable `Telnet` check out the following instructions/links for different the operating systems:

- **Windows 7**: See this article to [Enable Telnet in Windows 7 from WikiHow](https://www.wikihow.com/Activate-Telnet-in-Windows-7)
- **Windows 10**: See this article to [Enable Telnet in Windows 10 from Microsoft](https://social.technet.microsoft.com/wiki/contents/articles/38433.windows-10-enabling-telnet-client.aspx)
- **MacOS**:
You can install telnet using the Homebrew framework by typing the following commands in a terminal window.  Skip the first if you already have `brew` running.
```{shell}
# install brew (this might take a while)
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# install telnet
brew install telnet
```
- **Linux**: Most linux distributions will provide a telnet package but not install it by default.  Search for telnet using the standard packaging
tools for your distribution.  

For debian/ubuntu you would type the following command in a terminal window:
```
sudo apt install telnet
```
For CentOS/RHEL/Scientific Linux:
```
yum install telnet -y
```

## Download the PIT
The first step is to download the PIT as a zip file from [here](https://github.com/khufkens/phenocam-installation-tool/zipball/master). 
Once the zip file was downloaded, extract the file and take a note where the extracted directory is located on your machine. 
You will need this for the next step.  Typically, this will be in a Downloads directory/folder, e.g. Downloads/ 

## Use the PIT
The installation script runs within a terminal on all platforms. To open a terminal search for the `Terminal` in MacOS spotlight or the `Command Prompt` in the program search field in Windows. Make sure the camera and the computer are on the same network with internet access. [*Note:* Do not connect the camera directly to the computer.]

1. Open the `Terminal` or the `Command Prompt` and change the directory to where you extracted the zip file using the `cd` command. e.g.

**On Windows:**  
```{shell}
cd Downloads\khufkens-phenocam-installation-tool-53553a6
```
**On Linux / MacOS:**
```{shell}
cd ~/Downloads/khufkens-phenocam-installation-tool-53553a6/
```

2. Enter the `PIT` command as described by examples below:

**On Windows:**  
```{shell}
PIT.bat IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```

**On Linux / MacOS:** 
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
