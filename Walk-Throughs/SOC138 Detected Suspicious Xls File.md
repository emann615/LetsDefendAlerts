# EventID 77 - SOC138 - Detected Suspicious Xls File

## Alert

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/87d86c2a-041c-43ef-b94a-3495cda0fa95" height="80%" width="80%"/>
</br>
</br>

## Define Threat Indicator

Unknown or unexpected outgoing internet traffic

I went to the Endpoint security page and searched the source address (172.16.17.56). The IP address is associated with the Sofia machine on the internal network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a6620d5d-3785-4367-a032-0b8e747e4715" height="80%" width="80%"/>
</br>
</br>

I checked the event history on the machine. There are a few events in the process and terminal history, but nothing really stands out as suspicious. There are no events logged in the network and browser history.

Next, I went to the Log Management page and filtered for the source address (172.16.17.56). Three entries were returned, and two of them correspond with the time of the alert. They show connection to an unknown IP address 177.53.143.89, and the raw log data looks suspicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/0e085e07-102f-4f1e-ac8f-687b81c83f65" height="80%" width="80%"/>
</br>
</br>

## Check if the malware is quarantined/cleaned

The alert and raw log data shows that device action was allowed, so the document was not quarantined or cleaned.

## Analyze Malware

The document is malicious.

I went to VirusTotal and searched the MD5 hash (7ccf88c0bbe3b29bf19d877c4596a8d4) for the file. The results showed that 45/62 vendors flagged the file as malicious.

<img src="" height="80%" width="80%"/>
</br>
</br>

I also searched the MD5 hash in Hybrid Analysis. The file was identified as malicious with a Threat Score 100/100.

<img src="" height="80%" width="80%"/>
</br>
</br>

I I analyzed the ORDER SHEET & SPEC.xlsm file with AnyRun to see what happens when the file is opened. AnyRun identified malicious activity. The file connects to IP address 177.53.143.89, which we saw on the Log Management page. The domain for the IP address is multiwaretecnologia.com.br

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched 177.53.143.89 in VirusTotal, but no vendors fl agged it as malicious.

<img src="" height="80%" width="80%"/>
</br>
</br>

To be safe, I also searched the domain multiwaretecnologia.com.br. This time the results showed that 10/90 vendors flagged the domain as malicious.

<img src="" height="80%" width="80%"/>
</br>
</br>

I searched the domain multiwaretecnologia.com.br in Hybrid Analysis. The domain is identified as malicious with a Threat Score of 100/100.

<img src="" height="80%" width="80%"/>
</br>
</br>

## Check If Someone Requested the C2

The C2 address was accessed.

On the Log Management page I filtered for entries with a destination address of 177.53.143.89. Connection to the address was also made on a device with the IP address 172.16.17.24 

On the Endpoint Security page I was able to see that IP address 172.16.17.24 is associated with the Nolan machine on the internal network. The process, network, and terminal history show evidence that the file was executed on this machine.

### Containment

I contained the Nolan and Sofia machines on the Endpoint Security Page.

## Add Artifacts

<img src="" height="80%" width="80%"/>
</br>
</br>

## Analysts Note

<img src="" height="80%" width="80%"/>
</br>
</br>

## Results

<img src="" height="80%" width="80%"/>
</br>
</br>

