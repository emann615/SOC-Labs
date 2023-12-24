# EventID 77 - SOC138 - Detected Suspicious Xls File

## Alert

The Monitoring page shows that this alert was triggered because a suspicious XLS file was detected. I took ownership of the alert, created a case, and started the playbook.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/87d86c2a-041c-43ef-b94a-3495cda0fa95" height="80%" width="80%"/>
</br>
</br>

## Define Threat Indicator

I went to the Endpoint security page and searched the source address 172.16.17.56. The IP address is associated with the Sofia machine on the internal network.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a6620d5d-3785-4367-a032-0b8e747e4715" height="80%" width="80%"/>
</br>
</br>

I checked the event history on the machine. There are a few events in the process and terminal history, but nothing really stands out as suspicious. There are no events logged in the network and browser history.

Next, I went to the Log Management page and filtered for the source address 172.16.17.56. Three entries were returned, and two of them correspond with the time of the alert. They show connection to an unknown IP address 177.53.143.89, and the raw log data looks suspicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/0e085e07-102f-4f1e-ac8f-687b81c83f65" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/03cae954-c1bd-45d9-8148-fe51ac63be2f" height="40%" width="40%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/b527e665-4717-4018-a69d-9367b5dee534" height="40%" width="40%"/>
</br>
</br>

## Check if the malware is quarantined/cleaned

The alert shows that device action was allowed, so the document was not quarantined or cleaned.

## Analyze Malware

I went to VirusTotal and searched the MD5 hash (7ccf88c0bbe3b29bf19d877c4596a8d4) for the file. The results show that 45/62 vendors flagged the file as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/1adab952-ce30-4f8e-a917-12e11afd4d71" height="80%" width="80%"/>
</br>
</br>

I also searched the MD5 hash in Hybrid Analysis. The file was identified as malicious with a Threat Score 100/100.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/3f0bfd16-6025-43a4-b754-d7fd1e7a0de6" height="80%" width="80%"/>
</br>
</br>

I I analyzed the ORDER SHEET & SPEC.xlsm file with AnyRun to see what happens when the file is opened. AnyRun identified malicious activity. The file connects to IP address 177.53.143.89, which we saw on the Log Management page. The domain for the IP address is multiwaretecnologia.com.br

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/56380959-84f4-44c3-a8a5-2462d6c04050" height="80%" width="80%"/>
</br>
</br>

I analyzed the IP address 177.53.143.89 in VirusTotal, but no vendors flagged it as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/c2b40733-ce73-4364-bbf4-3c5dbfefabe4" height="80%" width="80%"/>
</br>
</br>

To be safe, I also searched the domain multiwaretecnologia.com.br. This time the results showed that 10/90 vendors flagged the domain as malicious.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/b8179a5f-9f91-4e33-b6cc-3e6728d6c198" height="80%" width="80%"/>
</br>
</br>

I searched the domain multiwaretecnologia.com.br in Hybrid Analysis. The domain is identified as malicious with a Threat Score of 100/100.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/4076df06-61d2-440f-b54a-1730541be911" height="80%" width="80%"/>
</br>
</br>

## Check If Someone Requested the C2

I alreadyknew that the C2 address was accessed on the Sofia machine, but I wanted to see if any other machines on the internal network accessed the address. I went back to the Log Management page and filtered for entries with the destination IP address 177.53.143.89. Connection to the address was also made on a machine with the IP address 172.16.17.24 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/f9ccf315-f19f-4c19-bc16-14bd0aa44d22" height="80%" width="80%"/>
</br>
</br>

On the Endpoint Security page I was able to see that IP address 172.16.17.24 is associated with the Nolan machine on the internal network. 

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/10f1644e-b0f2-4de2-a30a-f5c3f79b33b9" height="80%" width="80%"/>
</br>
</br>

The process, network, and terminal history show evidence that the file was executed on this machine.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/49a6357a-8557-46b8-aa1b-95a592c82069" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/108edaa3-ab4f-4f43-8c40-1a6a838aeca6" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/c256c26b-494a-4e6a-8fc2-1d2b724b01af" height="80%" width="80%"/>
</br>
</br>

## Containment

I contained the Nolan and Sofia machines on the Endpoint Security page to prevent further spread of the attack.

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/acadeeeb-60f9-4763-812c-6960b032e55b" height="80%" width="80%"/>
</br>
</br>

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/baf7be5f-b1be-4eda-a9db-5cb656839444" height="80%" width="80%"/>
</br>
</br>

## Add Artifacts

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/a6a7600f-8b97-419a-b3a3-0f49703fd712" height="60%" width="60%"/>
</br>
</br>

## Analysts Note

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/1bac4390-3b41-47ab-ba49-b5513c090a52" height="60%" width="60%"/>
</br>
</br>

## Results

<img src="https://github.com/emann615/LetsDefendAlerts/assets/117882385/99d5bc10-a0e3-4153-a370-861467570a29" height="80%" width="80%"/>
</br>
</br>

