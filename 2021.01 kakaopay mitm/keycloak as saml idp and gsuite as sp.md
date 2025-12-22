```
### 테스트환경
```

- ```
    g-suite
    ```
    
    ```
    도메인: magnon.page
    ```
    
    ```
    로그인 테스트 URL: [https://mail.google.com/a/magnon.page](https://mail.google.com/a/magnon.page)
    ```
    
- ```
    rh-sso
    ```
    
    ```
    URL: [http://rhsso.bliex.net](http://rhsso.bliex.net)
    ```
    
    ```
    realm: gsuite
    ```
    
      
            
```
### rh-sso client 설정
```
 
```
Client ID: google.com/a/magnon.page
```

```
Name: Google Apps
```

```
Enabled: \<on\>
```

```
Consent Required: \<off\>
```

```
Login Theme: \<Not Selected\>
```

```
Client Protocol: saml
```

```
Include AuthnStatement: \<on\>
```

```
Include OneTimeUse Condition: \<off\>
```

```
Sign Documents: \<on\>
```

```
Optimize REDIRECT signing key lookup: \<off\>
```

```
Sign Assertions: \<on\>
```

```
Signature Algorithm: RSA_SHA256
```

```
SAML Signature Key Name: KEY_ID
```

```
Canonicalization Method: EXCLUSIVE
```

```
Encrypt Assertions: \<off\>
```

```
Client Signature Required: \<off\>
```

```
Force POST Binding: \<on\>
```

```
Front Channel Logout: \<on\>
```

```
Force Name ID Format: \<on\>
```

```
Name ID Format: email
```

```
Root URL: \<blank\>
```

```
Valid Redirect URIs: [https://mail.google.com/*](https://mail.google.com/*)
```

```
Base URL: /auth/realms/gsuite/protocol/saml/clients/googleapps?RelayState=true
```

```
Master SAML Processing URL: \<blank\>
```

```
IDP Initiated SSO URL Name: googleapps
```

```
IDP Initiated SSO Relay State: \<blank\>
```
 
- ```
    Fine Grain SAML Endpoint Configuration
    ```
    
    ```
    Assertion Consumer Service POST Binding URL: [https://www.google.com/a/magnon.page/acs](https://www.google.com/a/magnon.page/acs)
    ```
    
    ```
    Assertion Consumer Service Redirect Binding URL: \<blank\>
    ```
    
    ```
    Logout Service POST Binding URL: \<blank\>
    ```
    
    ```
    ogout Service Redirect Binding URL: \<blank\>
    ```
      
```
### export한 client 정보￼
```
 
