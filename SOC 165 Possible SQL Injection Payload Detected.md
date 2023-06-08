# EventID 115 - SOC165 - Possible SQL Injection Payload Detected

## Collect Data

I searched the Endpoint Security tool to see if either of the IP addresses are owned by the internal network.
* The destination IP address 172.16.17.18 is associated with WebServer1001.
* The source IP address 167.99.169.17 did not return any results, indicating that it is outside the network.
   
I searched 167.99.169.17 in AbuseIPDB to identify the owner and IP address reputation.
* It shows that the ISP is DigitalOcean LLC
* The IP was reported 15,152 times, but the Confidence of Abuse is 0%.

Next, I searched 167.99.169.17 in Cisco Talos IP & Domain Reputation Center
* It shows the IP reputation as Neutral.

Since Abuse IPDB and Cisco Talos were inconclusive, I checked VirusTotal.
- VirusTotal shows that 9 vendors identified the IP address as malicious.

I still wanted a second source to confirm that the IP is malicious, so I also checked Hybrid Analysis.
* The results show that the IP is malicious with a Threat Score of 100/100

## Examine HTTP Traffic

I used a URL decoder to decode and examine the URL in the HTTP Request.
* Decoded URL: https://172.16.17.18/search/?q=" OR 1 = 1 -- -
  * The decoded URL indicates **SQL injection** is the attack method.

## Check If It Is a Planned Test

I searched the source IP address, destination Ip address, and hostname in the Email Security tool.
* No results were populated so their is no indication that this was a planned test.
* There is also no indication that an attack simulation product was used.

## What is the Direction of Traffic?

Based on the investigation so far, I know the source IP address is from the internet and the destination Ip address if from the internal network.
* Therefor the direction of traffic is **Internet -> Company Network**.

## Check Whether the Attack Was Successful

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
