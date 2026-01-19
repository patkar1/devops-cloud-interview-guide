## Question  
`/var` is almost 90% full. What will be your next steps?

### 📝 Short Explanation  
This question checks your troubleshooting and disk management skills. The `/var` directory is commonly used for logs, spools, caches, and runtime data — so issues here can break system processes or fill up disks silently.

## ✅ Answer  
My first step is to identify what’s consuming the space inside `/var`. Then I would clean up unnecessary files like rotated logs, caches, or orphaned packages — and put alerts or log rotation in place to avoid recurrence.

### 📘 Detailed Explanation  

---

### ✅ Step 1: Inspect Disk Usage Under `/var`

```bash
sudo du -sh /var/* | sort -hr | head -10
```
This will show which directories inside `/var` are consuming the most space — usually it’s `/var/log`, `/var/cache`, or `/var/lib/docker`.

---

### ✅ Step 2: Clean Log Files  
If `/var/log` is the culprit:

```bash
sudo journalctl --vacuum-size=200M
sudo rm -rf /var/log/*.gz /var/log/*.[0-9]
```

Or truncate large log files:
```bash
sudo truncate -s 0 /var/log/syslog
```

---

### ✅ Step 3: Clear Package Cache  
If using `apt` or `yum`, clear the package manager cache:

```bash
sudo apt clean         # Debian/Ubuntu
sudo yum clean all     # RHEL/CentOS
```

---

### ✅ Step 4: Check Docker Artifacts  
If the server runs containers:

```bash
docker system df        # See what’s taking space
docker system prune -a  # Remove unused containers/images
```

**⚠️ Warning:** Prune removes *unused* images and volumes — be cautious on production systems.

---

### ✅ Step 5: Consider Moving or Archiving Data  
If data in `/var` is needed but rarely accessed:
- Archive old logs to `/home` or S3
- Use `logrotate` to compress and limit logs:
  ```bash
  sudo nano /etc/logrotate.conf
  ```

---

### ✅ Step 6: Set Up Alerts and Monitoring  
- Install `ncdu`, `duf`, or setup Prometheus/Grafana alerts for disk usage thresholds.
- Automate cleanup with cron or systemd timers if appropriate.

---

### 🧠 Why `/var` Fills Up:
- Verbose logging (e.g., failed cron jobs, app debug logs)
- Docker images/layers
- Orphaned cache files
- Email spools or crash dumps

> Summary:  
> Quickly inspect, clean, and automate monitoring. Ensure critical services like journald, docker, and package managers are not starved of space.



my method 

/var filesystem is almost 90% full

Step 1: Confirm the problem

First, I check whether /var is really full and how much space is left.

df -h /var


👉 This tells me the exact usage and available space.

Step 2: Find what is using space inside /var

Next, I identify which directory is consuming the most space.

du -sh /var/*


Most of the time, large usage comes from:
-s is summery and h is for human redalbe du is used for which directory is using the space

/var/log → log files

/var/lib → Docker, databases

/var/cache → package cache

/var/tmp → temporary files

Step 3: Check log files (most common reason)

Logs grow very fast, especially in production.

du -sh /var/log/*


If I find very large logs, I truncate them safely (not delete).

> /var/log/syslog
> /var/log/messages


👉 Truncating clears content but keeps the file for the running service.

Step 4: Check Docker or application data

If Docker is running, it usually consumes a lot of space.

du -sh /var/lib/docker
docker system df


Then I clean unused Docker data safely:

docker system prune -a -f


👉 This removes unused images, containers, and frees disk space.

Step 5: Clean cache and temp files

These files are safe to clean.

apt-get clean        # Ubuntu
yum clean all        # RHEL/CentOS
rm -rf /var/tmp/*

Step 6: Check for deleted but open files

Sometimes files are deleted but still held by a running process.

lsof | grep deleted


If found, I restart the related service.

Step 7: Verify disk space again

After cleanup, I confirm the space is freed.

df -h /var

Step 8: Prevent this in future (Important)

Ensure log rotation is enabled

Set disk usage alerts (80%, 90%)

Move heavy data like Docker to a separate disk

Interview-Ready Short Answer (You can say this 👇)

“First, I check disk usage and identify what is consuming space under /var. I clean large logs, unused Docker data, cache and temp files, check for deleted open files, and finally ensure log rotation and monitoring to prevent future issues.”

If you want, I can also:

Convert this into 1-minute interview answer

Give a real Azure VM example

Share a cleanup automation script

Just tell me 👍

https://chatgpt.com/share/696eacfa-796c-8005-b38b-9949e1dbf25e
---
