**Q**: Where can the payload come from?  
**A**: A web request that's sent from either the mobile or the web client


**Q**: Where can the payload execute?  
**A**: The code can execute through the web client, or the mobile client

**Q**: Which component likely houses the code that needs remediation?  
**A**: The Reviews Service, as this is where the application code resides

**Q**: What considerations do you need to present to your management regarding this approach?  
**A**: Understanding the injection context, first; this will determine the sanitization strategy (e.g., in between a HTML tag, inside of an HTML attribute, JavaScript, CSS, or in a URL). Remediate at the application level as the WAF acts as a secondary defense. Having a core development team that can mitigate ongoing security vulnerabilities will always be more cost effective than paying for WAF services. Upon implementation, consider the following:

- Only allow access from your vendor's firewall by configuring a `.htaccess` file
- DNS records should not point to the server's origin IP without it being proxied
- Stream WAF firewall events to your SIEM solution for visibility and monitoring
- If using a shared hosting model, ensure emails are proxied through an external mailing solution (e.g., Office 365, G Suite)
- Decommission all unmaintained servers (this could potentially leak the service's infrastructure)

