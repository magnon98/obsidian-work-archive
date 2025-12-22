```
cat /etc/ssl/openssl.cnf | sed "s/\= policy_match/\= policy_anything/" \> openssl_custom.conf
```
 
```
### or 
```
 
```
cat /etc/pki/tls/openssl.cnf | sed "s/\= policy_match/\= policy_anything/" \> openssl_custom.conf
```
    
```
cat \<\<EOF \> apig.d-platform.doosan.com.conf  
[req]  
distinguished_name = req_distinguished_name  
req_extensions = v3_req  
prompt = no
```
 
```
[req_distinguished_name]  
commonName = d-platform.doosan.com
```
 
```
[v3_req]  
keyUsage = keyEncipherment, dataEncipherment  
extendedKeyUsage = serverAuth  
subjectAltName = @alt_names
```
 
```
[san]  
subjectAltName = @alt_names
```
 
```
[alt_names]  
DNS.1 = apig.d-platform.doosan.com  
DNS.2 = foo.d-platform.doosan.com  
DNS.3 = bar.d-platform.doosan.com  
DNS.4 = *.apig.d-platform.doosan.com  
EOF
```
    
```
openssl req -x509 \  
  -nodes \  
  -days 730 \  
  -newkey rsa:2048 \  
  -keyout apig.d-platform.doosan.com.key \  
  -out apig.d-platform.doosan.com.crt \  
  -config apig.d-platform.doosan.com.conf \  
  -extensions 'v3_req'
```