```
{  
    "clientId": "google.com/a/magnon.page",  
    "name": "Google Apps",  
    "baseUrl": "/auth/realms/gsuite/protocol/saml/clients/googleapps?RelayState=true",  
    "surrogateAuthRequired": false,  
    "enabled": true,  
    "alwaysDisplayInConsole": false,  
    "clientAuthenticatorType": "client-secret",  
    "redirectUris": [  
        "[https://mail.google.com/*](https://mail.google.com/*)"  
    ],  
    "webOrigins": [],  
    "notBefore": 0,  
    "bearerOnly": false,  
    "consentRequired": false,  
    "standardFlowEnabled": true,  
    "implicitFlowEnabled": false,  
    "directAccessGrantsEnabled": false,  
    "serviceAccountsEnabled": false,  
    "publicClient": false,  
    "frontchannelLogout": true,  
    "protocol": "saml",  
    "attributes": {  
        "saml.assertion.signature": "true",  
        "saml_assertion_consumer_url_redirect": "",  
        "saml.force.post.binding": "true",  
        "saml.multivalued.roles": "false",  
        "saml_single_logout_service_url_post": "",  
        "saml.encrypt": "false",  
        "saml_assertion_consumer_url_post": "[https://www.google.com/a/magnon.page/acs](https://www.google.com/a/magnon.page/acs)",  
        "saml.server.signature": "true",  
        "saml_idp_initiated_sso_url_name": "googleapps",  
        "saml.server.signature.keyinfo.ext": "false",  
        "exclude.session.state.from.auth.response": "false",  
        "saml.signing.certificate": "MIICvzCCAacCBgF2jre+ZjANBgkqhkiG9w0BAQsFADAjMSEwHwYDVQQDDBhnb29nbGUuY29tL2EvbWFnbm9uLnBhZ2UwHhcNMjAxMjIzMDgyNzU1WhcNMzAxMjIzMDgyOTM1WjAjMSEwHwYDVQQDDBhnb29nbGUuY29tL2EvbWFnbm9uLnBhZ2UwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCcqwlW3zcH+dD38yzypenvH9JDO8N2HSjSSReKdVCMBGfuBpnUyU/DyM5WMOo3LMA7m6zErr+hZsVe5F9Jj2Hz3C7RKpoU0Z68ib2pAC/g5TbOy+1TdtnXjDSMZUuOhHIyuG4G4YKtVcIEEMg2i0SoGXEPzRttGJVo38c547IvP91MInEW0vz3xgxjAEB73sxsR0uci8BqzvxZbMp6w2hsObPi423SD4GPpAb6ipS1ikaBKYvHWP8Awyk235xa5rjjZsACWKQRf6r6hXPFyefJ7Bz8xyeU0PANqI2+92V5A3ezmTfVpFX80o2or4U9MF4PxlhhZhnJ9i+5p+Nbv2d9AgMBAAEwDQYJKoZIhvcNAQELBQADggEBADzu7PBP7i+2h6JPN0kS1WTgS7U4s1fRWtUH9kSv3BiS97FGjLqj5RGs28lpcXjKVyC2ZJmZrwUbkQWaWetl4n4RWNnurfHuwwzyt81KyEHPO9m4CL2IkbT2ps+Y1I2CBIoj+kp3Qyi9sE4MC5l63iJbbL8YlNBWT2zs4H6cjJ1qxN0TdZ4guALHc+LOiKA5u+0Qlm41SenP869Yq505gAmSYELRtDdAuG+BXDifJDTvyaU6SeST6Cwd2QcDg8Ec/2F8brqT95uWXEMJLIcGExwG1xRvLH/pq0Z6hF6CIZnEKxBG7aarJlzQX4rapb1ZTM+bAZGsYKuSaJk/d8G6hzs=",  
        "saml_single_logout_service_url_redirect": "",  
        "saml.signature.algorithm": "RSA_SHA256",  
        "saml_force_name_id_format": "true",  
        "tls.client.certificate.bound.access.tokens": "false",  
        "saml.client.signature": "false",  
        "saml.authnstatement": "true",  
        "display.on.consent.screen": "false",  
        "saml.signing.private.key": "MIIEpAIBAAKCAQEAnKsJVt83B/nQ9/Ms8qXp7x/SQzvDdh0o0kkXinVQjARn7gaZ1MlPw8jOVjDqNyzAO5usxK6/oWbFXuRfSY9h89wu0SqaFNGevIm9qQAv4OU2zsvtU3bZ14w0jGVLjoRyMrhuBuGCrVXCBBDINotEqBlxD80bbRiVaN/HOeOyLz/dTCJxFtL898YMYwBAe97MbEdLnIvAas78WWzKesNobDmz4uNt0g+Bj6QG+oqUtYpGgSmLx1j/AMMpNt+cWua442bAAlikEX+q+oVzxcnnyewc/McnlNDwDaiNvvdleQN3s5k31aRV/NKNqK+FPTBeD8ZYYWYZyfYvuafjW79nfQIDAQABAoIBAHH7mjrjAcXCwn9zI/OSNIXuT+rsk0Pe6TE9TmxE+Ao2tmqd0NPYdzkJYt2gjvb/jwiPNX6PaQqDm/tzCcSaFfj26/TwGtQkwmmHiT5ozWzBN0PzaEJ+SPWioyS2GeehgvhV6G8HKSz1JMgScagFYTkv8Ws+ncKczS9VCDyc5amrl7JWjg3bmyG9MhlQFe6XU1zv3R90O5acMpJxLhPPmy8Ntc2AfIqWt2DTLSmwD8Mi5PGZp9XTcHa9jit66hxTApughIUfj1R+Fqhry+36nBXMaZ50GTaKiFTeO5v0WzfuiWSY+nCKVOroTPuwIcXVK78iCrtF3wyQrVlGYZxW4Z0CgYEA23wnu6HdVycCvjs5UJJOMxfNpL5iG41IPfnzvBUtmris0x3hJBBNX4OXixaOCAcZIIV64xs/oP/iTXQmE3sEdEIXjHBljSGxOWRLQfaXS1zPpqP6NqGqR/BxmmuSLu/R2C9dRAq+L8lbyuP/Bl38JKsc2S+QMrQI6c/NQHkqROcCgYEAtruERChfVNqwPwR0D0pmJXnZArVfUryCD5YrGcjYBmUGDrSqArKSyKkqJdeT2JDl7IxR/4IUZ5jOJd0UrmcV81m9X3KYFnVoICWZW8T44g9l0SB8iWDJo6JbmilZzY3UIBZuM2LB6UnMPzH/ILG2b5Cf7hRJYLJlw9awKEC/P/sCgYEAhlssH2noio8w2K58WVwWTqSFmBGLEP6deILntvzn28ysztd9mIv6MTvmqpf1/egKc6QCI7/sZWv+Zhdxr38grOJAdBHhuFElodJJV2nSF6oK2yGJ66NvD3aatEKhS+Y2eLYVy68f2TTT4hFLbeRekzvD/xdkmAUpZ6dzJ8KEI4UCgYBw5fw7TCJSP+dCmBLI27OuldDRTpP9f0BwNtycSq3FjacncNHVZtUvquzCgqXy2NtlwfBrh8fplcxQMn6znjc+qgRJs3hp79IMgo5014bZzJ+gjIzFKAqM0iP8ZG36hRU5WgJuNycNZq4NoWs6nPHVjipxoxEO8EnVrJAb3p0K/wKBgQCa6J3hW3Sbz8MYldeFkPOfSVovUDLPLXXpi/sIzmTMwj7kCwMygC/49K2SYE9ZvbUffqhlLfy5+UQOXDwKLxhFpbjf4JxsSsrzLFa/ZXhRvYI6H5cNzIy5M7kCyMG3deRt+piiAGXdAnkgcJ4DDvCi7o9Bg4MEh2hoNnxrS22FKg==",  
        "saml_name_id_format": "email",  
        "saml_signature_canonicalization_method": "[http://www.w3.org/2001/10/xml-exc-c14n#](http://www.w3.org/2001/10/xml-exc-c14n#)",  
        "saml.onetimeuse.condition": "false"  
    },  
    "authenticationFlowBindingOverrides": {},  
    "fullScopeAllowed": true,  
    "nodeReRegistrationTimeout": -1,  
    "protocolMappers": [  
        {  
            "name": "email",  
            "protocol": "saml",  
            "protocolMapper": "saml-user-property-mapper",  
            "consentRequired": false,  
            "config": {  
                "attribute.nameformat": "Basic",  
                "user.attribute": "email",  
                "friendly.name": "Email",  
                "attribute.name": "emailAddress"  
            }  
        }  
    ],  
    "defaultClientScopes": [  
        "web-origins",  
        "role_list",  
        "profile",  
        "roles",  
        "email"  
    ],  
    "optionalClientScopes": [  
        "address",  
        "phone",  
        "offline_access",  
        "microprofile-jwt"  
    ],  
    "access": {  
        "view": true,  
        "configure": true,  
        "manage": true  
    }  
}
```
 
