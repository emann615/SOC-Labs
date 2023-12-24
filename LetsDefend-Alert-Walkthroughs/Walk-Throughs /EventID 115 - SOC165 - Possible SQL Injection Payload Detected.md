# EventID 115 - SOC165 - Possible SQL Injection Payload Detected

## Alert

Looking at the Monitoring page, I see the alert was triggered because a possible SQL injection payload was detected. I took ownership of the alert and created a case, so I can start the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/0b5cb554-2194-4a33-819e-7b6b59276187" height="80%" width="80%"/>
</br>
</br>

## Collect Data

I searched the Endpoint Security page to see if either of the IP addresses are owned by the internal network. The destination IP address (172.16.17.18) is associated with WebServer1001. The source IP address (167.99.169.17) did not return any results, indicating that it is outside the network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2b4f5c07-4713-4daa-9c75-4bb81db51787" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/f56978f0-b32a-4959-812f-504bb044e9c4" height="80%" width="80%"/>
</br>
</br>

I searched 167.99.169.17 in AbuseIPDB to identify the owner and IP address reputation. It shows that the ISP is DigitalOcean LLC. The IP addresss has been reported 15,152 times, but the Confidence of Abuse is 0%.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/95612cf6-6357-4a07-a438-161f0d99cb01" height="80%" width="80%"/>
</br>
</br>

Next, I searched 167.99.169.17 in Cisco Talos IP & Domain Reputation Center. It identifies the IP reputation as Neutral.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/31644863-71df-423a-b154-92c80fb90cf4" height="80%" width="80%"/>
</br>
</br>

Since Abuse IPDB and Cisco Talos were inconclusive, I decided to check VirusTotal. It shows that 9 vendors identified the IP address as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2b8dfcc3-270f-493e-9a0a-57693846a82b" height="80%" width="80%"/>
</br>
</br>

I still wanted a second source to confirm that the IP is malicious, so I also checked Hybrid Analysis. The results show that the IP address is malicious with a Threat Score of 100/100.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/10bb51ca-d1f8-47e4-ac77-0239b91c3056" height="80%" width="80%"/>
</br>
</br>

## Examine HTTP Traffic

I used a URL decoder to decode and examine the URL in the HTTP Request. The decoded URL indicates **SQL injection** is the attack method.
* Decoded URL: https://172.16.17.18/search/?q=" OR 1 = 1 -- -

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2d4d2afc-b29b-4fc8-8ceb-4b90002a6403" height="80%" width="80%"/>
</br>
</br>

## Is Traffic Malicious?

Based on the information found after analyizing the source IP address and the requested URL, the traffic appears to be malicious.

## What Is The Attack Type?

After examining the logs of the HTTP traffic, I found information for an SQL query included in the requested URL. This indicates the attack type is SQL Injection.

## Check If It Is a Planned Test

I searched the source IP address, destination Ip address, and hostname on the Email Security page. No results were populated, so their is no indication that this was a planned test. There is also no indication that an attack simulation product was used.

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

Based on the investigation so far, I know the source IP address is from the internet, and the destination IP address is from the internal network. Therefore, the direction of traffic is **Internet -> Company Network**.

## Was the Attack Successful?

I checked the Log Managment page to see if there was any indication that the attack was successful. I searched the source IP address (167.99.169.17) and found multiple log entries.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/bc3e0019-5e1c-45c8-ae19-1c66b2200a17" height="80%" width="80%"/>
</br>
</br>

Based on the raw logs, it looks like there were multiple HTTP requests sent attempting SQL injection. All of the request resulted in a status code of 500 and a response size of 948.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a0f08f6a-a48d-4f8c-b689-c5b72d52c074" height="40%" width="40%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/bfc86b33-29ae-40e3-9626-0e99929647ea" height="40%" width="40%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/4e2a0860-5712-4604-8666-18231ba4cba8" height="40%" width="40%"/>
</br>
</br>

I decoded the URLs found in each HTTP requests. The decoded URLs show that multiple SQLi medthods were attempted.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/8d3db841-da91-4e2e-bb88-62fce1798d30" height="80%" width="80%"/>
</br>
</br>

Since mulitple there were multiple SQLi attempts using different methods that resulted in a consistent response size of 948, this indicates that that the attack was not successful.

I laso checked the command history for WebServer1001 on the Endpoint Security page. The command history shows no indication that the attack was successful.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/38f8e75d-bc99-4ac7-b278-911222783ceb" height="80%" width="80%"/>
</br>
</br>

## Add Artifacts

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/294de25c-608b-4ba6-a606-a17f15b5f14c" height="80%" width="80%"/>
</br>
</br>

## Do You Need Tier 2 Escalation?

Based on the organization's escalation procedure, there is no need for escalation since the attack was not successful, and it did not originate from the internal network.

## Analyst Note

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/703ab136-8aed-45dd-8421-fd662f550cf0" height="80%" width="80%"/>
</br>
</br>

## Result

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/47cc0263-9ca1-40e6-afd8-26472ace6b78" height="80%" width="80%"/>
</br>
</br>
