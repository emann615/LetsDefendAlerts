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

I searched the email subject (RE: Meeting Notes) on the Email Security page and found an email that corresponds to the alert. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/eb719a6f-6db9-4081-aafd-c78d8f6a969f" height="80%" width="80%"/>
</br>
</br>

The email contains an attachment to a zip file.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/aba6a1a6-430d-4844-96a6-c5eb2da934de" height="80%" width="80%"/>
</br>
</br>

### Analyze Url/Attachment

I downloaded the file in a sandbox environment and unzipped the file. I found three different files inside the folder, two dll files and one excel file.
- iroto.dll 
- iroto1.dll
- research-1646684671.xls

I went to VirusTotal and analyzed all three files. The iroto.dll file was flagged as malicious by 8/70 vendors. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/1d6b63d8-1b10-425b-819f-0428cbe373c0" height="80%" width="80%"/>
</br>
</br>

The iroto1.dll file was flagged as malicious by 10/69 vendors. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/bdc2389c-ceb7-4512-bfde-9ae2c9af748c" height="80%" width="80%"/>
</br>
</br>

The research-1646684671.xls file was flagged as malicious by 38/60 vendors. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/30420173-b12d-4fd1-9858-c0bec9940f2d" height="80%" width="80%"/>
</br>
</br>

Next, I analyzed the files with Hybrid Analysis. All three files were identified as malicious with a Threat Score of 100/100

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/dc6c6bb8-5bae-4bab-bc39-0081262fd9bd" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/aaedf717-5b23-4240-8dfa-6b34785cbdcf" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2c6e685d-9574-4af8-8b10-238ec32096c1" height="80%" width="80%"/>
</br>
</br>

I analyzed the research-1646684671.xls file with AnyRun. Malicious activity was identified. The file creates 2 regsvr32.exe processes, one for the iroto.dll file and another one for the iroto1.dll file. The file also makes a connection to IP address 188.213.19.81. This appears to be the C2 address.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Check If Mail Delivered to User?

The alert shows that device action was allowed, indicating that the email was delivered to the user.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Delete Email From Recipient!

On the Email Security page, I deleted the email.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Check If Someone Opened the Malicious File/URL?

On the Log Management page, I searched the C2 address (188.213.19.81) and found one entry. The source address is 172.16.17.57.

<img src="" height="80%" width="80%"/>
</br>
</br>

I went to the Endpoint Security page and searched 172.16.17.57. The IP address is associated with the LarsPRD device.

<img src="" height="80%" width="80%"/>
</br>
</br>

I checked the process history for the device and see that Excel created a regsvr32.exe process to register the iroto.dll file. The is the same process I saw when I analyzed the research-1646684671.xls file in AnyRun.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Containment

The LarsPRD computer was contained to prevent the spread of the attack.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Add Artifacts

<img src="" height="80%" width="80%"/>
</br>
</br>

## Analyst Note

<img src="" height="80%" width="80%"/>
</br>
</br>

## Results

<img src="" height="80%" width="80%"/>
</br>
</br>
