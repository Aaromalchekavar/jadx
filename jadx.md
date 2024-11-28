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



