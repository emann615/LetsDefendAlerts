# EventID 120 - SOC170 - Passwd Found in Requested URL - Possible LFI Attack

## Alert

On the Monitoring page, I see that the alert was triggered because "passwd" was found in the requested URL, indicating a possible LFI attack. I took ownership of the alert and created a case, so I can start the playbook.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Data Collection

I went to the Endpoint Security page, and did a search for the destination IP address and source IP address to see if they belong to the internal network. The destination IP address (172.16.17.13) is associated with WebServer1006 on the internal network. The source IP address (106.55.45.162) did not return any results, indicating it is from an external network.

<img src="" height="80%" width="80%"/>
</br>
</br>

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in AbuseIPDB to find information on its ownership and reputation. The ISP is Tencent Cloud Computing (Beijing) Co. Ltd., based in China. This IP was reported 3,481 times, and the Confidence of Abuse is 0%.

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in Cisco Talos IP & Domain Reputation Center. The Sender IP Reputation is Poor.

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in VirusTotal. After reanalyzing the IP address, 3/89 vendors flagged it as malicious.

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in Hybrid Analysis. The IP address was identified as suspicious with a Threat Score of 50/100.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Examine the HTTP Traffic

I examined the requested URL in the alert. It looks like someone attempted to access a password file.

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched the source IP address (106.55.45.162) on the Log Management page, and one entry was returned. I check the raw log data. The HTTP Response Status is 500, and the HTTP Response Size is 0.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Is Traffic Malicious?

Based on the information found after analyzing the source IP address and the raw log data, the traffic appears to be malicious.

## What Is The Attack Type?

The attack type is LFI.

## Check If It Is a Planned Test

On the Email Security page, I searched the hostname, destination IP address, and source IP address to see if there are any emails indicating that this was a planned test. No results were returned, so this does not appear to be a planned test.

<img src="" height="80%" width="80%"/>
</br>
</br>

<img src="" height="80%" width="80%"/>
</br>
</br>

<img src="" height="80%" width="80%"/>
</br>
</br>

## What Is the Direction of Traffic?

The source IP address (106.55.45.162) is from an external network, and the destination IP address (172.16.17.13) is associated with a server on the internal network. This indicates that the direction of traffic is **Internet -> Company Network**.

## Was the Attack Successful?

Based on the HTTP Response Status of 500 and the HTTP Response Size of 0, I determined that the attack was not successful.

## Add Artifacts

106.55.45.162 - Attacker's IP address
172.16.17.13 - Compromised server's IP address

## Do You Need Tier 2 Escalation?

Based on the organizations escalation policy, there is no need to escalate the case since the attack was not successful, and it originated from an external IP address.

## Analyst Note

A LFI attack against WebServer1006 was attempted by 106.55.45.162. After examining the raw log data, I was able to determine the attack was not successful. 

