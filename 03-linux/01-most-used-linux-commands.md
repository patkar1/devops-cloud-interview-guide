## Question  
What are 10 Linux commands you use daily? (Excluding basic ones like `ls` and `cd`)

### 📝 Short Explanation  
This question aims to assess your hands-on experience with Linux, focusing on diagnostic, file manipulation, service management, and automation-related commands that go beyond basic navigation.

## ✅ Answer  
Here are 10 Linux commands I use regularly, excluding the basics like `cd`, `ls`, and `pwd`:

---

### 1. `tail -f`  
```bash
tail -f /var/log/nginx/error.log
```
🔍 Monitor log files in real time — very useful for debugging issues as they happen.

---

### 2. `grep`  
```bash
grep -i "timeout" /var/log/app.log
```
🔎 Search through files, logs, or command outputs for specific patterns. I use this to quickly isolate errors.

---

### 3. `systemctl`  
```bash
systemctl restart nginx
```
🛠️ Control system services — starting, stopping, checking status of systemd services.

---

### 4. `journalctl`  
```bash
journalctl -u docker.service -f
```
🧾 View logs for systemd-managed services. Especially handy for debugging issues with services like Docker or Kubelet.

---

### 5. `ps aux | grep`  
```bash
ps aux | grep nginx
```
📋 List running processes. I use this to find rogue or resource-intensive processes.

---

### 6. `df -h` / `du -sh`  
```bash
df -h       # Check available disk space  
du -sh *    # See folder sizes in current directory
```
💾 Essential for disk space monitoring and cleaning up large files or folders.

---

### 7. `chmod` / `chown`  
```bash
chmod +x deploy.sh  
chown ubuntu:ubuntu script.sh
```
🔐 Manage file permissions and ownership — very common in CI/CD and provisioning tasks.

---

### 8. `find`  
```bash
find /var/log -name "*.log" -mtime +7
```
🔍 Locate files based on name, date, type, etc. Great for automating cleanup or audits.

---

### 9. `curl`  
```bash
curl -I http://localhost:8080
```
🌐 Test web endpoints, APIs, or service availability from the command line.

---

### 10. `rsync`  
```bash
rsync -avz /app/ user@server:/backup/
```
📁 Efficient file syncing and backup — much faster and more reliable than `scp` for large directories.

---

my interview question from gpt

Basic Level Questions

1. What is Shell Scripting?

Answer:
Shell scripting is writing a series of commands for the shell to execute in a file. It automates repetitive tasks, system administration, application deployment, etc.


---

2. Which shells are commonly used?

Answer:

Bash (Bourne Again Shell) – Most common

sh (Bourne Shell)

csh (C Shell)

ksh (Korn Shell)

zsh (Z Shell)



---

3. How do you make a shell script executable?

Answer:

chmod +x script.sh

Then run it using:

./script.sh


---

4. How do you define and access variables in shell script?

Answer:

name="Satish"
echo $name


---

5. What are positional parameters in shell scripting?

Answer:
They are variables that store arguments passed to a script:

$0 – Script name

$1, $2, … – First, second… arguments

$# – Number of arguments

$@ – All arguments



---

🔹 Intermediate Level Questions

6. How do you write an if-else statement in bash?

Answer:

if [ $age -gt 18 ]; then
  echo "Adult"
else
  echo "Minor"
fi


---

7. How do you write a for loop in shell?

Answer:

for i in 1 2 3 4 5
do
  echo "Number $i"
done


---

8. What is the use of #!/bin/bash at the top of scripts?

Answer:
It's called a shebang. It tells the system which interpreter to use (here, Bash) to execute the script.


---

9. What is the difference between "$*" and "$@"?

Answer:

"$*" – Treats all arguments as a single string.

"$@" – Treats each argument as a separate string.


Example:

for arg in "$@"; do
  echo $arg
done


---

10. How do you redirect output and errors in shell?

Answer:

command > out.txt         # stdout
command 2> error.txt      # stderr
command &> both.txt       # stdout + stderr


---

11. How to check if a file exists in a shell script?

Answer:

if [ -f myfile.txt ]; then
  echo "File exists"
fi


---

12. What is the difference between == and -eq?

Answer:

== is used for string comparison.

-eq is used for integer comparison.



---

🔹 Advanced Level Questions

13. What are trap commands?

Answer: Used to catch signals and run cleanup code before exiting:

trap "echo Caught SIGINT; exit" SIGINT


---

14. How do you pass arguments and return values from a function?

Answer:

myfunc() {
  echo "Hello $1"
  return 5
}

myfunc "DevOps"
echo $?  # This will print 5


---

15. What is set -e in bash?

Answer: It causes the script to exit immediately if any command returns a non-zero status (fail fast).


---

16. How can you read input from a user in shell?

Answer:

read -p "Enter your name: " name
echo "Hello $name"


---

17. How do you debug a shell script?

Answer: Use:

bash -x script.sh

or add set -x inside the script to see commands as they execute.


---

18. How to schedule a shell script with cron?

Answer: Use crontab -e and add:

0 2 * * * /home/user/script.sh

(This runs the script at 2 AM daily)


---

19. How do you compare strings in bash?

Answer:

if [ "$str1" == "$str2" ]; then
  echo "Strings match"
fi


---

20. What are some best practices in shell scripting for DevOps?

Answer:

Always use #!/bin/bash

Use set -euo pipefail for strict error handling

Validate inputs

Use meaningful variable/function names

Comment your code

Avoid hardcoding values

Log output and errors properly
