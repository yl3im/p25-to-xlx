# p25-to-xlx

###### Run a standalone P25 reflector and connect it to Module A of an XLX multimode reflector

I mostly followed this manual: https://www.lucifernet.com/2020/01/08/build-a-p25-dmr-cross-mode-bridge/

Install DVSwitch and P25 binaries:
```
mkdir -p /opt/dvswitch
wget https://github.com/DVSwitch/MMDVM_Bridge/raw/master/bin/MMDVM_Bridge.`dpkg --print-architecture` -O /opt/dvswitch/MMDVM_Bridge
wget https://github.com/DVSwitch/Analog_Bridge/raw/master/bin/Analog_Bridge.`dpkg --print-architecture` -O /opt/dvswitch/Analog_Bridge
chmod +x /opt/dvswitch/*

git clone https://github.com/nostar/DVReflectors.git
cd DVReflectors/P25Reflector
make && make install

cd
git clone https://github.com/g4klx/P25Clients.git
cd P25Clients
make && make install
```

Replace `1234567` and `N0CALL` with your DMR ID and callsign. Edit the XLX server address and P25 talkgroup number accordingly.

Run the following commands, each in its own "window" or use screen or tmux:

```
P25Reflector P25Reflector.ini
P25Gateway P25Gateway.ini
/opt/dvswitch/Analog_Bridge Analog_Bridge_DMR.ini
/opt/dvswitch/Analog_Bridge Analog_Bridge_P25.ini
/opt/dvswitch/MMDVM_Bridge MMDVM_Bridge.ini
```
