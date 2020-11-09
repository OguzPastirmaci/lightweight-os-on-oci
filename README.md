# Testing boot times of lightweight Linux distributions for running containers on OCI


## Test results
All tests were run on `VM.Standard.E3.Flex.4` shape in US West (Phoenix) region.

| OS             | OS version      | Docker version | Out of the box boot time with Docker   installed |
|----------------|-----------------|----------------|--------------------------------------------------|
| Clear Linux    | 33930           | 19.03.8        | 3.083s                                           |
| Fedora CoreOS  | 32.20201018.3.0 | 19.03.11       | 7.844s                                           |
| Flatcar Linux  | 2605.7.0        | 19.03.12       | 8.174s                                           |
| Ubuntu Minimal | 20.04           | 19.03.13       | 11.344s                                          |
| Ubuntu Core    | 18              | 19.03.11       | 14.823s                                                 |

## Test summary

- Ubuntu Minimal 20.04 is the only official OCI platform image in the test.
- Ubuntu Minimal 20.04's average boot time becomes `9.598s` when [Oracle Cloud Agent](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/enablingmonitoring.htm) service is disabled. The boot time becomes `9.598s` when Oracle Cloud Agent is removed.

- Flatcar Linux is [in the list](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/importingcustomimagelinux.htm#ossupport) of Linux Distributions that Support Custom Image Import on OCI.

- Clear Linux has the best boot time.


## What does supported/not supported mean?
OCI has a list of Linux distributions that support bringing your own image. If the Linux distribution is not in the list, it does not mean that it wouldn't work on OCI. It means that if you have any issues running it, Oracle will provide "commercially reasonable support limited to getting an instance launched and accessible via SSH."

See [this link](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/importingcustomimagelinux.htm#Importing_Custom_Linux_Images) for more information.

## Test steps

1 - Create the VM.

2 - Install Docker using the official instructions from the OS documentation.

3 - Reboot the VM.

4 - Stop the VM from OCI console.

5 - Start the VM and run `systemd-analyze` to check how long booting took.

6 - Repeat steps 4 & 5 three times and get the average of `systemd-analyze` results.

## Remarks on tested Linux distros


### Clear Linux
https://clearlinux.org/

Clear Linux OS is an open source, rolling release Linux distribution optimized for performance and security, from the Cloud to the Edge, designed for customization, and manageability.

- Not in the list of "Linux Distributions that Support Custom Image Import".
- Lowest boot time in the test.
- A distro by Intel so it's highly tuned for Intel platforms but works well with AMD, too. AMD even recommends using Clear Linux for performance testing its CPUs.

### Fedora CoreOS
https://getfedora.org/en/coreos

Fedora CoreOS is an automatically-updating, minimal operating system for running containerized workloads securely and at scale.

- Not in the list of "Linux Distributions that Support Custom Image Import".

### Flatcar Linux
https://www.flatcar-linux.org/

Flatcar Container Linux is an immutable Linux distribution for containers.

- In the list of "Linux Distributions that Support Custom Image Import".
- A fork of the CoreOS Container Linux and maintained by [Kinvolk](https://kinvolk.io/).

### Ubuntu Minimal
https://wiki.ubuntu.com/Minimal

Minimal Ubuntu is a set of Ubuntu images designed for automated deployment at scale and made available across a range of cloud substrates.

- The only official OCI platform image in the test list.
- Boot time can be lowered to `9.598s` by disabling Oracle Cloud Agent.

### Ubuntu Core
https://ubuntu.com/core

Ubuntu Core is a tiny, transactional version of Ubuntu for IoT devices and large container deployments.

- In the list of "Linux Distributions that Support Custom Image Import".
