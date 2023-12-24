# EventID 87 - SOC101 - Phishing Mail Detected

## Alert

The Monitoring page shows that this alert was triggered because phishing mail was detected. I took ownership of the alert, created a case, and started the playbook

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/0dd6a0ee-b556-4c8b-b0a0-9102ef6d66da" height="80%" width="80%"/>
</br>
</br>

## Parse Email

* When was it sent? Apr, 04, 2021, 11:00 PM
* What is the email's SMTP address? 146.56.195.192
* What is the sender address? lethuyan852@gmail.com
* What is the recipient address? mark@letsdefend.io
* Is the mail content suspicious? Yes
* Are there any attachment? No

## Are there attachments or URLs in the email?

I went to the Email Security page and found the email by searching the email subject included in the alert.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a9edab81-9996-4c2e-84a1-066e6dff7763" height="80%" width="80%"/>
</br>
</br>

There are no attachements, but there is a URL (http://nuangaybantiep.xyz) in the body of the email.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/cdfd6126-cb27-4e74-a95a-17a070590caf" height="80%" width="80%"/>
</br>
</br>

## Analyze Url/Attachment

First, I searched the SMTP address 146.56.195.192 in Cisco Talos. It is located in China and appears to be a spoofed Gmail.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/ec51b7a6-8b15-4c38-88aa-3baf961d2aeb" height="80%" width="80%"/>
</br>
</br>

I analyzed the URL in VirusTotal. Only 1/89 vendors flagged the URL as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a953cf5a-73ea-4291-9950-03bb489ce00b" height="80%" width="80%"/>
</br>
</br>

I also took a look at the Joe Snadbox analysis report for the URL. The report identifies the URL as suspicious. The URL is currently not reachable, but appears to have previously been used to spread a trojan.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/acb20109-78e2-4feb-8655-b5905f176cc8" height="80%" width="80%"/>
</br>
</br>

## Check If Mail Delivered to User?

The alert shows that Device Action was Allowed, indicating that the email was delivered to the user.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/56824935-1673-4ad4-a947-bb8a2599a70d" height="50%" width="50%"/>
</br>
</br>

## Check If Someone Opened the Malicios File/URL?

I went to the Log Management page and searched for the URL (http://nuangaybantiep.xyz). One log entry was returned with a source IP address of 172.16.17.88 and a destination IP address of 192.64.119.190. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/45fadcb1-c2c5-425a-94b2-662dd6bfcf25" height="80%" width="80%"/>
</br>
</br>

The raw data for the log shows the same URL I found in the email.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/23f02e2c-74b1-423b-b985-7a0fc0fb808b" height="40%" width="40%"/>
</br>
</br>

On the Endpoint Security page, I searched the source IP address from the log entry. It belongs to the MarkPRD device.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/ffc19f04-a193-452f-9c1e-77ca5966d62f" height="80%" width="80%"/>
</br>
</br>

Base on this information, the URL was accessed from the MarkPRD device.

## Containment

I contained the device to prevent the spread of the attack.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/91813e48-2920-443b-9507-52a699f638fa" height="30%" width="30%"/>
</br>
</br>

## Add Artifacts

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/e4c4571b-32a0-4386-ab53-1d93b81b488c" height="60%" width="60%"/>
</br>
</br>

## Analyst Note

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/59a27172-cfd0-441c-9c1f-ea51c0138f3e" height="60%" width="60%"/>
</br>
</br>

## Results

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/408d43bd-09e4-4ddf-8531-e2c873d5ce32" height="80%" width="80%"/>
</br>
</br>
