# Testing lightweight OS for running containers on OCI

All tests were run on VM.Standard.E3.Flex.4 shape in US West (Phoenix) region. Grub timeout was set to 0 where applicable.

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
