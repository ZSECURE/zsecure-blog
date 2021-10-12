# Curl Commands

## Get Command
```
~# curl http://10.10.53.235:8081/ctf/get
thm{****f99f}
```

## Post Commands
```
~# curl http://10.10.53.235:8081/ctf/post -d "flag_please"
thm{****ba09}
```

## Get a cookie and save to desktop
```
~# curl http://10.10.53.235:8081/ctf/getcookie -c Desktop/cookie.txt
Check your cookies!
```

## Curl command with cookie
```
~# curl http://10.10.53.235:8081/ctf/sendcookie -b flagpls=flagpls
thm{****47b3}
```
