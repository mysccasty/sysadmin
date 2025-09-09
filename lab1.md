## Лабораторная работа 1
Кузнецов Владимир Александрович
Группа: P4250
### 1. SSH  
Подключение в локальной сети 
```shell
ssh -i ~/.ssh/id_ed25519 -p 22222 'student@192.168.1.142'
```
```text
Linux mysc 6.1.0-39-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.148-1 (2025-08-26) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
student@mysc:~$
```
После изменения /etc/motd
```text
Linux mysc 6.1.0-39-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.148-1 (2025-08-26) x86_64
Hello, very nice to meet you!
```
### 2. iptables  
nmap не получает ответ из-за правил iptables  
```shell
nmap -p 22222 192.168.1.142
```
```text
Starting Nmap 7.98 ( https://nmap.org ) at 2025-09-09 16:09 +0300
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up) scanned in 3.04 seconds
```
Запускаем nmap без пинг проверки
```shell
nmap -Pn -p 22222 192.168.1.142
```
```text
Starting Nmap 7.98 ( https://nmap.org ) at 2025-09-09 16:11 +0300
Nmap scan report for 192.168.1.142
Host is up (0.036s latency).

PORT      STATE SERVICE
22222/tcp open  easyengine

Nmap done: 1 IP address (1 host up) scanned in 4.06 seconds
```
### 4. Логирование и анализ  
Команда для получения логов  
```shell
sudo journalctl -u ssh
```
Подключение с публичным ключом
```text
Accepted publickey for student from 192.168.1.84 port 61401 ssh2: ED25519
```
Попытка подключиться с другого устройства без публичного ключа
```text
Connection reset by authenticating user student 192.168.1.89 port 52585 [preauth]
```
Было получено 2 успешных подключения по ключу и 3 неуспешных, разрыв соединения во время аутентификации
