# 4. INTRO TO THE CLI

### What is a CLI?

- A "Command-line Interface"
- The interface you use to configure Cisco devices

A GUI is a "Graphical User Interface"

### How do you connect to a Cisco Device?

- Console Port : When you first configure a device, you have to connect via the Console Port.

You can use a "Rollover cable" : DB9 serial connector to RJ45 OR a DB9 Serial to USB

[Image removed]

### How do you actually access the CLI?

- You need to use a TERMINAL EMULATOR (Example: PuTTy is a popular choice) and connect via "Serial" (default settings)

### Cisco Default Settings are:

Speed (baud) : 9600 bits/second
Data bits: 8 data bits
Stop bits: 1 stop bit (sent after 8 data bits are sent)
Parity: None
Flow Control: None

---

When you first enter the CLI you will DEFAULT be in what is called 'User EXEC' mode.

USER EXEC MODE:

(Hostname) >		// Prompt looks like THIS //

- User EXEC mode is very limited.
- User can look at some things but can't make ANY changes to the configuration.
- AKA 'User Mode'

Using the 'enable' command, in User EXEC mode, switches you to 'Privileged EXEC' mode.

---

PRIVILEGED EXEC MODE:

- Provides complete access to view the device's configuration, restart the device, etc.
- Cannot change the configuration, but can change the time on the device, save the configuration file, etc.

(Hostname)#		// Prompt looks like THIS //

---

USE a Question Mark (?) to view the available commands in ANY mode. Combining ? with a letter or partial command will list all the commands with those letters.

[Image removed]


USE the TAB key to complete partially entered commands IF the command exists.

---

### GLOBAL CONFIGURATION MODE:

To enter Global Configuration Mode, enter the command, within Privileged EXEC mode

 'configure terminal' (or 'conf t')

Router# configure terminal
Router(config) #		

Router(config) # run 

Router(config) # no 

Type 'exit' to drop back into 'Privileged EXEC' mode.

---

### To Enable Password for User EXEC mode:

Router(config)# enable password (password)

- Passwords ARE case-sensitive.

// This command encrypts plain-text passwords, visible in the config files, using simple encryption.

Router(config)# service password-encryption

If you enable 'service password-encryption'

- Current passwords WILL be encrypted.
- Future passwords WILL be encrypted.
- The 'enable secret' WILL NOT be effected.

If you disable 'service password-encryption'

- Current passwords WILL NOT be decrypted.
- Future passwords WILL NOT be encrypted.
- The 'enable secret' WILL NOT be effected.

// This command enables passwords for the Privileged EXEC mode.

Router(config)# enable secret (password)

// enable secret will ALWAYS be encrypted (at level 5)

---

There are TWO separate configuration files kept on the device at once.

Running-config :

- The current, ACTIVE configuration file on the device. As you enter commands in the CLI, you edit the active configuration.

Startup-config :

- The configuration file that will be loaded upon RESTART of the device.

To see the configuration files, inside 'Privileged EXEC' mode:

Router# show running-config // for running config //

OR

Router# show startup-config // for startup config //

---

To SAVE the Running configuration file, you can:

Router# write
Building configuration...
[OK]

Router# write memory
Building configuration...
[OK]

Router# copy running-config startup-config

Destination filename [startup-config]?

Building configuration...
[OK]

---

To encrypt passwords:

Router# conf t

Router(config)# service password-encryption

This makes all current passwords *encrypted*

Future passwords will ALSO be *encrypted*

“Enable secret” will not be effected (it’s ALWAYS encrypted)

[Image removed]


Now you will see that the password is no longer in plaintext.

“7” refers to the type of encryption used to encrypt the password. In this case, “7” uses Cisco’s proprietary encryption.

“7” is fairly easy to crack since the encryption is weak.

For BETTER / STRONGER encryption, use “enable secret”

[Image removed]


“5” refers to MD5 encryption.

Can still be cracked but it’s much much stronger.

Once you use “enable secret” command, this will override “enable password”

---

To CANCEL or delete a command you entered, use the “no” keyword

[Image removed]


In this instance, disabling “service password-encryption”:

- current passwords will NOT be decrypted (unchanged)
- future passwords will NOT be encrypted
- the “enable secret” will not be effected

---

[Image removed]

[Image removed]

[Image removed]

[Image removed]

[Image removed]
