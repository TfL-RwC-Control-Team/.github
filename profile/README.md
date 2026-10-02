# Transport for London Railway Challenge Control Team
This Github organisation was created to house the code repositories for the 2025 control rebuild of the TfL RwC Locomotive.

CAD for control devices can also be found in the repositories here.
## Control Topology
```mermaid
%%{init: {
  'layout': 'elk',
  'flowchart': {
    'curve' : 'stepBefore',
    'nodeSpacing' : 50,
    'rankSpacing' : 80,
    'useMaxWidth' : true,
    'htmlLabels': true,
    'padding' : 10,
    'inheritDir': false
}}}%%

flowchart LR
CPD[\CANBus and Power Distributor\] e1@== CANBus + Pwr ==> MMC[Master Motor Controller]
CPD e2@<== CANBus + Pwr ==> SMC[Slave Motor Controller]
CPD e3@<== CANBus + Pwr ==> HandCont[Remote Controller]
CPD e4@<== CANBus + Pwr ==> CabCont[Ride-On Controller]
CPD e5@<== CANBus + Pwr ==> LAS[Location Annoucement Controller]
CPD e6@<== CANBus + Pwr ==> RDM[Remote Data Monitoring Controller]
CPD e7@<== CANBus + Pwr ==> RTC[Round Train Circuit]
CPD e8@<== CANBus + Pwr ==> CCS[Compressor Control System]

classDef animate stroke-dasharray: 9,5,stroke-dashoffset: 900,animation: dash 25s linear infinite;
class e1,e2,e3,e4,e5,e6,e7,e8 animate

SMS[Speed Encoder] -- DIn --> MMC
MMC -- DOut --> BrkR[Rear Brake Relay]
SMC -- DOut--> BrkF[Front Brake Relay]

subgraph LASGrp [Location Annoucement System]
UHF[UHF RFID Reciever] <-- SPI --> LAS
LAS -- 3.5mm Jack --> Amp[Audio Amp]
Amp --> Spkrs[Rear Speakers]
end

subgraph RDMGrp [Remote Data Monitoring System]
Modem -- Ethernet --> RDM
Ant1([Primary Antenna]) -- GSM --> Modem
Ant2([Secondary Antenna]) -- GSM --> Modem
Modem -- Ethernet --> WiFi[WiFi Transciever]
WiFi --> Ant1
end

subgraph Aux [Auxillary Systems]
RDM -- Relays --> Horn & Lights[Front/Rear Lights]
end

subgraph Signature ["2026 Alwyn Whalley"]
direction LR
style Signature fill:none,stroke:#ccc,stroke-width:1px,stroke-dasharray: 5 5,font-size:10px
end
UHF ~~~ Signature

click MMC "https://github.com/TfL-RwC-Control-Team/RoboteQ-HDC2460S" "RoboteQ-HDC2460S Repo"
click RDM "https://github.com/TfL-RwC-Control-Team/RDM" "RDM Repo"
click RTC "https://github.com/TfL-RwC-Control-Team/RTC" "RTC Repo"
click LAS "https://github.com/TfL-RwC-Control-Team/LAS" "LAS Repo"
click CCS "https://github.com/TfL-RwC-Control-Team/CCS" "CCS Repo"
click HandCont "https://github.com/TfL-RwC-Control-Team/TfLRwCDIS" "TfLRwCDIS Repo"
```
