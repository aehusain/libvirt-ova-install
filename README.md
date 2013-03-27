libvirt
=======

Libvirt is a public virtalization library, this repo shares the work which for some reason cannot be ported upstream.


I. OVA install for ESXi server

OVA stands for Open Virtualization Archive, it is an standard defined by consortium to pacakage and distribute
Virtual Machines. It defines necessary elements needed by VM such as: 
1. virtual hardware description.
2. virtual disk
3. networking definition for VM etc.

Natively Libvirt does not have a support to install OVA pacakages. I have submitted this patch to the upstream but 
as ESX deals with it in a peculiar way which is not same for all hypervisors. The major steps needed for performing
an OVA install on ESX are:
1. Run virtual machine spec against the server (ParseOVFDescriptor)
2. Create VM entity on the server
3. Transfer the disk pacaked inside OVA to the server. 

Below pacthes enable Libivrt to perform all above mentioned steps:
1. Public-API-to-allow-defining-new-domain-using-OVA-file.patch (defines a public API to perform OVA install)
2. Parsing-and-file-handling-operations-for-an-OVA-file.patch (enable Libvirt to parse OVA)
3. ESX-CURL-routine-to-allow-file-upload-to-the-server.patch (append file upload capability to Libvirt ESX driver)
4. ESX-Driver-support-to-define-new-domain-using-an-OVA.patch (append ESX driver to perform above mentioned
  operations)
5. virsh-Command-to-define-new-domain-using-OVA-package.patch (append virish command to perform OVA installs)

Please apply above patches to your Libvirt branch, I suspect their may be merge conflicts while applying patch 1
but others should apply well :-).

Please report if you see any issue. 

Thanks!
