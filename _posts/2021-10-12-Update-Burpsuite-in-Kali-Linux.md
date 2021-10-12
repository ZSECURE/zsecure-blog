# How to Update Burp Suite in Kali Linux

You can quickly launch Burp Suite Community from the Favorites section on the left. FYI, Burp Suite resides in `/usr/bin`.

**The Steps to Update Burp Suite:**

To update Burp Suite, go to Portswiggers website: [http://www.portswigger.net/burp/download.html](http://www.portswigger.net/burp/download.html)

- Download the latest .jar file into your Downloads folder
- Navigate to `/usr/bin` and select burpsuite
- Rename *burpsuite* to *burpsuite.old*
- Copy the jar that was just downloaded into /usr/bin
- Right-click and rename the jar to *burpsuite*
- In the *Permissions* tab, select *Allow executing file as program*
- Click *close*

Launch Burp Suite again and you’ll see that you won’t be alerted that there is a new update available. You’ll now be running the latest version. Upon successful launch, you can delete burpsuite.old from /usr/bin directory.
