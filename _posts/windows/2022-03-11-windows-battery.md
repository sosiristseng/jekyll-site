---
title: "Check battery status in Windows"
date: 2022-03-11T15:18:19+08:00
tags: ["windows", "battery"]
categories: ["Windows"]
---

To check laptop battery status and health, open Windows Powershell with Admin rights and run

```powershell
powercfg /batteryreport /output "C:\battery-report.html"
```

And open `C:\battery-report.html`

<!--more-->

Source: <https://www.pcmag.com/how-to/how-to-check-your-laptops-battery-health-in-windows-10>
