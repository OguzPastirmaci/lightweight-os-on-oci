# Testing boot times of lightweight Linux distributions for running containers on OCI


## Test results
All tests were run on VM.Standard.E3.Flex.4 shape in US West (Phoenix) region. Grub timeout was set to 0 where applicable.

| OS             | Version         | Out of the box boot time with Docker installed |
|----------------|-----------------|--------------------------------------------------|
| Clear Linux    | 33930           | 3.083s                                           |
| Fedora CoreOS  | 32.20201018.3.0 | 7.844s                                           |
| Flatcar Linux  | 2605.7.0        | 8.174s                                           | 
| RancherOS      | 1.5.6           |                                                  |
| Ubuntu Minimal | 20.04           | 11.344s                                          |
| Ubuntu Core    | 18              |                                                  |

Summary

- Ubuntu Minimal 20.04 is the only official OCI platform image within the list of Linux distros in this list.
- Ubuntu Minimal 20.04's average boot time is `9.598s` when [Oracle Cloud Agent](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/enablingmonitoring.htm) service is disabled. The boot time becomes `8.257s` when both Oracle Cloud Agent and `cloud-init` services are disabled. 


#### Test steps

1 - Create the VM.

2 - Install Docker using the official instructions from the OS documentation.

3 - Reboot the VM.

4 - Stop the VM from OCI console.

5 - Start the VM and run `systemd-analyze` to check how long booting took.

6 - Repeat steps 5 & 6 three times and get the average of `systemd-analyze` results.


## What does supported/not supported mean?
OCI has a list of Linux distributions that support bringing your own image. If the Linux distribution is not in the list, it does not mean that it wouldn't work on OCI. It means that if you have any issues running it, Oracle will provide "commercially reasonable support limited to getting an instance launched and accessible via SSH."

See [this link](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/importingcustomimagelinux.htm#Importing_Custom_Linux_Images) for more information.

## Clear Linux 33930 with Docker 19.03.8
https://clearlinux.org/

- Not in the list of "Linux Distributions that Support Custom Image Import".
- Lowest boot time in the test.
- A distro by Intel so it's highly tuned for Intel platforms but works well with AMD, too. AMD even recommends using Clear Linux for performance testing its CPUs.

## Fedora CoreOS 32.20201018.3.0 with Docker 19.03.11
https://getfedora.org/en/coreos

- Not in the list of "Linux Distributions that Support Custom Image Import".

## Flatcar Linux 2605.7.0 with Docker 19.03.12
https://www.flatcar-linux.org/

- In the list of "Linux Distributions that Support Custom Image Import".

## RancherOS 1.5.6 with Docker 19.03.11
https://rancher.com/docs/os/v1.x/en/

- Not in the list of "Linux Distributions that Support Custom Image Import".

## Ubuntu 20.04 Minimal with Docker 19.03.13
https://wiki.ubuntu.com/Minimal

- The only official OCI platform image in the test list.
- Boot time can be lowered to `8.257s` by disabling Oracle Cloud Agent and `cloud-init`.

## Ubuntu Core 18 with Docker 19.03.11
https://ubuntu.com/core

- In the list of "Linux Distributions that Support Custom Image Import".
