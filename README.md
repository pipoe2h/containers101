# Containers 101
The Containers 101 Workshop includes some labs. If you would like to take the labs you will need to configure your Wi-Fi interface following the steps below.

Each delegate has been assigned with an unique number. It's important you use your number to avoid any clash with other delegates.

## Configuring your Wi-Fi interface
You must connect to WeWork Wi-Fi to get access to the lab platform. This platform is running on a different IP range within the same L2 network, what makes the requirement to create an IP alias to your Wi-Fi connection in order to reach the lab platform.

Follow the next steps according to your computer operating system. Before you run the commands make sure you are connected to WeWork Wi-Fi and you can access the Internet.

* Windows user
  * Open your "Network Connections" and write down your Wi-Fi connection name (usually *Wi-Fi*)
  * Open a privileged *CMD.EXE* (RunAs Administrator)
  * Run the following command. Your Wi-Fi connection name and your delegate number is required:
  ```basic
  REM Enable dhcpstaticipcoexistence to allow for both DHCP and Static IP
  netsh interface ip set interface interface="<Wi-Fi Connection Name>" dhcpstaticipcoexistence=enable

  REM Add secondary Static IP (takes a few seconds to show up in ipconfig)
  netsh int ip add address "<Wi-Fi Connection Name>" 10.10.56.2<delegate number> 255.255.255.0
  ``` 

  Example for delegate *01*:
  ```basic
  netsh interface ip set interface interface="Wi-Fi" dhcpstaticipcoexistence=enable
  netsh int ip add address "Wi-Fi" 10.10.56.201 255.255.255.0
  ```
  * Test you can ping the Prism Central address (10.10.56.30)
  ```basic
  ping 10.10.56.30
  ```

* macOS user
  * Open a terminal
  * Run the following command. Your delegate number is required:
  ```bash
  echo "Add secondary Static IP"
  sudo ifconfig en0 alias 10.10.56.2<delegate number>/24 up
  ``` 

  Example for delegate *01*:
  ```bash
  sudo ifconfig en0 alias 10.10.56.201/24 up
  ```
  * Test you can ping the Prism Central address (10.10.56.30)
  ```bash
  ping 10.10.56.30
  ```

# Lab Setup
A SuperNuc is running AOS and Prism Central 5.9 with AHV. The lab uses Calm to provision a Linux instance with Docker (RancherOS) for each of the delegates.

Also, in the same Calm blueprint a *Registry Cache* instance is provisioned to reduce access to the Internet when pulling images.

Finally, a private Docker registry is provisioned too to upload the container images you will develop during the workshop.

```
Prism Central: https://10.10.56.30:9440
Username: admin
Password: <Check flip chart board>
```

## How to connect to your instance
You need to gather your instance IP address via Prism Central. You can use the *Explore* tab or do it via the *Calm* tab and looking for the *Bootcamp* application.

The instances are named **rancheros-\<delegate number>\-\<random numbers>**. Grab the IP address and connect using SSH.

* Windows user. You can use PuTTy.
* macOS user. Just use your terminal.

```
Username: rancher
Password: <Check flip chart board>
Port: 22
```

# Let's get started
1. Open Prism Central
2. Find the IP address of your instance and write it down
3. Connect to your instance via SSH
4. Clone the GitHub
```shell
git clone https://github.com/pipoe2h/containers101.git
```
5. List the directories to check the repo has been cloned
```shell
ls
```
```shell

```