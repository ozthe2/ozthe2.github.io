---
layout: post
title:  "Work Folders: Configure in a Failover Cluster Using Certificates from an Internal CA"
date:   2018-06-03 22:00:00 +0000
categories: WorkFolders
tags: [workfolders, failover, cluster, certificate, CA]
---
Today, I began to configure Work Folders in a two-node failover cluster for my workplace.  The implementation that we chose will use our internal Certificate Authority as syncing will only occur to computers when they are connected to our LAN internally. (We use [DirectAccess](https://docs.microsoft.com/en-us/windows-server/remote/remote-access/directaccess/directaccess) so computers always appear on the LAN even when out of the workplace.)  This is good news for me as it means I do not need (at least for now) to configure a WAP or ADFS server.

To start with, I fired up a lab in Hyper-v that was as close as possible to the actual production environment, using Windows Server 2012 R2 as a target server in order to present iSCSI storage to the cluster.

This is not like my usual step-by-step guides, more a documentation of the certificates procedure I used in order to get Work Folders functioning in my lab.  I found there was a lot of information on using self-signed certificates in a lab environment and also for a single Work Folders server – but not much on configuring certificates in a clustered capacity using an internal CA which requires a few different steps.  It also contains a couple of other related items I discovered on my voyage when using a failover cluster with Work Folders (such as CNAME in DNS).

So without further ado, let’s go….

### On the Certificate Authority:
On our CA, I copied the Web Server template, gave it a meaningful name and allowed the private key to be exported.  This is an important step as I will be installing this same certificate on multiple servers:

![wf1](/assets/images/wf1.JPG)

I then gave Authenticated users the enrol permission:

![wf2](/assets/images/wf2.JPG)

…and ensured that ‘Supply in the request was selected’

![wf3](/assets/images/wf3.JPG) 

### The Storage:
Having started the iSCSI initiator on the first sync server and configured the storage, I then took the storage offline.

Repeat this for the second node (and any other nodes that make up your cluster)
 

### Certificate Request:
On the first Work Folders Sync Server, I used the following details in the certificate request:

![wf4](/assets/images/wf4.JPG)

The important items to note here are that the common name should be workfolders.your.domain and the same for the alternative DNS name.  In addition, you will need to add the name of the VCO (Virtual Cluster Object).  In my case, It was named  fs1 as shown in the next screenshot taken from the Failover Cluster Manager console:

![wf5](/assets/images/wf5.JPG) 

### Configure the SSL certificate binding:
On one of the Work Folders sync servers, perform the following…

To configure the SSL certificate binding you will need to know the thumbprint of the certificate.  I did this in Powershell using the following command:

`Get-ChildItem -Path cert:\localmachine\my`

![wf6](/assets/images/wf6.JPG)

And then in an Administrative command prompt – (Not PowerShell!) I typed the following:

`netsh http add sslcert ipport=0.0.0.0:443 certhash=<Cert thumbprint> appid={CE66697B-3AA0-49D1-BDBD-A25C8359FD5D} certstorename=MY`
Obviously replacing <Cert thumbrint> with your certificate thumbprint!)

Note, ensure you use the ipport of *0.0.0.0:443* as shown in the command line.

### Export the Certificate:
On the same server that you just completed the certificate binding on, export the certificate…

![wf7](/assets/images/wf7.JPG)

### On the other sync server cluster nodes:
Import the certificate!
    
![wf8](/assets/images/wf8.JPG)
    
Configure the SSL certificate binding as per the instructions above.

### Add a CNAME in DNS
Add a cname of workfolders that points to your cluster file server role name – ie the VCO name (Virtual Cluster Object) – In my case I had named it fs1

![wf9](/assets/images/wf9.JPG)
 

That was it – after this, Work Folders worked like a charm! Sweet! 