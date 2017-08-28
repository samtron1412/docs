# Injection flaws
Injection flaws allow attackers to relay malicious code through a web application to another system. These attacks include calls to the operating system via system calls, the use external programs via shell commands, as well as call to backend databases via SQL.

The best way to determine if you are vulnerable to command injection attacks is to search the source code for all calls to external resources (e.g., system, exec, fork, Runtime.exec, SQL queries, or whatever the syntax is for making requests to interpreters in your environment)

# SQL injection
## Define
Untrusted data is sent to an interpreter as part of a command or query. Trick the the interpreter into executing unintended commands or accessing data without authorization.

## [Prevent](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet)
[stackoverflow](https://stackoverflow.com/questions/60174/how-can-i-prevent-sql-injection-in-php).

Never trust any kind of input, especially it comes from the client side, even though it comes from a select box, a hidden input or a cookie.
- Never connect to the database as a superuser or as the database owner. Use always users with very limits privileges.
- Parameterized API
	+ PHP: provided by [PDO](http://php.net/manual/en/pdo.prepared-statements.php), [MySQLi](http://php.net/manual/en/mysqli.quickstart.prepared-statements.php)
	+ Java:

		public insertUser(String name, String email) {
		   Connection conn = null;
		   PreparedStatement stmt = null;
		   try {
		      conn = setupTheDatabaseConnectionSomehow();
		      stmt = conn.prepareStatement("INSERT INTO person (name, email) values (?, ?)");
		      stmt.setString(1, name);
		      stmt.setString(2, email);
		      stmt.executeUpdate();
		   }
		   finally {
		      try {
		         if (stmt != null) { stmt.close(); }
		      }
		      catch (Exception e) {
		         // log this error
		      }
		      try {
		         if (conn != null) { conn.close(); }
		      }
		      catch (Exception e) {
		         // log this error
		      }
		   }
		}
- Escape special characters
- White list input validation

# XSS
## Define
An application takes untrusted data from attackers and sends it to a web browser without proper validation or escaping. XSS allows attackers to execute scripts in the victim's browser which can hijack user sessions, deface website, or redirect the user to malicious sites.

Search Google for example of XSS attack. Have three type of XSS: non-persistent(reflected), persistent(stored) and DOM-based

## Prevent
1. The preferred option is to properly escape all untrusted data based on the HTML context (body, attribute, JavaScript, CSS, or URL) that the data will be placed into. See the [OWASP XSS Prevention Cheat Sheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) for details on the required data escaping techniques.
2. Positive or "white-list" input validation is also recommended as it helps protect against XSS, but is not a complete defense as many applications require special characters in their input. Such validation should, as much as possible, validate the length, characters, format, and business rules on that data before accepting the input.
3. For rich content, consider auto-sanitization libraries like OWASP’s [AntiSamy](https://www.owasp.org/index.php/AntiSamy) or the [Java HTML Sanitizer Project](https://www.owasp.org/index.php/OWASP_Java_HTML_Sanitizer_Project).
4. Consider [Content Security Policy](https://www.owasp.org/index.php/Content_Security_Policy) (CSP) to defend against XSS across your entire site.

# CSRF
## Define
A CSRF attack forces a logged-on victim’s browser to send a forged HTTP request, including the victim’s session cookie and any other automatically included authentication information, to a vulnerable web application. This allows the attacker to force the victim’s browser to generate requests the vulnerable application thinks are legitimate requests from the victim.

## Prevent
1. The preferred option is to include the unique token in a hidden field. This causes the value to be sent in the body of the HTTP request, avoiding its inclusion in the URL, which is more prone to exposure.
2. Requiring the user to re-authenticate, or prove they are a user (e.g., via a CAPTCHA) can also protect against CSRF.
