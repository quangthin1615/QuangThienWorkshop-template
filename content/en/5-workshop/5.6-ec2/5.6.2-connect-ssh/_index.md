---
title: "5.6.2 Connect to EC2 Using SSH"
weight: 2
---

## Connect Using PowerShell

```bash
cd $HOME\Downloads
```

Set the key permissions:

```bash
icacls.exe .\monitoring-lab-key.pem /reset
icacls.exe .\monitoring-lab-key.pem /grant:r "$($env:USERNAME):(R)"
icacls.exe .\monitoring-lab-key.pem /inheritance:r
```

Connect:

```bash
ssh -i "monitoring-lab-key.pem" ec2-user@<Public-IP>
```

Type `yes` when asked to confirm the host fingerprint.

## Result

The SSH session connects successfully to the Amazon Linux 2023 instance.

![SSH connection](/QuangThienWorkshop-template/images/figure-04.png)
*Figure 4. Successful SSH connection to the EC2 instance.*
