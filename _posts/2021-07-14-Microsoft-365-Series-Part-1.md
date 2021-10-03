# Microsoft 365 Series - Part 1

## **Office 365 attacks**

*14/07/2021 | Zak Clifford | Security Consultant/Penetration Tester @ Cognisys*

### Zak's Top 5 Recommendations for Office 365 Security

1. Ensure mailbox audit logging is enabled on all accounts (where possible)
    
    The good ole saying "you can't secure what you can't see" applies here. Enabling audit logging is a helpful way to troubleshoot issues and acts as a starting point for incident response or to look for indicators of compromise (IOCs).
    
    Microsoft provides a script that enables non-owner mailbox access auditing on every mailbox in your organisation's tenancy. The script is available [here](https://raw.githubusercontent.com/OfficeDev/O365-InvestigationTooling/04b71798f8a398e627fd31c1613d46461dd50de7/EnableMailboxAuditing.ps1)
    
    To validate that all users have mailbox auditing enabled, run the following PowerShell commands
    
    ```powershell
    $Credentials = Get-Credential
    
    $O365Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $Credentials -Authentication Basic -AllowRedirection
    
    Import-PSSession $O365Session
    
    Get-Mailbox -ResultSize Unlimited | Select Name, AuditEnabled, AuditLogAgeLimit | Out-Gridview
    ```
    

