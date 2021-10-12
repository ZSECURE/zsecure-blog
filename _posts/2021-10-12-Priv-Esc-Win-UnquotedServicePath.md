# Privilege Escalation - Windows - How to find Unquoted Service Paths

Using a mixture of wmi and the find command you can search for Unquoted service paths using the below command
`wmic service get name,pathname,displayname,startmode | findstr /i auto | findstr /i /v "C:\Windows\\" | findstr /i /v """`