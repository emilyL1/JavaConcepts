# Security

## Basic Concepts
### three ways
- Authentication
    - the act of validating that users are whom they claim to be
    - user + pwd
    - token
    - 403 
- Authorization
    - the process of giving the user permission to access a specific resource or function. 
    - access
    - role
    - 401
- Prevent Attacks
    - CSRF
        - Cross-Site Request Forgery (CSRF) is an attack that forces authenticated users to submit a request to a Web application against which they are currently authenticated. CSRF attacks exploit the trust a Web application has in an authenticated user
        - Conversely, cross-site scripting (XSS) attacks exploit the trust a user has in a particular Web application
    - SQL Injection

### how to secure

#### Encryption

- Symmetric
    - uses a single key that needs to be shared among the people 
- Asymmetric
    -  uses a pair of public key and a private key to encrypt and decrypt
    -  A public key is made freely available to anyone who might want to send you a message. The second private key is kept a secret so that you can only know.
    -  A message that is encrypted using a public key can only be decrypted using a private key, while also, a message encrypted using a private key can be decrypted using a public key. 
- TLS
    - TLS is an encryption protocol designed to secure Internet communications. A TLS handshake is the process that kicks off a communication session that uses TLS encryption. 
    - During a TLS handshake, the two communicating sides exchange messages to acknowledge each other, verify each other, establish the encryption algorithms they will use, and agree on session keys. 
    - TLS [handshakes](https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/) are a foundational part of how HTTPS works.
#### Encode
- URLEncode
    - replaces non-ASCII characters with a "%" followed by hexadecimal digits.
- FileEncode
    - Base64
    - Covert Binary to String
#### Hash
- Keep the integrity of the file
    ```
    Signature
               MD5/SHA                Encription
      [file]  ------>  [128bit digits] ------>
      
    ```

## JWT tokens
- JSON Web Tokens 
- an encoded JSON data used for data exchange between client and server 
    - dosen't hide the information
    - use signature to maintain the integrity
- advatage： It carries data
- three parts:
    - Header
    - Payload
        - claims: expiration date, issuer, and other customized data.
    - Signature
        - used for verification
```
               Base64                
      [Json]  ------>  [String]
      
```
- Generate a token
 ```
JwtBuilder builder = Jwts.builder().setId(id)
            .setIssuedAt(now)
            .setSubject(subject)
            .setIssuer(issuer)
            .signWith(signatureAlgorithm, signingKey).compact();
```
- Decode a token
```
Claims claims = Jwts.parser()
            .setSigningKey(DatatypeConverter.parseBase64Binary(SECRET_KEY))
            .parseClaimsJws(jwt).getBody();
```

## Oauth 2.0
- Open Authorization 2.0
- It is a way to let users log in to a website/application using the 3rd party account
- Users don't have to share the credentials with the application
- token based, Two types of token
    - Access Token
    - Refresh Token

```
              --(4)with token->                  
      [User]  ----(1) req--> [Web]
    ^|                       
    ||                       
    |-------(2) pwd------> [Google]
    |-------(3) token------


```
- ![](https://help.bizagi.com/bpm-suite/en/security_8.png)

## Spring Security
- A customizable authentication and authorization framework used by spring applications.
- It provides integrations with popular Authentication and Authorization methods such as oauth, sso, ldap, database, http basic authentication.
- Support declarative configuration of access control using configuration class or annotations.
- [how to configure Resource Server](https://github.com/spring-projects/spring-security/wiki/OAuth-2.0-Migration-Guide)

