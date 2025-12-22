- ```
    cpm-ui01
    ```
    
    ```
    Public IP: 183.111.127.48
    ```
    
    ```
    Private IP: 192.168.200.136
    ```
    
    ```
    4 core / 8GB / 100GB
    ```
    
    ```
    ID: ubuntu
    ```
     - ```
    cpm-api01
    ```
    
    ```
    Public IP: -
    ```
    
    ```
    Private IP: 192.168.200.70
    ```
    
    ```
    4 core / 8GB / 100GB
    ```
    
    ```
    ID: ubuntu
    ```
    
    ```
    비고 - cpm-ui01을 통해 접속 가능
    ```
    
      
    
- ```
    cpm-keycloak01
    ```
    
    ```
    Public IP: -
    ```
    
    ```
    Private IP: 192.168.200.67
    ```
    
    ```
    4 core / 8GB / 100GB
    ```
    
    ```
    ID: ubuntu
    ```
    
      
    
- ```
    cpm-mysql01
    ```
    
    ```
    Public IP: -
    ```
    
    ```
    Private IP: 192.168.201.68
    ```
    
    ```
    4 core / 8GB / 100GB
    ```
    
    ```
    ID: ubuntu
    ```
    
    ```
    비고 - cpm-api01을 통해 접속 가능
    ```
    
          
```
### rsa private key  
-----BEGIN RSA PRIVATE KEY-----  
MIIEpgIBAAKCAQEAxjdIM1MRvCQk5ly9DMOU+P/z2z4SPviScpboRDpCfNJd4lxn  
DpOrbHjCuFLK2AtHANxGYL1p8758c67h3ARBf2eD3naAaRSiDvvo6Ws7GbmJaXJB  
SRrAgyauumNHcm/V3FLJSfkCHdItTM3FUvrWiylRYfK5Xbz8yrNAozYQKEc3wFLn  
2oUozhLdu0plZVTw+/lsShtTDsCahiz3GePa8WD3qya/eJkavfkOCbhICYObVKi1  
7d11Wmggr2hK77gp35u3aN5aywfioik5ZuBcOYsXWX4x5hUES/M2yeTs5xh1nxkZ  
+kokrM908iKUvZUiAtxTpxsXOIPiAaj7SGHAdQIDAQABAoIBAQCZUs3QlaMUS0kX  
wAikRO2JJkN1BbCLcS+m38BOdlpTv03L+PnmtqdVQpwshC5Pq3mC2uC9mAbK+j++  
JDqlO82GRYYloLh3j/RDbuydEcsnfPMj07NYXw8m49coaf8sMAHXaVo2lBzlAFz2  
Gf1W0J0ADDfdcimcrsFD8iA/n2QkIoX6gOsbMJEfaduvAxQ5kRvCnPVsZcpCLqCu  
KzMOb/I4YQSlLrYLmCBovf8eRzEcXnjRpnJ3Q8ybgDUedaEtvjfVOKP4UeqIimbJ  
5/wlS0uE2vbULTrv18R9bdQ5B0sm1tBDlcSFeEs4QcUoqIRck9vhkKdgMLxypLEX  
kSyGCr4JAoGBAOimRGOeF6kUDl2JmvQvhelFh7KO8NJIbzM0PFL6yT4Svu4Pd9mg  
Z31dcVEnWLe3rUIT5eoaYdpB/iIFeiW/WJ2qdQrXXmhka6eskLAJEE/TIK72+1RW  
JoIrG9XvDn2evbYpR7p2wtLsyXoHO2/sJb+UoI7NuV1hmHPE6m5towQvAoGBANoc  
Ri24cevLdHth1l7qicTdCDE+114+WYy+99YJX8sN8cAM2EKuMqpFKF2xL4Wi4/J0  
2XB8HjvTzUht8ZS+nKnvKC7ceKaHWWIN3zRpE6mfhH9Ge+GBftfUSxA5Q2P9iQUJ  
LIsor85Wr/kbiP+QgJUImKmLirpblcaCI4mtT0ibAoGBALKuMExKOWXUT4wriWUN  
ss2MZ0IOYos+spki/0nD7xfLkfSI0MXGWnWAdO2dSJgha+IaIjUAejMFCEfc6Qlg  
wpClQCtJaerHZZ9r+9wXuf106981NaZ6XC0RKtnONtToPFBRuBNP7yXMUpl0QIQf  
XIadggrrmfhMYqhXjq2tasxlAoGBAJ3dtyHijXo4oY+oSewbYCpAPWy/akzJXjGU  
C3g9ArvK1P7HjUP+J6e8NLJTy+yy8MANuVBEVfHBpKTXBvM9X9FTy8bXRvBpqNVi  
6vpZT6UHU3R3xLR88R0wiEAu4kseOC2P7VCv20fC0M3CE0++/IJiXXTiDkBCh87N  
ZQGCko8fAoGBAN9VC3/TmbHINEcb7jHaa1fKKkibwPQNawo6mxwdQGAADkOXtl/O  
gZBRSOEJh1ceO+gHLZTgWbwW+ZFrvJ+hqVVr4kcFFrMweqsfl758e6VGxHFJYbiN  
IR9xvpWy8E+gpaErY8oFVcszcZctof+3T5DzdbdTImcFH4h7O1mw7S4q  
-----END RSA PRIVATE KEY-----
```

```
UI:  
- base url: [http://183.111.127.48](http://183.111.127.48)  
- config: [http://183.111.127.48/app/config](http://183.111.127.48/app/config)
```
 
```
api: [http://183.111.127.48/api](http://183.111.127.48/api)
```
 
```
keycloak  
- master: [http://183.111.127.48/auth/](http://183.111.127.48/auth/)  
admin // roqkfrPwjd1216!
```
 
```
- cpm realm: [http://183.111.127.48/auth/realms/cpm/account](http://183.111.127.48/auth/realms/cpm/account)  
canape // Bliex1234
```