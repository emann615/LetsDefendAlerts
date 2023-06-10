# EventID 117 - SOC167 - LS Command Detected in Requested URL
## Alert

On the Monitoring page, I see that the alert was triggered because a ls command was detected in the requested URL. I take ownership of the alert and create a case, so I can start the playbook.

## Data Collected

I went to the Endpoint Security page and did a search for the destination IP address (188.114.96.15) to see if it was on the internal network. The results returned EliotPRD, but the IP address for that device does not match. The IP address for EliotPRD actually matches the source IP address (172.16.17.46) on the alert. 

I also saw that the primary user for that device is Eliot, and the last login was on Feb, 27, 2022, 12:00 AM. Based on this information, the source IP address belongs to the internal network, and the destination IP address is from an external network. The HTTP request was sent from the EliotPRD device to a device (188.114.96.15) on the internet.

## Examine HTTP Traffic

I went to the Log Management page to see if there are any entries that correspond to the alert. I searched the destination IP address (188.114.96.15), and multiple entries were returned.

I checked the raw log data for the entry that occurred at the time of the alert. There is no indication of a command injection attack in the HTTP request. It appears the alert was most likely triggered because the user searched the word "skills" on the blog page.

I checked the raw data for the other log entries to confirm that there is no malicious activity in any of the other HTTP traffic. I could find no evidence of malicious activity.

On the Endpoint Security page, I checked the browser history for EliotPRD. Based on the browser history, I can see that the user was browsing a blog page on the domain letsdefend.io, and searched the word "skills". These records match what I saw in the logs.

## Is Traffic Malicious?

Based of the information found in my investigation, the traffic is not malicious, and the alert is a false positive.

## Analyst Note

## Result
