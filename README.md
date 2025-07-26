# 🧨 Linux Priv-Esc + Log Poisoning Lab

🗓️ **Date:** July 2025  
🧪 **Type:** Red Team + SOC Simulation Lab  
🖥️ **System:** Debian-based VM  
🎯 **Goal:** Simulate attacker lifecycle – escalate, persist, exfil, hide

---

## 🔧 What I Did

Simulated a real-world Linux privilege escalation attack using misconfigured `sudo`, cron jobs, log poisoning, and data exfiltration.

| Phase            | Technique Used                                |
|------------------|------------------------------------------------|
| Priv-Esc         | `sudo -l` + GTFOBins (cat /etc/shadow)         |
| Persistence      | Cron job with reverse shell                    |
| Log Poisoning    | Forged log lines using `tee`, `sed`, and `truncate` |
| Exfiltration     | Sent `/etc/shadow` via `nc` with base64        |
| Cleanup          | Crontab removal, log wipe, stealth shell deletion |

---

## 🧪 Commands Used

See `commands_used.txt` for raw commands  
See `timeline.txt` for attacker PoV breakdown  
See `proof.txt` for summary of achieved outcomes

---

## 🔐 Proof Achieved

- ✅ Root shell access via `sudo /bin/cat /etc/shadow`
- ✅ Reverse shell set via cron
- ✅ `/var/log/auth.log` poisoned with fake login entries
- ✅ `/etc/shadow` exfiltrated over Netcat
- ✅ All tracks cleaned from system (cron, shell, logs)

---

## 🛡️ Blue Team Detection Strategy

- `grep -Ei 'bash|/dev/tcp' /var/log/auth.log`
- `sudo ausearch -f /etc/shadow`
- `crontab -l | grep /tmp`
- `ls -al /etc/cron* | grep stealth`

---

## ⚠️ Disclaimer

All actions performed in a controlled lab for educational purposes.  
Do not attempt on unauthorized systems.
