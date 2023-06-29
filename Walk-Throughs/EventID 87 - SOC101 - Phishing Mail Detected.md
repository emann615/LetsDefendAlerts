# EventID 87 - SOC101 - Phishing Mail Detected

## Alert

The Monitoring page shows that this alert was triggered because phishing mail was detected. I took ownership of the alert, created a case, and started the playbook

<img src="" height="80%" width="80%"/>
</br>
</br>

## Parse Email

When was it sent? Apr, 04, 2021, 11:00 PM
What is the email's SMTP address? 146.56.195.192
What is the sender address? lethuyan852@gmail.com
What is the recipient address? mark@letsdefend.io
Is the mail content suspicious? Yes
Are there any attachment? No

## Are there attachments or URLs in the email?

I went to the Email Security page and found the email by searching the email subject included in the alert. There are no attachements, but there is a URL (http://nuangaybantiep.xyz) in the body of the email.

<img src="" height="80%" width="80%"/>
</br>
</br>

I analyzed the URL in VirusTotal. Only 1/89 vendors flagged the URL as malicious.

<img src="" height="80%" width="80%"/>
</br>
</br>

I also took a look at the Joe Snadbox analysis report for the URL. The report identifies the URL as suspicious. The URL is currently not reachable, but appears to have previously been used to spread a trojan.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Check If Mail Delivered to User?

The alert shows that Device Action was Allowed, indicating that the email was delivered to the user.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Check If Someone Opened the Malicios File/URL?

I went to the Log Management page and searched for the URL (http://nuangaybantiep.xyz). One log entry was returned with a source IP address of 172.16.17.88 and a destination IP address of 192.64.119.190. 

<img src="" height="80%" width="80%"/>
</br>
</br>

The raw data for the log shows the same URL I found in the email.

<img src="" height="80%" width="80%"/>
</br>
</br>

On the Endpoint Security page, I searched the source IP address from the log entry. It belongs to the MarkPRD device.

<img src="" height="80%" width="80%"/>
</br>
</br>

Base on this information, the URL was accessed from the MarkPRD device.

## Containment

I contained the device to prevent the spread of the attack.

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

