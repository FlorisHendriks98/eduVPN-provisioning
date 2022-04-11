# Introduction

In its current state, eduVPN needs client interaction in order to establish a VPN connection.

It is also possible, for Windows and MacOS, to make eduVPN a system VPN that is always on via provisioning.

In this document we describe the steps in order to make this possible.

# Windows
## Prerequisites
* An AD Windows server with Active Directory Certificate Services installed. Make sure that automatic enrollment of computer certificates via GPO is enabled: https://www.youtube.com/watch?v=l03jXuR6dJw
* Fully set up eduVPN server.



# MacOS
## Prerequisites
* An AD Windows server with Active Directory Certificate Services installed. Make sure that automatic enrollment of computer certificates via GPO is enabled: https://www.youtube.com/watch?v=l03jXuR6dJw
* Fully deployed eduVPN server.
* macOS server with profilemanager enabled.

## Step 1
Here we configure a profile for the macOS client. With this profile we enroll the macOS client in AD and retrieve a machine certificate via RPC.

First open up the my devices web application and enroll the device to macOS server.

![Screenshot 2022-04-11 at 13 17 40](https://user-images.githubusercontent.com/47246332/162730069-cd00267a-0f97-4e0b-8e18-f3b848757996.png)

Next open the profile manager web application and edit the following settings for a device or group of devices (make sure that Certificate Server and Certificate Authority has the names of your own infrastructure):
* AD certificate

![Screenshot 2022-04-11 at 13 32 43](https://user-images.githubusercontent.com/47246332/162731516-ebbc1911-e137-4344-b7ee-bccf0b7f4f03.png)

* Directory (you can skip this step if the computer is already AD joined)

![Screenshot 2022-04-11 at 13 44 13](https://user-images.githubusercontent.com/47246332/162733002-6518fa42-907c-4987-ab40-e990271b87f2.png)
Note that we use as client ID %SerialNumber%, this ensure us that we do not have a duplicate name in Active Directory (https://discussions.apple.com/thread/7987975). If you want to use a different client ID, such as the hostname of the client, then the syntax can be found here https://support.apple.com/en-gb/guide/deployment/dep23422775/web.

After saving the profile configuration check if it is automatically pushed to the macOS client. If not download and install it manually (https://support.apple.com/en-gb/guide/profile-manager/pmdbd71ebc9/mac). 

## Step 2
Check the keychain access, you should now have a certificate with the name SERIALNUMBER.HOSTNAME. This is the machine certificate which is used to authenticate API calls in order to retrieve a VPN configuration.

Clone the repository:
`git clone `

Move the 
