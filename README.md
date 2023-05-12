# Khai Báo SIU
## Cách login vào SIU
### cắm vật lý
- cắm port vật lý vào cổng console.
- đặt giải IP 192.168.1.0/24 và telnet 192.168.1.1
### login Từ xa
>ssh admin@*ip_address*
// password
## Khai Báo  SIU
- Xóa commit cũ
>resettofactorysetting
- Mở mode khai báo
>startTransaction dvtdl
### đặt tên cho SIU
setmoattribute dvtdl STN=0 stn_name **SIUDLBT3D**
## Khai báo tại Port GE-0
### Mở port 0
createmo dvtdl STN=0,EthernetInterface=GE0
setmoattribute dvtdl STN=0,EthernetInterface=GE port SFP
setmoattribute dvtdl STN=0,EthernetInterface=GE mode auto
setmoattribute dvtdl STN=0,EthernetInterface=GE portNumber 0
setmoattribute dvtdl STN=0,EthernetInterface=GE sendLinkAlarmAllowed true
createmo dvtdl STN=0,VLANGroup=WAN
setmoattribute dvtdl STN=0,VLANGroup=WAN depLinkLayer STN=0,EthernetInterface=GE
### Tạo Brige 1 cho IuB 3G
createmo dvtdl STN=0,Bridge=1
createmo dvtdl STN=0,VLANGroup=WAN,VLAN=**3G_Mux_IuB**
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=3G_Mux_IuB tagValue 310
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=3G_Mux_IuB depBridge STN=0,**Bridge=1**
### Tạo Brige 2 cho OAM 3G
createmo dvtdl STN=0,Bridge=2
createmo dvtdl STN=0,VLANGroup=WAN,VLAN=**3G_OAM**
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=3G_OAM tagValue 360
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=3G_OAM depBridge STN=0,**Bridge=2**
### Tạo brige 3 cho Service 4G
createmo dvtdl STN=0,Bridge=3
createmo dvtdl STN=0,VLANGroup=WAN,VLAN=4G-enodeB
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=4G-enodeB tagValue 150
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=4G-enodeB depBridge STN=0,Bridge=3
### Tạo brige 4 cho OAM 4G
createmo dvtdl STN=0,Bridge=4
createmo dvtdl STN=0,VLANGroup=WAN,VLAN=4G-enodeB-OAM
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=4G-enodeB-OAM tagValue 250
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=4G-enodeB-OAM depBridge STN=0,Bridge=4
### Tạo brige 5 cho FTTH
createmo dvtdl STN=0,Bridge=5
createmo dvtdl STN=0,VLANGroup=WAN,VLAN=AON
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=AON tagValue 3102
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=AON depBridge STN=0,Bridge=5
### Tạo brige 6 cho 2G
createmo dvtdl STN=0,Bridge=6
createmo dvtdl STN=0,VLANGroup=WAN,VLAN=2G-ABIS
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=2G-ABIS tagValue 356
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=2G-ABIS depBridge STN=0,Bridge=6

## Port GE-1 3G-4G
### Mở port 1 và tạo vlan group dịch vụ
createmo dvtdl STN=0,EthernetInterface=GE1
setmoattribute dvtdl STN=0,EthernetInterface=GE1 port SFP
setmoattribute dvtdl STN=0,EthernetInterface=GE1 mode auto
setmoattribute dvtdl STN=0,EthernetInterface=GE1 portNumber 1
setmoattribute dvtdl STN=0,EthernetInterface=GE1 sendLinkAlarmAllowed true
createmo dvtdl STN=0,VLANGroup=DICHVU
setmoattribute dvtdl STN=0,VLANGroup=DICHVU depLinkLayer STN=0,EthernetInterface=GE1
### Khai bÁO IUB 3G và tag bridge 1
createmo dvtdl STN=0,VLANGroup=DICHVU,VLAN=3G_Mux_IuB
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=3G_Mux_IuB tagValue 310
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=3G_Mux_IuB depBridge STN=0,Bridge=1
### Khai bÁO OAM 3G và tag bridge 2
createmo dvtdl STN=0,VLANGroup=DICHVU,VLAN=3G_OAM
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=3G_OAM tagValue 360
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=3G_OAM depBridge STN=0,Bridge=2

### Khai bÁO SERVICE 4G và tag bridge 3
createmo dvtdl STN=0,VLANGroup=DICHVU,VLAN=4G-enodeB
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=4G-enodeB tagValue 150
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=4G-enodeB depBridge STN=0,Bridge=3

### Khai bÁO OAM 4G và tag bridge 4
createmo dvtdl STN=0,VLANGroup=DICHVU,VLAN=4G-enodeB-OAM
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=4G-enodeB-OAM tagValue 250
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=4G-enodeB-OAM depBridge STN=0,Bridge=4
### Khai bÁO 2G và tag bridge 6
createmo dvtdl STN=0,VLANGroup=DICHVU,VLAN=VLAN=2G-ABIS
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=VLAN=2G-ABIS tagValue 356
setmoattribute dvtdl STN=0,VLANGroup=DICHVU,VLAN=VLAN=2G-ABIS depBridge STN=0,Bridge=6
## Port 2 dành cho AON
createmo dvtdl STN=0,EthernetInterface=GE2
setmoattribute dvtdl STN=0,EthernetInterface=GE2 port SFP
setmoattribute dvtdl STN=0,EthernetInterface=GE2 mode auto
setmoattribute dvtdl STN=0,EthernetInterface=GE2 portNumber 2
setmoattribute dvtdl STN=0,EthernetInterface=GE2 sendLinkAlarmAllowed true
createmo dvtdl STN=0,VLANGroup=FTTX


setmoattribute dvtdl STN=0,VLANGroup=FTTX depLinkLayer STN=0,EthernetInterface=GE2
createmo dvtdl STN=0,VLANGroup=FTTX,VLAN=AON
setmoattribute dvtdl STN=0,VLANGroup=FTTX,VLAN=AON tagValue 3102
setmoattribute dvtdl STN=0,VLANGroup=FTTX,VLAN=AON depBridge STN=0, Bridge=5
## Khai telnet cho Siu
createmo dvtdl STN=0,VLANGroup=WAN,VLAN=IPTELNET
setmoattribute dvtdl STN=0,VLANGroup=WAN,VLAN=IPTELNET tagValue 47
createmo dvtdl STN=0,IPInterface=IPTELNET
setmoattribute dvtdl STN=0,IPInterface=IPTELNET primaryIP_Address 192.168.100.2
setmoattribute dvtdl STN=0,IPInterface=IPTELNET primarySubNetMask 255.255.255.252
setmoattribute dvtdl STN=0,IPInterface=IPTELNET depLinkLayer STN=0,VLANGroup=WAN,VLAN=IPTELNET
setmoattribute dvtdl STN=0,IPInterface=IPTELNET defaultGateway 192.168.100.1
setmoattribute dvtdl STN=0,IPInterface=IPTELNET trustDSCP true
## Check khai báo và commit
checkconsistency dvtdl
commit dvtdl forcedcommit
