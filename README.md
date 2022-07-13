# Check_MK-SIGNAL_Notification

[CheckMK](https://checkmk.com/) plugin for sending notifications via [Signal Messenger](https://signal.org)

Prerequisites

    1) Java Runtime Environment installed >= 17
   
        Ubuntu/Debian: 
            sudo update-alternatives --config java
            sudo apt-get install openjdk-17-jre
        Ubuntu 22.04: sudo apt install openjdk-18-jre
        
        additional help: https://tecadmin.net/install-latest-java-on-debian/

     2) Get signal-cli >= v0.10.8 from https://github.com/AsamK/signal-cli

## 1. Installation: signal-cli

<i>YOUR_CHECKMK_SITE_NAME -> enter your CheckMK site name here</i>

```/bin/sh
omd su YOUR_CHECKMK_SITE_NAME
wget https://github.com/AsamK/signal-cli/releases/download/v0.10.8/signal-cli-0.10.8-Linux.tar.gz
tar xf signal-cli-0.10.8-Linux.tar.gz -C ~/local
ln -sf ~/local/signal-cli-0.10.8/bin/signal-cli ~/local/bin/
```

## 2. Installation: CheckMK plugin



```/bin/sh
wget https://github.com/WojRep/Check_MK-SIGNAL_Notification/releases/download/2.0.0/signal-messenger-notification-2.0.0.mkp
mkp install signal-messenger.mkp
```

Set Your Signal Messenger Account (eg. from phone number)
`nano ~/local/share/check_mk/notifications/signal-messenger`

In CheckMK, you set the "Pager address: field in the user settings, and there you enter the phone number with the country code (e.g. +48)



## 3. Manual configuration of Signal Messenger account

Important: The ACCOUNT is your phone number in international format and must include the country calling code. Hence it should start with a "+" sign. (See Wikipedia for a list of all country codes.)

    Register a number (with SMS verification)

      signal-cli -a ACCOUNT register

    You can register Signal using a land line number. In this case you can skip SMS verification process and jump directly to the voice call verification by adding the --voice switch at the end of above register command.

    Registering may require solving a CAPTCHA challenge: Registration with captcha

    Verify the number using the code received via SMS or voice, optionally add --pin PIN_CODE if you've added a pin code to your account

      signal-cli -a ACCOUNT verify CODE
