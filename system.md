1. 系統log在/var/log裡

2. last:使用 last 可以查得系統上面有登入主機者的身份，

```
$ last | grep "system boot"
```

可以看系統什麼時候被重開機

3. systemd-analyze: 看開機時系統做了什麼，還可以 systemd-analyze plot >> ~/1.svg存成svg檔用網頁開

4. journalctl

5. less -R 會上色

