# Packet Tracer - Configure Initial Switch Settings

### Laporan Praktikum Jaringan Komputer

#### Objectives

- Part 1: Verify the Default Switch Configuration
- Part 2: Configure a Basic Switch Configuration
- Part 3: Configure a MOTD Banner
- Part 4: Save Configuration Files to NVRAM
- Part 5: Configure S2

### Background / Scenario

In this activity, you will perform basic switch configuration tasks. You will secure access to the command-line interface (CLI) and console ports using encrypted and plain text passwords. You will also learn how to configure messages for users logging into the switch. These message banners are also used to warn unauthorized users that access is prohibited.

Note: In Packet Tracer, the Catalyst 2960 switch uses IOS version 12.2 by default. If required, the IOS version can be updated from a file server in the Packet Tracer topology. The switch can then be configured to boot to IOS version 15.0, if that version is required.

![App Screenshot](/Images/Switch%201/1.png)

### Background / Scenario

#### Part 1 : Verify the Default Switch Configuration

- Step 1 : Enter privileged EXEC mode.

#### a. Click S1 and then the CLI tab. Press Enter.

#### b. Enter privileged EXEC mode by entering the enable command:

```bash
Switch> enable
Switch#
```

![App Screenshot](/Images/Switch%201/2.png)

- Step 2: Examine the current switch configuration.
  Enter the show running-config command.

```bash
Switch# show running-config
```

![App Screenshot](/Images/Switch%201/3.png)

#### Part 2: Create a Basic Switch Configuration

- Step 1: Assign a name to a switch.
  To configure parameters on a switch, you may be required to move between various configuration modes. Notice how the prompt changes as you navigate through the switch.

```bash
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# exit
S1#
```

![App Screenshot](/Images/Switch%201/14.png)

- Step 2: Secure access to the console line.
  To secure access to the console line, access config-line mode and set the console password to letmein.

```bash
S1# configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
S1(config)# line console 0
S1(config-line)# password letmein
S1(config-line)# login
S1(config-line)# exit
S1(config)# exit
%SYS-5-CONFIG_I: Configured from console by console
S1#
```

![App Screenshot](/Images/Switch%201/16.png)

- Step 3: Verify that console access is secured.
  Exit privileged mode to verify that the console port password is in effect.

```bash
S1# exit
Switch con0 is now available
Press RETURN to get started.
User Access Verification
Password:
S1>
```

![App Screenshot](/Images/Switch%201/5.png)

- Step 4: Secure privileged mode access.
  Set the enable password to c1$c0. This password protects access to privileged mode.

```bash
S1> enable
S1# configure terminal
S1(config)# enable password c1$c0
S1(config)# exit
%SYS-5-CONFIG_I: Configured from console by console
S1#
```

![App Screenshot](/Images/Switch%201/6.png)

- Step 5: Verify that privileged mode access is secure.

a. Masukkan perintah `exit` sekali lagi untuk keluar dari switch.

b. Tekan tombol `<Enter>` dan Anda akan diminta untuk memasukkan kata sandi:

```bash
User Access Verification

Password:
```

c. Kata sandi pertama adalah kata sandi konsol yang Anda konfigurasi untuk line con 0. Masukkan kata sandi ini untuk kembali ke mode user EXEC.

d. Masukkan perintah untuk mengakses mode privileged.

e. Masukkan kata sandi kedua yang Anda konfigurasi untuk melindungi mode privileged EXEC.

f. Verifikasi konfigurasi Anda dengan memeriksa isi file running-configuration:

```bash
S1# show running-config
```

![App Screenshot](/Images/Switch%201/7.png)

Notice that the console and enable passwords are both in plain text. This could pose a security risk if someone is looking over your shoulder or obtains access to config files stored in a backup location.

- Step 6: Configure an encrypted password to secure access to privileged mode.

The enable password should be replaced with the newer encrypted secret password using the enable secret command. Set the enable secret password to itsasecret.

```bash
S1# config t
S1(config)# enable secret itsasecret
S1(config)# exit
S1#
```

![App Screenshot](/Images/Switch%201/8.png)
Note: The enable secret password overrides the enable password. If both are configured on the switch, you must enter the enable secret password to enter privileged EXEC mode.

- Step 7: Verify that the enable secret password is added to the configuration file.

Enter the show running-config command again to verify the new enable secret password is configured.

`Note: You can abbreviate show running-config as`

```bash
S1# show run
```

![App Screenshot](/Images/Switch%201/9.png)

- Step 8: Encrypt the enable and console passwords.

As you noticed in Step 7, the enable secret password was encrypted, but the enable and console passwords were still in plain text. We will now encrypt these plain text passwords using the service password-encryption command.

```bash
S1# config t
S1(config)# service password-encryption
S1(config)# exit
```

![App Screenshot](/Images/Switch%201/10.png)

#### Part 3: Configure a MOTD Banner

- Step 1: Configure a message of the day (MOTD) banner.

The Cisco IOS command set includes a feature that allows you to configure messages that anyone logging onto the switch sees. These messages are called message of the day, or MOTD banners. Enclose the banner text in quotations or use a delimiter different from any character appearing in the MOTD string.

```bash
S1# config t
S1(config)# banner motd "This is a secure system. Authorized Access Only!"
S1(config)# exit
%SYS-5-CONFIG_I: Configured from console by console
S1#
```

![App Screenshot](/Images/Switch%201/11.png)

#### Part 4: Save and Verify Configuration Files to NVRAM

- Step 1: Verify that the configuration is accurate using the show run command.

Save the configuration file. You have completed the basic configuration of the switch. Now back up the running configuration file to NVRAM to ensure that the changes made are not lost if the system is rebooted or loses power.

```bash
S1# copy running-config startup-config
Destination filename [startup-config]?[Enter]
Building configuration...
[OK]
```

![App Screenshot](/Images/Switch%201/12.png)

#### Part 5: Configure S2

You have completed the configuration on S1. You will now configure S2. If you cannot remember the commands, refer to Parts 1 to 4 for assistance.

Configure S2 with the following parameters:

Open Configuration Window for S2

a. Device name: S2

![App Screenshot](/Images/Switch%202/Enable.png)

![App Screenshot](/Images/Switch%202/Hostname.png)

b. Protect access to the console using the letmein password.

![App Screenshot](/Images/Switch%202/line%20console%200.png)

c. Configure an enable password of c1$c0 and an enable secret password of itsasecret.

![App Screenshot](/Images/Switch%202/acess%20pass%20zaki.png)

![App Screenshot](/Images/Switch%202/Step%204%20ena%20pass%20cisco.png)

d. Configure an appropriate message to those logging into the switch.

![App Screenshot](/Images/Switch%202/Step%205.png)

e. Encrypt all plain text passwords.

![App Screenshot](/Images/Switch%202/Step%208.png)

![App Screenshot](/Images/Switch%202/Step%206.png)

f. Ensure that the configuration is correct.

![App Screenshot](/Images/Switch%202/Step%207.png)

g. Save the configuration file to avoid loss if the switch is powered down.

![App Screenshot](/Images/Switch%202/Part%203%20step%201.png)

![App Screenshot](/Images/Switch%202/Part%204%20Step%201.png)
