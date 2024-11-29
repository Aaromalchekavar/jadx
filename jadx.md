keytool -genkeypair -alias mykey -keyalg RSA -keystore keystore.jks -storepass f123 -validity 365
jarsigner -keystore keystore.jks -storepass f123 -keypass f123 -signedjar maven_javaapp_signed.jar target/maven-java-app-1.0 mykey
jarsigner verify -keystore keystore.jks -storepass f123 -keypass -f123 maven_javaapp_signed.jar
 login -u 
 scout cves flask-img 
 build -t flask-app:2 <path> 
 scout cves flask-app:2 
 scout quickview flask-app:2 - optional just to validate 
 scout recommendations flask-app:2 - optional just to validate 
 scout cves --format sarif --output <path>/flask-app:2_cves.json 
 trust key generate admin-key --dir <path> 
 trust signer add admin-key fuser1234/<emid>:flask --key <path>/admin-key.pub 
 tag flask-app:2 fuser1234/<emid>:flask 
 trust sign fuser1234/<emid>:flask 
 push fuser1234/<emid>:flask 
 image pull fuser1234/<emid>:flask  
 compose.yml update the latest image
 compose up 

 1. **Single-quote-based injection**
   - This exploits improper handling of single quotes in SQL queries.
   - Example:
     ```
     Input: ' OR '1'='1
     Query: SELECT * FROM users WHERE username = '' OR '1'='1';
     Effect: Always evaluates to true, potentially returning all rows.
     ```



 2. **Comment-based injection**
   - This uses SQL comments to ignore the rest of the query.
   - Example:
     ```
     Input: ' OR '1'='1' -- 
     Query: SELECT * FROM users WHERE username = '' OR '1'='1' -- ' AND password = '';
     Effect: The condition after `--` is ignored.
     ```



 3. **Union-based injection**
   - This allows combining the results of another query with the original query.
   - Example:
     ```
     Input: ' UNION SELECT null, username, password FROM users --
     Query: SELECT id, name, email FROM customers WHERE id = '' UNION SELECT null, username, password FROM users --';
     Effect: Extracts data from the `users` table.
     ```



 4. **Boolean-based injection**
   - This manipulates conditional statements to infer information.
   - Example:
     ```
     Input: ' AND 1=1 --
     Query: SELECT * FROM users WHERE username = '' AND 1=1 --;
     Effect: Executes normally since `1=1` is always true.
     ```



 5. **Time-based injection**
   - This exploits SQL functions like `SLEEP()` to infer database behavior based on delays.
   - Example:
     ```
     Input: '; SLEEP(5); --
     Query: SELECT * FROM users WHERE username = ''; SLEEP(5); --;
     Effect: Causes a delay, indicating vulnerability.
     ```



 6. **Error-based injection**
   - This forces the application to return database errors for information.
   - Example:
     ```
     Input: ' AND 1=CONVERT(int, (SELECT @@version)) --
     Query: SELECT * FROM users WHERE username = '' AND 1=CONVERT(int, (SELECT @@version)) --;
     Effect: Reveals database version via error message.
     ```



 Preventing SQL Injection
To protect against these attacks:
1. **Use Prepared Statements/Parameterized Queries**:
   - Replace dynamic SQL with parameterized queries.
   - Example (PHP with PDO):
     ```php
     $stmt = $pdo->prepare('SELECT * FROM users WHERE username = :username');
     $stmt->execute(['username' => $input]);
     ```
   
// This should REALLY be validated too
String custname = request.getParameter("customerName");
// Perform input validation to detect attacks
String query = "SELECT account_balance FROM user_data WHERE user_name = ? ";
PreparedStatement pstmt = connection.prepareStatement( query );
pstmt.setString( 1, custname);
ResultSet results = pstmt.executeQuery( )

