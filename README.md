## Required Tools

    python:                 Wifite is compatible with both python2 and python3.
    iwconfig:               For identifying wireless devices already in Monitor Mode.
    ifconfig:               For starting/stopping wireless devices.
    Aircrack-ng suite, includes:
        airmon-ng:          For enumerating and enabling Monitor Mode on wireless devices.
        aircrack-ng:        For cracking WEP .cap files and WPA handshake captures.
        aireplay-ng:        For deauthing access points, replaying capture files, various WEP attacks.
        airodump-ng:        For target scanning & capture file generation.
        packetforge-ng:     For forging capture files.

Optional,  but Recommended:

     tshark:                 For detecting WPS networks and inspecting handshake capture files.
     reaver:                 For WPS Pixie-Dust & brute-force attacks.
   Note: Reaver's wash tool can be used to detect WPS networks if tshark is not found.
   
     bully:                  For WPS Pixie-Dust & brute-force attacks.
   Alternative to Reaver. Specify --bully to use Bully instead of Reaver.
   Bully is also used to fetch PSK if reaver cannot after cracking WPS PIN.
   
     coWPAtty:               For detecting handshake captures.
     pyrit:                  For detecting handshake captures.
     hashcat:                For cracking PMKID hashes.
     hcxdumptool:            For capturing PMKID hashes.
     hcxpcaptool:            For converting PMKID packet captures into hashcat's forma

## Run :
    git clone https://github.com/derv82/wifite2.git
    cd wifite2
    sudo ./Wifite.py
## Install Wifite:
    sudo python setup.py install
Note: Uninstalling is not as easy. The only way to uninstall is to record the files installed by the above command and remove those files:

    sudo python setup.py install --record files.txt \
      && cat files.txt | xargs sudo rm \
      && rm -f files.txt

## Basic usage:

      optional arguments:
        -h, --help                                 show this help message and exit

      SETTINGS:
        -v, --verbose                              Shows more options (-h -v). Prints commands and outputs. (default:
                                                   quiet)
        -i [interface]                             Wireless interface to use, e.g. wlan0mon (default: ask)
        -c [channel]                               Wireless channel to scan e.g. 1,3-6 (default: all 2Ghz channels)
        -inf, --infinite                           Enable infinite attack mode. Modify scanning time with -p (default:
                                                   off)
        -mac, --random-mac                         Randomize wireless card MAC address (default: off)
        -p [scan_time]                             Pillage: Attack all targets after scan_time (seconds)
        --kill                                     Kill processes that conflict with Airmon/Airodump (default: off)
        -pow [min_power], --power [min_power]      Attacks any targets with at least min_power signal strength
        --skip-crack                               Skip cracking captured handshakes/pmkid (default: off)
        -first [attack_max], --first [attack_max]  Attacks the first attack_max targets
        -ic, --ignore-cracked                      Hides previously-cracked targets. (default: off)
        --clients-only                             Only show targets that have associated clients (default: off)
        --nodeauths                                Passive mode: Never deauthenticates clients (default: deauth targets)
        --daemon                                   Puts device back in managed mode after quitting (default: off)

      WEP:
        --wep                                      Show only WEP-encrypted networks
        --require-fakeauth                         Fails attacks if fake-auth fails (default: off)
        --keep-ivs                                 Retain .IVS files and reuse when cracking (default: off)

      WPA:
        --wpa                                      Show only WPA-encrypted networks (includes WPS)
        --new-hs                                   Captures new handshakes, ignores existing handshakes in hs (default:
                                                   off)
        --dict [file]                              File containing passwords for cracking (default: /usr/share/dict/wordlist-
                                                   probable.txt)

      WPS:                                                                                                                                                                                                                                       
        --wps                                      Show only WPS-enabled networks                                                                                                                                                                
        --wps-only                                 Only use WPS PIN & Pixie-Dust attacks (default:                                                                                                                                               
                                                   off)                                                                                                                                                                                          
        --bully                                    Use bully program for WPS PIN & Pixie-Dust attacks (default:                                                                                                                                  
                                                   reaver)                                                                                                                                                                                       
        --reaver                                   Use reaver program for WPS PIN & Pixie-Dust attacks (default:                                                                                                                                 
                                                   reaver)                                                                                                                                                                                       
        --ignore-locks                             Do not stop WPS PIN attack if AP becomes locked (default:                                                                                                                                     
                                                   stop)                                                                                                                                                                                         

      PMKID:                                                                                                                                                                                                                                     
        --pmkid                                    Only use PMKID capture, avoids other WPS & WPA attacks (default:                                                                                                                              
                                                   off)                                                                                                                                                                                          
        --no-pmkid                                 Don't use PMKID capture (default: off)                                                                                                                                                        
        --pmkid-timeout [sec]                      Time to wait for PMKID capture (default: 120 seconds)                                                                                                                                         

      COMMANDS:
        --cracked                                  Print previously-cracked access points
        --check [file]                             Check a .cap file (or all hs/*.cap files) for WPA handshakes
        --crack                                    Show commands to crack a captured handshake
