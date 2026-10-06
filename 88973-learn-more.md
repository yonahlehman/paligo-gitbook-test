# learn-more

The `learn-more` command retrieves additional descriptions from the CLI for SAST vulnerabilities.


The command must be run with the attribute `query-id`, which can be retrieved from a scan’s results and passed to this command.


## Usage
```
./cx utils learn-more --query-id <query-id> --format [json|table|list]
```


## Flags
**`--query-id` Required**

The SAST query-id for a vulnerability.

**`--format` Default: list**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the learn-more command.


## Examples
### learn-more command
### Default (without format flag)
```
./cx utils learn-more --query-id 5854466950125120303
QueryID                : 5854466950125120303
QueryName              : Open_Redirect
QueryDescriptionID     : Stored_Open_Redirect
ResultDescription      : The potentially tainted value provided by @SourceElement in @SourceFile at line @SourceLine is used as a desti
nation URL by @DestinationElement in @DestinationFile at line @DestinationLine, potentially allowing attackers to perform an open redirection.


Risk                   : An attacker could use social engineering to get a victim to click a link to the application, so that the user 
will be immediately redirected to another site of the attacker's choice. An attacker can then craft a destination website to fool the v
ictim; for example - they may craft a phishing website with an identical looking UI as the previous website's login page, and with a si
milar looking URL, convincing the user to submit their access credentials in the attacker's website. Another example would be a phishing website with an identical UI as that of a popular payment service, convincing the user to submit their payment information.


Cause                  : The application redirects the user’s browser to a URL provided by a tainted input, without first ensuring that
 URL leads to a trusted destination, and without warning users that they are being redirected outside of the current site. An attacker 
could use social engineering to get a victim to click a link to the application with a parameter defining another site to which the app
lication will redirect the user’s browser. Since the user may not be aware of the redirection, they may be under the misconception that the website they are currently browsing can be trusted.


GeneralRecommendations :
1.  Ideally, do not allow arbitrary URLs for redirection. Instead, create a mapping from user-provided parameter values to legitimate URLs.
2.  If it is necessary to allow arbitrary URLs:
    *   For URLs inside the application site, first filter and encode the user-provided parameter, and then either:
        *   Create a white-list of allowed URLs inside the application
        *   Use variables as a relative URL as an absolute one, by prefixing it with the application site domain - this will ensure all redirection will occur inside the domain
    *   For URLs outside the application (if necessary), either:
        *   White-list redirection to allowed external domains by first filtering URLs with trusted prefixes. Prefixes must be tested u
p to the third slash \[/\] - `scheme://my.trusted.domain.com/,` to prevent evasion. For example, if the third slash \[/\] is not valida
ted and scheme://my.trusted.domain.com is trusted, the URL scheme://my.trusted.domain.com.evildomain.com would be valid under this filter, but the domain actually being browsed is evildomain.com, not domain.com.
        *   For fully dynamic open redirection, use an intermediate disclaimer page to provide users with a clear warning that they are leaving the site.


Samples                : [{Java protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String redirectUrl = request.getParameter("redirectUrl");
    if (redirectUrl != null) {
        response.sendRedirect(redirectUrl);
    } else {
          response.sendRedirect("/");
    }
} Java Servlet Vulnerable to Open Redirection} {Java protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String redirectUrl = request.getParameter("redirectUrl");
    if (redirectUrl != null && redirectUrl.startsWith("https://www.trusteddomain.com/")) {
        response.sendRedirect(redirectUrl);
    } else {
          response.sendRedirect("/");
    }
} Whitelisting an Allowed External Domain, Preventing Open Redirection}]
```

### Json format
```
./cx utils learn-more --query-id 5854466950125120303 --format json
[{"queryId":"5854466950125120303","queryName":"Open_Redirect","queryDescriptionId":"Stored_Open_Redirect","resultDescription":"The pote
ntially tainted value provided by @SourceElement in @SourceFile at line @SourceLine is used as a destination URL by @DestinationElement
 in @DestinationFile at line @DestinationLine, potentially allowing attackers to perform an open redirection.\n\n","risk":"An attacker 
could use social engineering to get a victim to click a link to the application, so that the user will be immediately redirected to ano
ther site of the attacker's choice. An attacker can then craft a destination website to fool the victim; for example - they may craft a
 phishing website with an identical looking UI as the previous website's login page, and with a similar looking URL, convincing the use
r to submit their access credentials in the attacker's website. Another example would be a phishing website with an identical UI as tha
t of a popular payment service, convincing the user to submit their payment information.\n\n","cause":"The application redirects the us
er’s browser to a URL provided by a tainted input, without first ensuring that URL leads to a trusted destination, and without warning 
users that they are being redirected outside of the current site. An attacker could use social engineering to get a victim to click a l
ink to the application with a parameter defining another site to which the application will redirect the user’s browser. Since the user
 may not be aware of the redirection, they may be under the misconception that the website they are currently browsing can be trusted.\
n\n","generalRecommendations":"\r\n1.  Ideally, do not allow arbitrary URLs for redirection. Instead, create a mapping from user-provid
ed parameter values to legitimate URLs.\r\n2.  If it is necessary to allow arbitrary URLs:\r\n    *   For URLs inside the application s
ite, first filter and encode the user-provided parameter, and then either:\r\n        *   Create a white-list of allowed URLs inside th
e application\r\n        *   Use variables as a relative URL as an absolute one, by prefixing it with the application site domain - thi
s will ensure all redirection will occur inside the domain\r\n    *   For URLs outside the application (if necessary), either:\r\n     
   *   White-list redirection to allowed external domains by first filtering URLs with trusted prefixes. Prefixes must be tested up to 
the third slash \\[/\\] - `scheme://my.trusted.domain.com/,` to prevent evasion. For example, if the third slash \\[/\\] is not validat
ed and scheme://my.trusted.domain.com is trusted, the URL scheme://my.trusted.domain.com.evildomain.com would be valid under this filte
r, but the domain actually being browsed is evildomain.com, not domain.com.\r\n        *   For fully dynamic open redirection, use an i
ntermediate disclaimer page to provide users with a clear warning that they are leaving the site.\r\n\n\n","samples":[{"progLanguage":"
Java","code":"protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {\n  
  String redirectUrl = request.getParameter(\"redirectUrl\");\n    if (redirectUrl != null) {\n        response.sendRedirect(redirectUr
l);\n    } else {\n          response.sendRedirect(\"/\");\n    }\n}","title":"Java Servlet Vulnerable to Open Redirection"},{"progLang
uage":"Java","code":"protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOExceptio
n {\n    String redirectUrl = request.getParameter(\"redirectUrl\");\n    if (redirectUrl != null \u0026\u0026 redirectUrl.startsWith(\
"https://www.trusteddomain.com/\")) {\n        response.sendRedirect(redirectUrl);\n    } else {\n          response.sendRedirect(\"/\");\n    }\n}","title":"Whitelisting an Allowed External Domain, Preventing Open Redirection"}]}]
```

