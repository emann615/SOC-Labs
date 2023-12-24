# EventID 120 - SOC170 - Passwd Found in Requested URL - Possible LFI Attack

## Alert

On the Monitoring page, I see that the alert was triggered because "passwd" was found in the requested URL, indicating a possible LFI attack. I took ownership of the alert and created a case, so I can start the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/5a40b96c-2f37-4470-b110-2b6ba32eee79" height="80%" width="80%"/>
</br>
</br>

## Data Collection

I went to the Endpoint Security page, and did a search for the destination IP address and source IP address to see if they belong to the internal network. The destination IP address (172.16.17.13) is associated with WebServer1006 on the internal network. The source IP address (106.55.45.162) did not return any results, indicating it is from an external network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/c672612a-dfc9-4795-98d9-7a68a93cee38" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/8da6228c-f87e-4916-a1f7-aed9776e6085" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in AbuseIPDB to find information on its ownership and reputation. The ISP is Tencent Cloud Computing (Beijing) Co. Ltd., based in China. This IP was reported 3,481 times, and the Confidence of Abuse is 0%.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/134d3b85-0558-4c90-a562-c3a0a261b79a" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in Cisco Talos IP & Domain Reputation Center. The Sender IP Reputation is Poor.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/66d0d253-ed69-40b8-9d78-2b89323da945" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in VirusTotal. After reanalyzing the IP address, 3/89 vendors flagged it as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/159f62ec-8ea5-483a-92f8-22f2fe8182fd" height="80%" width="80%"/>
</br>
</br>

I searched 106.55.45.162 in Hybrid Analysis. The IP address was identified as suspicious with a Threat Score of 100/100.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/ff626624-eedf-4275-8026-1fab47105316" height="80%" width="80%"/>
</br>
</br>

## Examine the HTTP Traffic

I searched the source IP address (106.55.45.162) on the Log Management page, and one entry was returned. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/f4e77f2f-715c-429c-b15a-7948136800b8" height="80%" width="80%"/>
</br>
</br>

I checked the raw log data. Based on the requested URL, it looks like someone attempted to access a password file. The HTTP Response Status is 500, and the HTTP Response Size is 0.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/1cba66f6-eba6-44e1-bf51-734bd50a6d55" height="40%" width="40%"/>
</br>
</br>

## Is Traffic Malicious?

Based on the information found after analyzing the source IP address and the raw log data, the traffic appears to be malicious.

## What Is The Attack Type?

The attack type is LFI, because the attacker included a local password file in the requested URL.

## Check If It Is a Planned Test

On the Email Security page, I searched the hostname, destination IP address, and source IP address to see if there are any emails indicating that this was a planned test. No results were returned, so this does not appear to be a planned test.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/4604a505-baf3-4b2e-9433-2734161ce84c" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/5e15e290-4801-4da5-a1eb-de2aad756ff3" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/de719098-5eb9-43f8-988b-7e47294278ff" height="80%" width="80%"/>
</br>
</br>

## What Is the Direction of Traffic?

The source IP address (106.55.45.162) is from an external network, and the destination IP address (172.16.17.13) is associated with a server on the internal network. This indicates that the direction of traffic is **Internet -> Company Network**.

## Was the Attack Successful?

Based on the HTTP Response Status of 500 and the HTTP Response Size of 0, I determined that the attack was not successful.

## Add Artifacts

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/5827a3d5-4942-40d6-b1e8-d8d81f8378cd" height="80%" width="80%"/>
</br>
</br>

## Do You Need Tier 2 Escalation?

Based on the organizations escalation policy, there is no need to escalate the case since the attack was not successful, and it originated from an external IP address.

## Analyst Note

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/e669d5bd-7976-4f10-b046-d8c22e62abc6" height="80%" width="80%"/>
</br>
</br>

## Results

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/9fb60df0-8438-4b60-ba53-04e7caf7a265" height="80%" width="80%"/>
</br>
</br>

