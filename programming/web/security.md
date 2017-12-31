# Security

## XSS (Cross-Site Scripting)

웹사이트 관리자가 아닌 이가 웹 페이지에 악성 스크립트를 삽입할 수 있는 취약점. 해커가 사용자의 정보(쿠키, 세션 등)를 탈취하거나, 자동으로 비정상적인 기능을 수행하게 할 수 있다.

To prevent XSS, the common response is to escape and encode all untrusted data. But this is far from the full story. In 2015, modern web apps use JavaScript hosted on CDNs or outside infrastructure. Modern web apps include 3rd party JavaScript libraries for A/B testing, funnel/market analysis, and ads. We use package managers like Bower to import other peoples’ code into our apps.

What if only one of the scㄴㅁripts you use is compromised? Malicious JavaScript can be embedded on the page, and Web Storage is compromised. These types of XSS attacks can get everyone’s Web Storage that visits your site, without their knowledge. This is probably why a bunch of organizations advise not to store anything of value or trust any information in web storage. This includes session identifiers and tokens.

요즘은 Chrome extension 같은 것도 있으니 더 조심해야 하는게 아닌가 싶음


## CSRF(Cross-Site Request Forgery)

CSRF is an attack that tricks the victim into submitting a malicious request. It inherits the identity and privileges of the victim to perform an undesired function on the victim's behalf. For most sites, browser requests automatically include any credentials associated with the site, such as the user's session cookie, IP address, Windows domain credentials, and so forth. Therefore, if the user is currently authenticated to the site, the site will have no way to distinguish between the forged request sent by the victim and a legitimate request sent by the victim.

CSRF can be prevented by using synchronized token patterns. This sounds complicated, but all modern web frameworks have support for this.

CSRF can also be partially prevented by checking the HTTP Referer and Origin header from your API. CSRF attacks will have Referer and Origin headers that are unrelated to your application.


## Cookies Security

Cookies, when used with the `HttpOnly` cookie flag, are not accessible through JavaScript, and are immune to XSS. You can also set the `Secure` cookie flag to guarantee the cookie is only sent over HTTPS.

`SameSite` 쿠키는 서버로 하여금 쿠키가 cross-site 요청과 함께 전송되지 않았음을 단정케 하여, cross-site 요청 위조 공격(CSRF)에 대해 어떤 보호 방법을 제공합니다.


## Cookies vs LocalStorage

- Cookies: vulnerable to `CSRF`. 하지만 우리 웹 페이지가 털리지만 않는다면 어지간한건 다 막을 수 있음.
- LocalStorage: vulnerable to `XSS`. I think `CSRF` is also possible.


Reference:  
https://stormpath.com/blog/where-to-store-your-jwts-cookies-vs-html5-web-storage  
https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies  
https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)  
