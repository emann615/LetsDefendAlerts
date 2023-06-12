# EventID 118 - SOC168 - Whoami Command Detected in Request Body

## Alert

On the Monitoring page, I see that the alert was triggered because a whoami command was detected in a HTTP request. I took ownership of the alert and created a case, so I can start the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/86c8c253-9919-49fc-9e51-2e0a7e92005e" height="80%" width="80%"/>
</br>
</br>

## Collect Data

I went to the Endpoint Security page, and did a search for the destination IP address and source IP address to see if they belong to the internal network. The destination IP address (172.16.17.16) is associated with WebServer1004 on the internal network. No results were populated for the source IP address (61.177.172.87), indicating it is from an external network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/b1cf681c-b2d6-4728-99d8-71899e01071b" height="80%" width="80%"/>
</br>
</br>

I searched 61.177.172.87 in AbuseIPDB to find information on its ownership and reputation. The ISP is ChinaNet Jiangsu Province Network, based out of China. The IP address has been reported 87,677 times, and the Confidence of Abuse is 0%.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/051cc705-fecd-4110-8178-d0d655eb3897" height="80%" width="80%"/>
</br>
</br>

I searched 61.177.172.87 in Cisco Talos IP & Domain Reputation Center. It shows the Sender IP Reputation is Poor.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/c8a8d744-1d68-4a00-8343-942bf502c665" height="80%" width="80%"/>
</br>
</br>

I searched 61.177.172.87 in VirtusTotal. The last analysis date was 15 days ago, so I reanalyzed the IP address. the results show that 7/89 vendors flagged the IP address as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/01be3c05-5022-4fd1-abc7-4cc0c594a678" height="80%" width="80%"/>
</br>
</br>

I searched 61.177.172.87 in Hybrid Analysis. The IP address was identified as malicious with a Threat Score of 100/100.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/1669f105-dd70-41ca-bc57-e42da72f8337" height="80%" width="80%"/>
</br>
</br>

## Examine HTTP Traffic

On the Log Management page, I searched the source IP address (61.177.172.87) and found multiple log entries. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/62adcc10-3f5c-4d41-999b-61a8070385ad" height="80%" width="80%"/>
</br>
</br>

I examined the raw data for each entry to see the full HTTP request headers. All the requests were targeting a video page. There is evidence of command injection in the POST Parameters header. Each request has a HTTP Response Status of 200 and the HTTP Response Size was different for each request.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/5d6326ca-2a10-4753-9b2f-0c45835002ad" height="80%" width="80%"/>
</br>
</br>

## Is Traffic Malicious?

Based on the information found after analyzing the source IP address and the raw log data that corresponds with the alert, the traffic appears to be malicious.

## What Is The Attack Type?

After examining the logs of the HTTP traffi, I found evidence of terminal commands included in the HTTP requests. This indicates the attack type is Command Injection.

## Check If It Is a Planned Test

On the Email Security page, I searched the hostname, destination IP address, and source IP address to see if there are any emails indicating that this was a planned test. No results were returned, so this does not appear to be a planned test.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/744fd0a1-77c4-4e63-a7a4-f6418f10d382" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/293d7c92-149e-4727-8d39-9951647fed12" height="80%" width="80%"/>
</br>
</br>

<img src="" height="80%" width="80%"/>
</br>
</br>

## What Is the Direction of Traffic?

The source IP address is from an external network, and the destination IP address is associated with a server on the internal network. This indicates that the direction of traffic is **Internet -> Company Network**.

## Was the Attack Successful?

On the Endpoint Security page, I checked the Terminal History of WebServer1004. I saw the same commands that were sent in the HTTP request are reflected in the command history on the server. This indicates that the attack was successful.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Containment

Since the server was compromised, I contained the host to prevent the spread of the attack and reduce the impact.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Add Artifacts

61.177.172.87 - Attacker's IP address
172.16.17.16 - Compromised server's IP address

<img src="" height="80%" width="80%"/>
</br>
</br>

## Do You Need Tier 2 Escalation?

Based on the organizations escalation policy, escalation of the case is required because the attack was successful.

## Analyst Note

<img src="" height="80%" width="80%"/>
</br>
</br>

61.177.172.87 attacked WebServer1004 using command injection. The command history for WebServer1004 shows that the attack was successful. WebServer1004 has been contained to prevent the spread of the attack, and the case has been escalated to tier 2.
