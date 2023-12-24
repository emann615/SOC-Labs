# EventID 119 - SOC169 - Possible IDOR Attack Detected

## Alert

On the Monitoring page, I see that the alert was triggered because consecutive requests were made to the same page. I took ownership of the alert and created a case, so I can start the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/ef6b5f42-6010-4415-8e3e-400c6e96c4d4" height="80%" width="80%"/>
</br>
</br>

## Collect Data

I went to the Endpoint Security page, and did a search for the destination IP address and source IP address to see if they belong to the internal network. The destination IP address (172.16.17.15) is associated with WebServer1005 on the internal network. The source IP address (134.209.118.137) returns no result, indicating it is from an external network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/bde569e9-2025-435f-bdae-7b4e655317a5" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/ebb021ef-b026-4f97-80b8-748e2872167e" height="80%" width="80%"/>
</br>
</br>

I searched 134.209.118.137 AbuseIPDB to find information on its ownership and reputation. The ISP is DigitalOcean LLC. The IP address has been reported 1,539 times, and the Confidence of Abuse is 1%.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/18b3d834-efc1-4211-9875-bea1e87bf52e" height="80%" width="80%"/>
</br>
</br>

I searched 134.209.118.137 in Cisco Talos IP & Domain Reputation Center. It shows the Sender IP Reputation is Poor.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/48d72418-ed43-421e-9543-0e60d8330d4b" height="80%" width="80%"/>
</br>
</br>

I searched 134.209.118.137 in VirusTotal. After reanalyzing the IP address, 1/89 vendors flagged it as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a38407de-c53a-40ad-9c4c-98d825b5a7d1" height="80%" width="80%"/>
</br>
</br>

I searched 134.209.118.137 in Hybrid Analysis. The IP address was identified as malicious with a Threat Score of 50/100.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/fb1269dc-11ff-4343-81b8-55f2e7b737fb" height="80%" width="80%"/>
</br>
</br>

## Examine the HTTP Traffic

I searched the source IP address (134.209.118.137) on the Log Management page, and multiple log entries were returned. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/cb9d418a-20f4-436d-9f5c-ba06cbbe7335" height="80%" width="80%"/>
</br>
</br>

I examined the raw log for each entry. The Post Parameters header shows that multiple attempts were made to access user information by changing the user_id value for each request. The HTTP Response Status for all the requests is 200. The HTTP Response Size is different for each request.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/adee7988-cee0-46af-9cc8-2f89a5d94229" height="40%" width="40%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/9b87932c-afb6-431c-8576-ac2988c71cbf" height="40%" width="40%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/35172118-87d9-4715-9bab-a697f070c641" height="40%" width="40%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/4d3a07ca-f82a-44c0-a83c-71a581a577d3" height="40%" width="40%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/ed84eed6-6564-452c-91c6-365bce97aabb" height="40%" width="40%"/>
</br>
</br>

## Is Traffic Malicious?

Based on the information found after analyzing the source IP address and the raw log data, the traffic appears to be malicious.

## What Is The Attack Type?

The attack type is IDOR, becuase the attcker made requests to access information that does not belong to them by changing the user_id value.

## Check If It Is a Planned Test

On the Email Security page, I searched the hostname, destination IP address, and source IP address to see if there are any emails indicating that this was a planned test. No results were returned, so this does not appear to be a planned test.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/6f873494-6160-4f37-8b12-618dbd8c4182" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/feaa08c3-bd07-4fb1-9206-71c1b190ce99" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/b41a9b03-d7f6-4930-905c-cca0d5f6ac9f" height="80%" width="80%"/>
</br>
</br>

## What Is the Direction of Traffic?

The source IP address (134.209.118.137) is from an external network, and the destination IP address (172.16.17.15) is associated with a server on the internal network. This indicates that the direction of traffic is **Internet -> Company Network**.

## Was the Attack Successful?

Based on the HTTP Response Status and HTTP Response Size I saw in the raw log data, the attack was successful. The response status was 200, and the response size was different for each request.

## Containment

Since the server was compromised, I contained the host to prevent the spread of the attack and reduce the impact.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/36eb7519-580b-4c7b-9c64-c8fd8c48aff0" height="80%" width="80%"/>
</br>
</br>

## Add Artifacts

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/c2dab97b-97c4-4d99-8301-96d6046296b8" height="80%" width="80%"/>
</br>
</br>

## Do You Need Tier 2 Escalation?

Based on the organizations escalation policy, escalation of the case is required because the attack was successful.

## Analyst Note

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/0b788726-22d0-41bd-ae44-5091fe5db3f3" height="80%" width="80%"/>
</br>
</br>

## Results

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/ce1c3d32-ddb8-4113-8f37-cc7e876cfe5e" height="80%" width="80%"/>
</br>
</br>
