---
title: "5.11.1 Creating CPU Load"
weight: 1
---

In the SSH terminal, install the stress tool:

```bash
sudo yum install stress -y
```

Run CPU load for 5 minutes:

```bash
stress --cpu 2 --timeout 300
```

During the test, CPU utilization increases significantly, creating the conditions for the Alarm to be triggered.