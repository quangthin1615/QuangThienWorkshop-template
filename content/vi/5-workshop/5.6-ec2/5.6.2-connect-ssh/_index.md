---
title: "5.6.2 Kết nối SSH"
weight: 2
---

## Kết nối bằng PowerShell

1. Mở PowerShell trên Windows.
2. Di chuyển tới thư mục chứa key:

```powershell
cd $HOME\Downloads
```

3. Cấp quyền cho key:

```powershell
icacls.exe .\monitoring-lab-key.pem /reset
icacls.exe .\monitoring-lab-key.pem /grant:r "$($env:USERNAME):(R)"
icacls.exe .\monitoring-lab-key.pem /inheritance:r
```

4. Kết nối:

```powershell
ssh -i "monitoring-lab-key.pem" ec2-user@<Public-IP-cua-instance>
```

5. Gõ `yes` nếu được hỏi xác nhận fingerprint.

![Hình 4. Kết nối SSH vào instance thành công qua PowerShell](/QuangThienWorkshop-template/images/figure-04.png)

## Kết quả

Kết nối SSH vào EC2 thành công.