```
### rhsso SAML 연동용 인증서 (공개키) 확인
```

```
Realm Settings --\> General 탭 --\> Endpoints --\> SAML 2.0 Identity Provider Metadata 링크 클릭
```

```
\<dsig:X509Certificate\> 노드의 값 확인
```

```
-----BEGIN CERTIFICATE-----￼\<\<\<확인한 값을 64바이트씩 끊어서 word-wrap\>\>\>￼-----END CERTIFICATE-----
```
      

```
### g suite admin 설정
```
 
```
보안 --\> 타사 IdP를 사용해 싱글 사인온(SSO) 설정
```
 
```
'타사 ID 제공업체에 SSO 설정' 에 체크
```

```
로그인 페이지 URL: [http://rhsso.bliex.net/auth/realms/gsuite/protocol/saml/clients/googleapps](http://rhsso.bliex.net/auth/realms/gsuite/protocol/saml/clients/googleapps)
```

```
로그아웃 페이지 URL: [http://rhsso.bliex.net/auth/realms/gsuite/protocol/openid-connect/logout?redirect_uri=https%3A%2F%2Fmail.google.com%2Fa%2Fmagnon.page](http://rhsso.bliex.net/auth/realms/gsuite/protocol/openid-connect/logout?redirect_uri=https%3A%2F%2Fmail.google.com%2Fa%2Fmagnon.page)
```

```
확인 인증서: saml 인증서 업로드
```

```
'도메인별 발행자 사용'에 체크
```
 
![RED HAT SINGLE SIGNON Gsuite Co nfigure Realm Sett...](Exported%20image%2020251106120201-0.png) ![P SS AS 0 0 SSO ID 6009k Of LIRL httprhssobliexnet...](Exported%20image%2020251106120202-1.png)