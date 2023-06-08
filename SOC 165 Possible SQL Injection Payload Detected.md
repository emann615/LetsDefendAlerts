# EventID 115 - SOC165 - Possible SQL Injection Payload Detected

## Alert

Looking at the Monitoring page, I see an alert was triggered because a poddible SQL injection payload was detected.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/0b5cb554-2194-4a33-819e-7b6b59276187" height="80%" width="80%"/>
</br>
</br>

I take ownership of the alert and create a case, so I cant start the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/f2d64f00-ec61-4cb6-892e-1f3944aaafd3" height="80%" width="80%"/>
</br>
</br>

## Collect Data

First, I must collect some basic data about the attack, including the ownership and reputation of the IP adresses involved.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/6d741aa8-6e9c-465e-a52f-f50909b950e2" height="80%" width="80%"/>
</br>
</br>

I searched the Endpoint Security tool to see if either of the IP addresses are owned by the internal network.
* The destination IP address 172.16.17.18 is associated with WebServer1001.
* The source IP address 167.99.169.17 did not return any results, indicating that it is outside the network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2b4f5c07-4713-4daa-9c75-4bb81db51787" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/f56978f0-b32a-4959-812f-504bb044e9c4" height="80%" width="80%"/>
</br>
</br>

I searched 167.99.169.17 in AbuseIPDB to identify the owner and IP address reputation.
* It shows that the ISP is DigitalOcean LLC
* The IP was reported 15,152 times, but the Confidence of Abuse is 0%.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/95612cf6-6357-4a07-a438-161f0d99cb01" height="80%" width="80%"/>
</br>
</br>

Next, I searched 167.99.169.17 in Cisco Talos IP & Domain Reputation Center
* It shows the IP reputation as Neutral.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/31644863-71df-423a-b154-92c80fb90cf4" height="80%" width="80%"/>
</br>
</br>

Since Abuse IPDB and Cisco Talos were inconclusive, I checked VirusTotal.
- VirusTotal shows that 9 vendors identified the IP address as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2b8dfcc3-270f-493e-9a0a-57693846a82b" height="80%" width="80%"/>
</br>
</br>

I still wanted a second source to confirm that the IP is malicious, so I also checked Hybrid Analysis.
* The results show that the IP is malicious with a Threat Score of 100/100

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/10bb51ca-d1f8-47e4-ac77-0239b91c3056" height="80%" width="80%"/>
</br>
</br>

## Examine HTTP Traffic

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/f26b7874-4e5f-4af7-ad45-e29efb7af1e9" height="80%" width="80%"/>
</br>
</br>

I used a URL decoder to decode and examine the URL in the HTTP Request.
* Decoded URL: https://172.16.17.18/search/?q=" OR 1 = 1 -- -
  * The decoded URL indicates **SQL injection** is the attack method.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2d4d2afc-b29b-4fc8-8ceb-4b90002a6403" height="80%" width="80%"/>
</br>
</br>

## Check If It Is a Planned Test

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/fdee709c-36dd-4f65-b519-d213e196dba9" height="80%" width="80%"/>
</br>
</br>

I searched the source IP address, destination Ip address, and hostname in the Email Security tool.
* No results were populated, so their is no indication that this was a planned test.
* There is also no indication that an attack simulation product was used.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/9b20c0b0-efce-4f82-9763-d05ef4c78920" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/bb30c54b-93a3-4807-bbad-b67fef846700" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2944b804-c84f-4257-ac15-c3138697a1d8" height="80%" width="80%"/>
</br>
</br>

## What is the Direction of Traffic?

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2944b804-c84f-4257-ac15-c3138697a1d8" height="80%" width="80%"/>
</br>
</br>

Based on the investigation so far, I know the source IP address is from the internet and the destination Ip address if from the internal network.
* Therefor the direction of traffic is **Internet -> Company Network**.

## Check Whether the Attack Was Successful

<img src="" height="80%" width="80%"/>
</br>
</br>

I checked the Log Managment tool to see if there was any indication that the attack was successful.
* I searched the source IP (167.99.169.17) and found multiple log entries.
* Based on the raw logs it looks like there were multiple HTTP requests sent attempting SQL injection.
* all of the request resulted in a status code of 500 and a response size of 948.
* I decoded URLs found in each HTTP requests.
* The decoded URLs show that multiple SQLi medthods were attempted.
* Since mulitple there were multiple SQLi attempts using different methods that resulted in a consistent response size of 948, this indicates that that the attack was not successful.

I laso checked the Command History for WebServer1001 in the Endpoint Security tool.
* The command history shows no indication that the attack was successful.

## Do You Need Tier 2 Escalation?

Since the attack the attack was not successful and it did not originate from the internal network, there is no need to escalate.

## Analyst Note
