# Testing boot times of lightweight Linux distributions for running containers on OCI


## Test results
All tests were run on VM.Standard.E3.Flex.4 shape in US West (Phoenix) region. Grub timeout was set to 0 where applicable.

| OS                   | Out of the box boot time with Docker   installed |
|----------------------|--------------------------------------------------|
| Clear Linux 33930    | 3.083s                                           |
| Fedora CoreOS 32     | 7.844s                                           |
| Flatcar Linux 2605   | 8.174s                                           |
| RancherOS 1.5.6      |                                                  |
| Ubuntu 20.04 Minimal | 11.344s                                          |
| Ubuntu Core 18       |                                                  |

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

- Lowest boot time in the test.
- A distro by Intel so it's highly tuned for Intel platforms but works well with AMD, too. AMD even recommends using Clear Linux for performance testing its CPUs.
- Not in the list of "Linux Distributions that Support Custom Image Import".


## Fedora CoreOS 32.20201018.3.0 with Docker 19.03.11

## Flatcar Linux 2605.7.0 with Docker 19.03.12

## RancherOS 1.5.6 with Docker 19.03.11

## Ubuntu 20.04 Minimal with Docker 19.03.13

## Ubuntu Core 18 with Docker 19.03.11


