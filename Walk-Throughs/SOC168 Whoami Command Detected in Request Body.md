# EventID 118 - SOC168 - Whoami Command Detected in Request Body

## Alert

On the Monitoring page, I see that the alert was triggered because a whoami command was detected in a HTTP request. I took ownership of the alert and created a case, so I can start the playbook.

## Collect Data

I went to the Endpoint Security page and did a search for the destination IP address and source IP address to see if they belong to the internal network. The destination IP address (172.16.17.16) is associated with WebServer1004 on the internal network. No results were populated for the source IP address (61.177.172.87), indicating it is from an external network.

I searched 61.177.172.87 in AbuseIPDB to find information on its ownership and reputation. The ISP is ChinaNet Jiangsu Province Network, based out of China. The IP address has been reported 87,677 times, and the Confidence of Abuse is 0%.

I searched 61.177.172.87 in Cisco Talos IP & Domain Reputation Center. It shows the Sender IP Reputation is Poor.

I searched 61.177.172.87 in VirtusTotal. The last analysis date was 15 days ago, so I reanalyzed the IP address. the results show that 7/89 vendors flagged the IP address as malicious.

I searched 61.177.172.87 in Hybrid Analysis. The IP address was identified as malicious with a Threat Score of 100/100.

## Examine HTTP Traffic

Monitoring
- No evidence of command injection in the Requested URL on the alert.

Log Management
- I searched 61.177.172.87.
	- Multiple (5) log entries were returned.
- I examined the raw data for each entry to see the full HTTP request headers.
- All the requests were targeting the Video page.
- There is evidence of command injection in the POST Parameters header.
- Each request has a HTTP Response Status of 200 and the HTTP Response Size was different for each request.

## Is Traffic Malicious?

- Yes, the traffic appears to be malicious.

## What Is The Attack Type?

- The attack type is Command Injection.

## Check If It Is a Planned Test

- On the Email Security page, I searched the hostname, destination IP address, and source IP address to see if there are any emails indicating that this was a planned test. No results were returned, so this does not appear to be a planned test.

## What Is the Direction of Traffic?

- The source IP address is from an external network, and the destination IP address is associated with a server on the internal network. This indicates that the direction of traffic is **Internet -> Company Network**.

## Check Whether the Attack Was Successful

Endpoint Security
- I checked the Terminal History of WebServer1004.
- I see the commands that were sent in the HTTP request are reflected in the command history on the server.
- This indicates that the attack was successful.

### Was the Attack Successful?

Yes, the attack was successful.

## Containment

Endpoint Security
- Since the server was compromised, I requested containment of the host to prevent the spread of the attack and reduce the impact.

## Add Artifacts

- 61.177.172.87 - Attacker's IP address
- 172.16.17.16 - Compromised server's IP address

## Do You Need Tier 2 Escalation?

- Based on the organizations escalation policy, escalation of the case is required because the attack was successful.

## Analyst Note

61.177.172.87 attacked WebServer1004 using command injection. The command history for WebServer1004 shows that the attack was successful. WebServer1004 has been contained to prevent the spread of the attack, and the case has been escalated to tier 2.
