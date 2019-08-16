# wifuzz
WiFuzz is an Access Point 802.11 stack fuzzer. It generates "fuzzy" 802.11 network packets to trigger corner-case errors in the 802.11 stack implemented in today's Access Points.

Automatically exported from [code.google.com/p/wifuzz]()

#### Pre requisites

* Wi-Fi driver with monitor mode and injection support;
* WiFuzz requires Scapy v2.4.3. Scapy from branch [#ca341e287e](https://github.com/secdev/scapy/tree/ca341e287e49e410a6348bebb6852e28d68ceab8) is working fine.

#### Example

You can choose what states to fuzz. The following states are available:

```shell
----------------------------------------------------------------------------
|    Name    |        State         |             Description              |
----------------------------------------------------------------------------
|    any     |         none         | Random 802.11 frame fuzzer           |
|   assoc    |    authenticated     | Association request fuzzer           |
|    auth    |        probed        | Authentication request fuzzer        |
|   beacon   |         none         | Beacon request fuzzer                |
|  deassoc   |      associated      | Deassociation request fuzzer         |
|   deauth   |    authenticated     | Deauthentication request fuzzer      |
|    eap     |      associated      | EAP protocol fuzzer                  |
|   eapol    |      associated      | EAPOL (EAP-over-LAN) protocol fuzzer |
|   probe    |         none         | Probe request fuzzer                 |
----------------------------------------------------------------------------
```

You can execute the tool with the selected state/states by running the command:

```bash
sudo python wifuzz.py -s wifi_name -i wlan2mon -o ./output assoc,auth,deassoc,deauth,eapol,probe
```

You should receive the following output:

```python
Sat Aug 17 02:08:27 2019 {MAIN} Target SSID: wifi_name; Interface: wlan2mon; Ping timeout: 60; PCAP directory: ./out; Test mode? False; Fuzzer(s): assoc,auth,deassoc,deauth,eapol,probe;
Sat Aug 17 02:08:27 2019 {WIFI} Waiting for a beacon from SSID=[wifi_name]
Sat Aug 17 02:08:28 2019 {WIFI} Channel 1
Sat Aug 17 02:08:28 2019 {WIFI} Channel 2
Sat Aug 17 02:08:29 2019 {WIFI} Beacon from SSID=[wifi_name] found (MAC=[24:0a:c4:9a:58:28])
Sat Aug 17 02:08:29 2019 {WIFI} Starting fuzz 'assoc,auth,deassoc,deauth,eapol,probe'
Sat Aug 17 02:08:29 2019 {WIFI} Fuzztype: ['assoc', 'auth', 'deassoc', 'deauth', 'eapol', 'probe']
Sat Aug 17 02:08:29 2019 {WIFI} [R00001] Sending packets 1-100
Progress: 100 [100.0%], Fuzztype: deauth 
```

If a crash is received, a pcap capture is saved in the folder pointed by the -o argument (output in this example).