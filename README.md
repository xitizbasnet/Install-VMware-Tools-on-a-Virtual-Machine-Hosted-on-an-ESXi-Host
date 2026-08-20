# Install-VMware-Tools-on-a-Virtual-Machine-Hosted-on-an-ESXi-Host
Install VMware Tools on a Virtual Machine Hosted on an ESXi Host

# Install VMware Tools on a Virtual Machine Hosted on an ESXi Host

> **📘 Overview**
> This guide provides instructions for installing **VMware Tools** on a virtual machine (VM) running on an **ESXi host**. The recommended installation method depends on the guest operating system.

## Method 1: Install VMware Tools from the ESXi Host — Recommended

Follow these steps to install VMware Tools through the **vSphere Client**:

1. Sign in to the **vSphere Client**.
2. Select the virtual machine.
3. Right-click the VM and select:
   **Guest OS → Install VMware Tools**
   or
   **Guest OS → Upgrade VMware Tools**
4. ESXi mounts a **VMware Tools ISO** to the VM's virtual CD/DVD drive.

> **💡 Tip**
> Ensure that the VM's virtual CD/DVD drive is connected before proceeding with the installation.

---

## For Windows Guest OS

1. Sign in to the Windows VM.
2. Open **This PC** and locate the mounted VMware Tools CD drive.
3. Run the VMware Tools installer:

```text
setup.exe
```

4. Select **Typical** installation.
5. Complete the installation wizard.
6. Reboot the VM.

> **⚠️ Important**
> Rebooting the VM may be required for all VMware Tools components and drivers to become fully operational.

---

## For Linux Guest OS

For modern Linux distributions, VMware recommends using **Open VM Tools**.

### RHEL / CentOS / Rocky / AlmaLinux

Install Open VM Tools:

```bash
sudo dnf install open-vm-tools -y
```

Enable and start the VMware Tools service:

```bash
sudo systemctl enable --now vmtoolsd
```

Reboot the VM:

```bash
sudo reboot
```

### Ubuntu / Debian

Update the package repositories:

```bash
sudo apt update
```

Install Open VM Tools:

```bash
sudo apt install open-vm-tools open-vm-tools-desktop -y
```

Enable and start the Open VM Tools service:

```bash
sudo systemctl enable --now open-vm-tools
```

Reboot the VM:

```bash
sudo reboot
```

---

## Verify Installation

After installation, verify that VMware Tools is running correctly.

### Windows

Open:

```text
services.msc
```

Ensure that **VMware Tools Service** is running.

### Linux

Check the installed VMware Tools version:

```bash
vmware-toolbox-cmd -v
```

Alternatively, check the service status:

```bash
systemctl status vmtoolsd
```

---

## Check VMware Tools Status from vSphere

To verify the VMware Tools status from the **vSphere Client**:

**VM → Summary → VMware Tools**

You should see:

```text
VMware Tools: Running (Current)
```

> **✅ Expected Result**
> The **VMware Tools** status should indicate that the tools are **Running (Current)**.

---

## Troubleshooting

Use the following checks if VMware Tools installation or operation encounters issues:

* Ensure the VM's **CD/DVD drive is connected**.
* If the VMware Tools ISO fails to mount, verify that the **ESXi host has the VMware Tools package installed**.
* For Linux distributions, prefer **Open VM Tools**, as it is the VMware-supported method for most modern distributions.

> **🔧 Troubleshooting Tip**
> When troubleshooting, first verify the VM's virtual CD/DVD connection and the VMware Tools service status inside the guest operating system.

---

## Additional Information

If you provide the following environment details, exact installation commands and procedures can be provided:

* **Guest OS version** — for example, Windows Server, Ubuntu, CentOS, etc.
* **ESXi version**

> **📌 Note**
> Installation commands and procedures may vary depending on the guest operating system and ESXi version.
