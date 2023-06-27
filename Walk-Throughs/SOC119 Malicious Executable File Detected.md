# EventID 83 - SOC119 - Proxy - Malicious Executable File Detected

## Alert

## Collection Data

I was able to find the following information from the alert:
* Source Address: 172.16.17.5
* Destination Address: 51.195.68.163
* User-Agent: Chrome - Windows

## Search Log

On the Log Management page, I filtered for the source address (172.16.17.5), and two entries were returned. One of the entries corresponds to the time of the alert. I took a look at the raw log data, but didn't find anything particularly interesting or suspicious.

## Analyze URL Address

I went to VirusTotal and searched the the requested URL. Only 1/90 vendors flagged the URL as malicious. 

Next, I searched the destination IP address (51.195.68.163). The results show that 0/88 vendors flagged the IP address as malicious.

I also searched 51.195.68.163 in Hybrid Analysis. No threats were identified.

I used a sandbox environment to view the page the requested URL directs to. The page downloads the winrar-x32-622.exe file, which is an installer for WinRAR.

I analyzed the file in VirusTotal, and 0/71 vendors flagged the file as malicious.

I also analyzed the file in Hybrid Analysis, and the results came back clean.

In order to see what happens when the file is executed, I analyzed it with AnyRun. The file was flagged as malicious, but further examination of the processes created when the file is executed showed no signs of anything out of the ordinary. It simply installs WinRAR as you would expect. Despite being flagged as malicious, the file does not appear to actually do anything malicious.

## Add Artifacts

4948d0c9e52f69510e082c0f18e09de0 - WinRAR.exe
https://www.win-rar.com/postdownload.html?&L=0&Version=32bit - WinRAR download page

## Analyst Note

The requested URL directs to the official WinRAR site and downloads the installer. The file is not malicious, and no further action is required.
