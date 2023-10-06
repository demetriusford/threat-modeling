### Part I. (Questions)

**Q**: Where can the payload come from?  
**A**: A web request that's sent from either the mobile or the web client

**Q**: Where can the payload execute?  
**A**: The code can execute through the web client, or the mobile client

**Q**: Which component likely houses the code that needs remediation?  
**A**: The reviews service, as this is where the application code resides

**Q**: What considerations do you need to present to your management regarding this approach?  
**A**: Understand the injection context, first; this will determine the sanitization strategy (e.g., in between a HTML tag, inside of an HTML attribute, JavaScript, CSS, or in a URL). Prioritize remediating at the application level as the WAF acts as a secondary defense. Having a core development team that can mitigate ongoing security vulnerabilities will always be more cost effective than incurring additional costs for WAF services. Upon implementation, consider the following:

- Only allow access from your vendor's firewall by configuring a `.htaccess` file
- DNS records should not point to the server's origin IP without it being proxied
- Stream WAF firewall events to your SIEM solution for visibility and monitoring
- If using a shared hosting model, ensure emails are proxied through an external mailing solution (e.g., Office 365, G Suite)
- Decommission all unmaintained servers (this could potentially leak the service's infrastructure)

**Q**: Does the WAF mitigate the XSS risk to any degree?  
**A**: A WAF can mitigate against *some* XSS injections. It's particularly effective against catching stored and reflective XSS. However, a stored DOM-based XSS would never receive the input from the browser, rendering server-side filters useless. Likewise, many 0-day [disclosures](https://github.com/waf-bypass-maker/waf-community-bypasses/blob/main/payloads.twitter.csv) are made publicly available for security professionals 

**Q**: What other activities do you think may need to occur here?  
**A**: WAFs are a compensating control that need to be fine tuned to ensure they work effectively. With this in mind, here are some key recommendations:

- Check if HTML escaping has been disabled in the web application's framework
- Check the source code for any variables that might be marked as "safe"
- Sanitize input at the application and API level. Specifically, variables that can be controlled by the client (e.g., query strings, POST data, HTTP headers, and cookies)
- Enforce a strict content-security policy to allow/block specific scripts 
- Enforce content types for each request
- Configure the HTTP header `X-Content-Type-Options` with `nosniff` to stop the browser from automatically detecting content types

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Part II. (Diagram)

![](./assets/dfd.png)
