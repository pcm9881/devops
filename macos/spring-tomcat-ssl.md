# spring tomcat ssl 적용

## Environment
1. Spring Framework
1. Tomcat
1. keytool
1. Java JDK 8 (1.8.0_152)

## purpose
Facebook Login 개발환경을 구성하기 위해 localhost에 SSL을 적용.

## Contents

1. Generate Keystroe 
1. Updating Connector in server.xml
1. Checking Browser


### Generate Keystroe

``` sh
$ keytool -genkey -alias tomcat -keyalg RSA
```

``` sh
What is your first and last name? 
    [Unknown]: localhost 
What is the name of your organizational unit? 
    [Unknown]: 
What is the name of your organization? 
    [Unknown]: 
What is the name of your City or Locality? 
    [Unknown]: 
What is the name of your State or Province? 
    [Unknown]: 
What is the two-letter country code for this unit? 
    [Unknown]: 
Is CN=localhost, OU=Unknown, O=Unknown, L=Unknown, ST=Unknown, C=Unknown correct? 
    [no]: yes 

Enter key password for <tomcat> 
    (RETURN if same as keystore password):
```

### Updating Connector in server.xml

- AS-IS

```
<!--
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
           maxThreads="150" scheme="https" secure="true"
           clientAuth="false" sslProtocol="TLS" />
-->
```

- TO-BE
change `#{content}#`

```
<Connector SSLEnabled="true" acceptCount="100" clientAuth="false"
    disableUploadTimeout="true" enableLookups="false" maxThreads="25"
    port="8443" keystoreFile="#keystroePath#" keystorePass="#keystroePassword#"
    protocol="org.apache.coyote.http11.Http11NioProtocol" scheme="https"
    secure="true" sslProtocol="TLS" />
```

### Checking Browser
[https://localhost:8443](https://localhost:8443)


## REPERANCE
[https://howtodoinjava.com/tomcat/how-to-configure-tomcat-with-ssl-or-https/](https://howtodoinjava.com/tomcat/how-to-configure-tomcat-with-ssl-or-https/)