![PowerShell.png](https://github.com/ZSECURE/zsecure-blog/blob/gh-pages/_images/1/PowerShell.png)

[Enable Mailbox Auditing in Office 365 Users using PowerShell](https://o365reports.com/2020/01/21/enable-mailbox-auditing-in-office-365-powershell/)

2.   Enable multi-factor authentication (MFA) or two-factor authentication (2FA)

Enabling MFA is a good way to layer your defences against brute force attacks. Not only does the threat actor need to guess or know your password, but they need to have access to your second factor; this can be by a more secure authenticator application or the least secure option of SMS. The SMS option for 2FA is considered less secure as there are known methods to carry out Mobile number transfers or even via the mobile service operator customer portal. 

1. Go to the admin centre at [https://admin.microsoft.com](https://admin.microsoft.com/).
2. Select **Show All**, then choose the **Azure Active Directory Admin Center**.
3. Select **Azure Active Directory**, **Properties**, **Manage Security defaults**.
4. Under **Enable Security defaults**, select **Yes** and then **Save**.
5. Next time the selected employees sign in, they'll be asked to set up the Microsoft Authenticator app on their phones for a second form of authentication.

Note: For new subscriptions purchased after October 21, 2019, Secure defaults are turned on automatically.

[Turn on multifactor authentication](https://docs.microsoft.com/en-us/microsoft-365/business-video/turn-on-mfa?view=o365-worldwide)

3.   Disable Legacy Authentication protocols

Disabling legacy authentication is the first and foremost step in securing your M365 environment. This is a well-known way for threat actors to bypass security controls such as Multi-Factor Authentication (MFA or 2FA) and perform brute force attacks.

Use the following guide from Microsoft to block legacy authentication via [Conditional Access](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/block-legacy-authentication) 

Or using the below PowerShell commands

```powershell
$Credentials = Get-Credential

$O365Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $Credentials -Authentication Basic -AllowRedirection

Import-PSSession $O365Session

Get-CASMailbox -identity zak@zsecure.uk | fl Name,OwaEnabled,MapiEnabled,EwsEnabled,ActiveSyncEnabled,PopEnabled,ImapEnabled,smtpclientauthenticationdisabled

Name                             : zak
OWAEnabled                       : True
MAPIEnabled                      : True
EwsEnabled                       : True
ActiveSyncEnabled                : True
PopEnabled                       : True
ImapEnabled                      : True
SmtpClientAuthenticationDisabled : False

Get-CASMailbox -identity zak@zsecure.uk | fl Name,OwaEnabled,MapiEnabled,EwsEnabled,ActiveSyncEnabled,PopEnabled,ImapEnabled,smtpclientauthenticationdisabled

Name                             : zak
OWAEnabled                       : True
MAPIEnabled                      : True
EwsEnabled                       : True
ActiveSyncEnabled                : True
PopEnabled                       : False
ImapEnabled                      : False
SmtpClientAuthenticationDisabled : True
```

Use the following PowerShell to confirm disablement

```powershell

$Credentials = Get-Credential

$O365Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $Credentials -Authentication Basic -AllowRedirection

Import-PSSession $O365Session

Get-CASMailbox  | Select  Name,OwaEnabled,MapiEnabled,EwsEnabled,ActiveSyncEnabled,PopEnabled,ImapEnabled,smtpclientauthenticationdisabled | Out-GridView
```

![_images/1/PowerShell2.png](_images/1/PowerShell2.png)

[Three ways to disable basic authentication and legacy protocols in Exchange Online](https://www.itpromentor.com/block-basic-auth/)

4.   Enable Azure AD Password Protection.

Having a strong password policy is key to securing your M365 tenancy; this is the password that secures your email, documents and even teams conversations. Ensure that you are either using a password manager or a minimum 20 character password with a mixture of upper and lowercase characters, numbers and special characters. Consider using [xkpasswd.net/s/](http://xkpasswd.net/s/) for inspiration. It's easier to remember a password that's a combination of multiple words with a sequence of special characters e.g. 

```
__92_column_AGAIN_best_11__
```

Ensuring you have enabled the account lockout policy in Azure/On-premise AD is the best way to mitigate brute force attacks internally on your network and your M365 account. Azure AD password protection not only allows you to enable password lockout, complexity and a custom list of banned passwords, it also allows you to apply the same controls on your on-premise AD.  

You can enable this feature prevailing you have the license for it, following these steps

1. [https://portal.azure.com](https://portal.azure.com) 
2. Azure Active Directory 
3. Security
4. Authentication methods 
5. Password protection

[Azure AD password protection](https://katystech.blog/2021/02/azure-ad-password-protection/)

5.    Restrict mail forwarding to external domains

And last but not least, we have the single most used and successful exploitation method for M365, and that's forwarding mail to external domains. This is a common way threat actors monitor your inbox without you knowing. A threat actor would often gain access to your emails, create a forwarding rule to their inbox and then waits for sensitive information to come into your inbox, i.e. a big payment due, transferring money or any other information they can get to further aid their attack. Often they will create either mailbox rules or set up auto-forwarding to their remote domain that they can control and monitor. Disabling this feature will reduce the exfiltration methods that a threat actor can use. 

You can prevent this by setting up a transport rule

To create a mail transport rule:

1. Go to the [Exchange admin centr](https://go.microsoft.com/fwlink/p/?linkid=2059104)e.
2. In the **mail flow** category, select **rules**.
3. Select **+**, and then **Create a new rule**.
4. Select **More options** at the bottom of the dialogue box to see the full set of options.
5. Apply the settings in the following table. Leave the rest of the settings at the default, unless you want to change these.
6. Select **Save**.

[Transport Rule](https://www.notion.so/adac520852c046eab0514c03bcd521dc)

[FBI warns of email forwarding rules being abused in recent hacks | ZDNet](https://www.zdnet.com/article/fbi-warns-of-email-forwarding-rules-being-abused-in-recent-hacks/)

Here at [Cognisys](https://www.cognisys.co.uk), we offer M365 tenant reviews to advise you on your current security posture and make recommendations on further securing your tenancy. Please get in touch with our [Account Management team](https://cognisys.co.uk/) to discuss further.

Thanks for reading,

Zak

Twitter: [@zak_hax](https://twitter.com/zak_hax) 

LinkedIn: [zak-clifford](https://www.linkedin.com/in/zak-clifford/)
