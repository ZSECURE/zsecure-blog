# Enumeration | SMB - Port 445

## Enumerate with crackmapexec
(hostname | domain name might be leaked)

```crackmapexec smb 10.10.10.123```

Enumerate password policy from the domain helpful for brute-forcing

```crackmapexec smb 10.10.10.123 --pass-pol```

Enumerate shares

```crackmapexec smb 10.10.10.123 --shares```

## Enumerate using smbclient

Enumerate shares

```smbclient -L //10.10.10.123```

Enumerate shares

```smbmap -H 10.10.10.123```

## Enumerate using smbmap

Enumerate shares using a user that doesn't exist, sometimes specifying no user doesn't give you the same result.

```smbmap -H 10.10.10.123 -U 'asdf'```

## Enumerate using Enum4Linux

Quickly get all the SMB information in one scan

```enum4linux -a 10.10.10.123```
