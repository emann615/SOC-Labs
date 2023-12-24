# EventID 83 - SOC119 - Proxy - Malicious Executable File Detected

## Alert

The Monitoring page shows that this alert was triggered because a malicious executable file was detected. I took ownership of the alert, created a case, and started the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/e6bece4a-70f3-409e-aee1-83b589f764d5" height="80%" width="80%"/>
</br>
</br>

## Collection Data

I found the following information in the alert:
* Source Address: 172.16.17.5
* Destination Address: 51.195.68.163
* User-Agent: Chrome - Windows

## Search Log

On the Log Management page, I filtered for the source address (172.16.17.5), and two entries were returned. One of the entries corresponds to the time of the alert. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/2bf54e49-e34d-45b4-89ae-05e278836dc2" height="80%" width="80%"/>
</br>
</br>

I took a look at the raw log data, but didn't find anything particularly interesting or suspicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/3a28c2a2-5ccf-445a-8da0-f5e7ccebc215" height="40%" width="40%"/>
</br>
</br>

## Analyze URL Address

I went to VirusTotal and analyzed the requested URL. Only 1/90 vendors flagged the URL as malicious. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/c9aeb348-6b2c-43a3-a262-96c2610edf99" height="80%" width="80%"/>
</br>
</br>

Next, I analyzed the destination IP address (51.195.68.163). The results showds that 0/88 vendors flagged the IP address as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/9b16fdf6-29e1-4a1a-b279-b0c3db21b842" height="80%" width="80%"/>
</br>
</br>

I also searched 51.195.68.163 in Hybrid Analysis. No threats were identified.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/41eef816-bb3d-4883-86f4-b97e07f504cf" height="80%" width="80%"/>
</br>
</br>

I used a sandbox environment to view the page the requested URL directs to. The page downloads the winrar-x32-622.exe file, which is an installer for WinRAR. I analyzed the file in VirusTotal, and 0/71 vendors flagged the file as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/75986d84-cd6e-4a92-aa19-583b1777336b" height="80%" width="80%"/>
</br>
</br>

I also analyzed the file in Hybrid Analysis, and the results came back clean.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/1ef635ee-0f74-4aed-879f-b2efd7bf588c" height="80%" width="80%"/>
</br>
</br>

In order to see what happens when the file is executed, I analyzed it with AnyRun. The file was flagged as malicious, but further examination of the processes created when the file is executed showed no signs of anything out of the ordinary. It simply installs WinRAR as you would expect. Despite being flagged as malicious, the file does not appear to actually do anything malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/f727ffaf-ccb9-4c2c-928a-9cd49b2ec6a1" height="80%" width="80%"/>
</br>
</br>

## Add Artifacts

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/811e0a51-8a12-4d0a-b60a-bd96cfbebd2f" height="60%" width="60%"/>
</br>
</br>

## Analyst Note

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/dbba2aa9-93e4-4b4f-9649-ff743b5aeb21" height="60%" width="60%"/>
</br>
</br>

## Results

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/3430813e-46ff-4595-b852-9d81cdb9db45" height="80%" width="80%"/>
</br>
</br>
