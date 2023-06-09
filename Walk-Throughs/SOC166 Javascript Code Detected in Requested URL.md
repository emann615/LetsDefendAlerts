# EventID 116 - SOC166 - Javascript Code Detected in Requested URL

## Alert

The Monitoring page shows that this alert was triggered because JavaScript code was detected in a Requested URL. I took ownership of the alert and create a case, so I can start the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/e0abc9dc-afff-4d32-9989-013d70e48885" height="80%" width="80%"/>
</br>
</br>

## Collect Data

I searched the Endpoint Security page to see if the source IP address or destination IP address belongs to the internal network. The destination IP address (172.16.17.17) is associated with WebServer1002 on the internal network. There were no results for the source IP address (112.85.42.13), indicating that it is outside the network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a0a3b2c9-7f1e-49b1-8901-a9139b40331e" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/168e0a11-e57c-487c-ab81-40f91e982161" height="80%" width="80%"/>
</br>
</br>

I searched 112.85.42.13 in AbuseIPDB to see what information I could find on the ownership and reputation. The results show its ISP is China Unicom Jiangsu Province Network. The IP address has been reported 45,587 times, but the Confidence of Abuse is 1%.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/30beed4f-85eb-4c67-84e1-4e5351b1224a" height="80%" width="80%"/>
</br>
</br>

In order to find more information on the reputation, I searched 112.85.42.13 in Cisco Talos IP & Domain Reputation Center. It shows the IP reputation is Poor.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/c263d297-cbf9-4f0e-a617-556cb2cb5dae" height="80%" width="80%"/>
</br>
</br>

I also searched 112.85.42.13 in VirusTotal. The last analysis was 16 days ago, so I reanalyzed the IP address. The results show 4/89 vendors flagged the IP address as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/71fbc329-971d-4af7-baf5-a2d91e003510" height="80%" width="80%"/>
</br>
</br>

I searched 112.85.42.13 in Hybrid Analysis to get an additional source on the IP address reputation. The results identified the IP address as malicious with a Threat Score of 100/100.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/61f89c0b-17b2-4097-a052-58c36681b2c0" height="80%" width="80%"/>
</br>
</br>

## Examine HTTP Traffic

After examining the requested URL, I was able to confirm it does contain a script.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/35fb6322-ed00-4de8-b79d-20bf3a64b10b" height="80%" width="80%"/>
</br>
</br>

## Is the Traffic Malicious

Based on the information found in the previous step of my investigation, the traffic appears to be malicious. JavaScript code has been inserted into the requested URL, and the source IP address (112.85.42.13) has been identified as malicious by multiple sources.

### What Is The Attack Type?

The attack type is XSS, because a malicious script has been inserted into the requested URL.

### Check If It Is a Planned Test

<img src="" height="80%" width="80%"/>
</br>
</br>

On the Email Security page, I searched the hostname, destination IP address, and source IP address to see if there are any emails indicating that this was a planned test. No results were returned, so this does not appear to be a planned test.

### What Is the Direction of Traffic?

<img src="" height="80%" width="80%"/>
</br>
</br>

The source IP address is from the internet, and the destination IP address is associated with a server on the internal network. This indicates that the direction of traffic is **Internet -> Company Network**.

### Check Whether the Attack Was Successful

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched the source IP address (112.85.42.13) on the Log Management page to see if there is any information indicated whether or not the attack was successful. Multiple log entries were returned.

After checking the raw logs for each entry, I was able to see that multiple attempts at XSS were made. The HTTP Response Size was 0, and the HTTP Response Status was 302 for all the XSS attempts, indicating that the attack was not successful.

### Was the Attack Successful?

<img src="" height="80%" width="80%"/>
</br>
</br>

Based on the findings in the previous step of my investigation, the attack was not successful.

### Add Artifacts

<img src="" height="80%" width="80%"/>
</br>
</br>

### Do You Need Tier 2 Escalation?

<img src="" height="80%" width="80%"/>
</br>
</br>

There is no need to escalate the case since the attack was not successful, and it originated from an external IP address.

## Analyst Note

<img src="" height="80%" width="80%"/>
</br>
</br>

There were multiple attempts by 112.85.42.13 to attack WebServer1002 using XSS. All attempts resulted in a HTTP response status of 302 and a HTTP response size of 0, indicating that the attack was not successful.
