# EventID 93 - SOC146 - Phishing Mail Detected - Excel 4.0 Macros

## Alert

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/d1def34f-76d0-4791-a663-e5e5062db801" height="80%" width="80%"/>
</br>
</br>

## Parse Email

* When was it sent? Jun, 13, 2021, 02:13 PM
* What is the email's SMTP address? 24.213.228.54
* What is the sender address? trenton@tritowncomputers.com
* What is the recipient address? lars@letsdefend.io
* Is the mail content suspicious? Yes
* Are there any attachment? Yes

### Are there attachments or URLs in the email?

I searched the  email subject (RE: Meeting Notes) on the Email Security page and found an email that corresponds to the alert. The email contains an attachment to a zip file.

### Analyze Url/Attachment

I downloaded the file in a sandbox environment and unzipped the file. I found three different files inside the folder, two dll files and one excel file.
- iroto.dll 
- iroto1.dll
- research-1646684671.xls

I went to VirusTotal and analyzed all three files. The iroto.dll file was flagged as malicious by 8/70 vendors. The iroto1.dll file was flagged as malicious by 10/69 vendors. The research-1646684671.xls file was flagged as malicious by 38/60 vendors. All three files were labeled as trojans.
- MD5: e03bde4862d4d93ac2ceed85abf50b18 - iroto.dll 
- MD5: 8e6fbefcbac2a1967941fa692c82c3ca - iroto1.dll
- MD5: b775cd8be83696ca37b2fe00bcb40574 - research-1646684671.xls


Next, I analyzed the files with Hybrid Analysis. All three files were identified as malicious with a Threat Score of 100/100

I analyzed the research-1646684671.xls file with AnyRun. Malicious activity was identified. The file creates 2 regsvr32.exe processes, one for the iroto.dll file and another one for the iroto1.dll file. The file also makes a connection to IP address 188.213.19.81. This appears to be the C2 address.

## Check If Mail Delivered to User?

The alert shows that device action was allowed, indicating that the email was delivered to the user.

## Delete Email From Recipient!

On the Email Security page, I deleted the email.

## Check If Someone Opened the Malicious File/URL?

On the Log Management page, I searched the C2 address (188.213.19.81) and found one entry. The source address is 172.16.17.57.

I went to the Endpoint Security page and searched 172.16.17.57. The IP address is associated with the LarsPRD device.

I checked the process history for the device and see that Excel created a regsvr32.exe process to register the iroto.dll file. The is the same process I saw when I analyzed the research-1646684671.xls file in AnyRun.

## Containment

The LarsPRD computer was contained to prevent the spread of the attack.

## Add Artifacts

## Analyst Note
