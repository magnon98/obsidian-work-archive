access to secured api-server  

```
$ MASTER_IP=123.123.123.123
$ TOKEN_NAME=`kubectl get serviceaccount default -o jsonpath="{.secrets..name}"`
$ AUTH_TOKEN=`kubectl get secret $TOKEN_NAME -o jsonpath='{.data.token}' | base64 -d`
$ curl https://$MASTER_IP:6443/ --header "Authorization: Bearer $AUTH_TOKEN"
```
 load balancing 등을 위해 마스터노드들의 앞쪽에 reverse proxy하나를 두어야 함.
 
```
const https = require('https');
let opts = {
    hostname: '127.0.0.1',
    port: '6443',
    path: '/',
    method: 'GET',
    rejectUnauthorized: false,
    headers: {
        // 'Authorization': 'Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRlZmF1bHQtdG9rZW4tYzRubjYiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGVmYXVsdCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImMyMGZjM2E5LTY4NGEtMTFlNy05OGRmLTBlYWI0ZDc0YTc5YSIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZWZhdWx0OmRlZmF1bHQifQ.E66jH3p5poNpz7sYIt5MKrgjlFM_lybLBdFj_mU5m919rsszFILkJ9B19F7KxEW-DDqC7SPVJmXdCqP1bG4e6ONlAj5CasKo4tavuzQXEoiu9Sikcalc8DGC3L8O579igSG1I2p9HlAU4rpBEdW4eJhnWMYAq9ULHm-S83cN7Jv8aUodaVTsgAHfOcarrggoLL83877R-IJJVZujV68kXRhVKeNFsZ7i5n0ayls59czNjdogRH2JjMa5TQmBKyUjMnFTUtMi5pH9wm0Im-vBlAylomvQ33nJQ9KfdlvtFMAhcJkwXBpgYPyNQ4DbBUr86oe1tBrdlufClqpdPXUW_Q'
    },
};
https.get(opts, res =\> {
    let result = '';
    res.setEncoding('utf8');
    res.on('data', data =\> {
        result += data;
    });
    res.on('error', err =\> {
        console.error(err);
    })
    res.on('end', () =\> {
        console.info('result:\n', result);
    })
});
```
    
```
[ec2-user@master01 kubernetes]$ kubectl create serviceaccount admin
serviceaccount "admin" created
[ec2-user@master01 kubernetes]$
[ec2-user@master01 kubernetes]$
[ec2-user@master01 kubernetes]$ kubectl get serviceaccount admin -o yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: 2017-07-17T00:52:02Z
  name: admin
  namespace: default
  resourceVersion: "60554"
  selfLink: /api/v1/namespaces/default/serviceaccounts/admin
  uid: 25b7a6f2-6a8a-11e7-92c8-0eab4d74a79a
secrets:
- name: admin-token-8ngzl
[ec2-user@master01 kubernetes]$
[ec2-user@master01 kubernetes]$
[ec2-user@master01 kubernetes]$ kubectl get secret admin-token-8ngzl -o yaml
apiVersion: v1
data:
  ca.crt: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM5ekNDQWQrZ0F3SUJBZ0lKQU5CQ1h2dWtqZkhRTUEwR0NTcUdTSWIzRFFFQkN3VUFNQkl4RURBT0JnTlYKQkFNTUIydDFZbVV0WTJFd0hoY05NVGN3TnpFME1EUXdPVFF6V2hjTk5EUXhNVEk1TURRd09UUXpXakFTTVJBdwpEZ1lEVlFRRERBZHJkV0psTFdOaE1JSUJJakFOQmdrcWhraUc5dzBCQVFFRkFBT0NBUThBTUlJQkNnS0NBUUVBCjZ0SXRsc2tpOUt6aG5DMFh4bVNLOUNKTWt0VzlRNzFSYW5aTndXOXRxQ01sNUZWTjhOSnlDNUYyd09PNGNQN1AKOU1McllwaUNIa2xpZlVWM0RiV3hoa0xWUElyOC91OXlNbHZSWjMwYVNTRmVZTDNWOFBJaHozT09RUU5ZbFFvaAorWHpaTHNIOTJMWW8wVW5VTEk2clYrSFFsK2JOL0gwMVZVRmpkVHBzOHUrWGpiK1IvR1JoN3RabTYvblp3bzZSCnNNUTVTYTQ2SFNCM2NBazFScnBUa3B0cFJQUUpNTWIreHR6eXNWR01aTUZuSWFhTms1VkQ0TkRBRWJhdHJOMFEKa3lwQlRPR1ZwcmIrSWNoNGljS3FvVEpuaC8zQmppNnFmQ2pGcEJRYW54YktBRTJKRVM1UmNJTG4wQXV2ZWRSeApDdHBwb2hWdlZBaVcrWE9vN3pRZGF3SURBUUFCbzFBd1RqQWRCZ05WSFE0RUZnUVVOSzFLNmZsMDkyTGhPMTRYCkF0M2w2RkRpeDM0d0h3WURWUjBqQkJnd0ZvQVVOSzFLNmZsMDkyTGhPMTRYQXQzbDZGRGl4MzR3REFZRFZSMFQKQkFVd0F3RUIvekFOQmdrcWhraUc5dzBCQVFzRkFBT0NBUUVBTlZpbVdUMXNCSGFNdm5hVHhsRWI1ZzZFeUJhTgplSkZaTnV0MnZPWDhIMFMzL1BvNVExcEQ5VlMrYmV5RkNVRWJPUWpPM0FzbjVISTlKTE1DNDN5ME43VnVCdWcwCkgzT2d3d3pJTXN2RFFYTytyQnBTdmNEYi9TV2NlMFgxMTFkbHk5QnBaS1M2eTZROHN4ZHhrdkFVeWFBZ1l0elEKZ2hFRmI4c0xSWCtxZ2VHS2pLYW5FYnE0eStzN1NrRlEyWUs1WEVldStvZ0tsbzNOWmU5THZpL0lCaHZqY3hBNwpLUUpZY2Q4WFkzekFXcUp3cE5mWDFxRnFLMWt3OWZMMytFTTRXdlNlYTJzckMzQmtST3hsZ2FZNjIxQWsweHh6CnhjdTZrbWxiUm00M3pEZ3dnNmUvbHRrUFVxd1QyOG16ZlBsdThnc201ZFUvcmVFK3FMTkY2c2FNT0E9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
  namespace: ZGVmYXVsdA==
  token: ZXlKaGJHY2lPaUpTVXpJMU5pSXNJblI1Y0NJNklrcFhWQ0o5LmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXVZVzFsYzNCaFkyVWlPaUprWldaaGRXeDBJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5elpXTnlaWFF1Ym1GdFpTSTZJbUZrYldsdUxYUnZhMlZ1TFRodVozcHNJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5elpYSjJhV05sTFdGalkyOTFiblF1Ym1GdFpTSTZJbUZrYldsdUlpd2lhM1ZpWlhKdVpYUmxjeTVwYnk5elpYSjJhV05sWVdOamIzVnVkQzl6WlhKMmFXTmxMV0ZqWTI5MWJuUXVkV2xrSWpvaU1qVmlOMkUyWmpJdE5tRTRZUzB4TVdVM0xUa3lZemd0TUdWaFlqUmtOelJoTnpsaElpd2ljM1ZpSWpvaWMzbHpkR1Z0T25ObGNuWnBZMlZoWTJOdmRXNTBPbVJsWm1GMWJIUTZZV1J0YVc0aWZRLmY3MGJvZWd1U3dQVGFlc3JYZ1dNRm9nUkhyZnkzZnBscVhhSDBvYmdsQ0Q4OFR1SEV5bl9USTVoVXlGd0I0R0xaT1V5RjFCeWF3N0NwWU1DMlZMZWRIUmtzeDg1UV81LTdYVk9nR1J0c0swZG1mbUx5MjRxQjE2S1FOZlJRNjh2dWozajFPQXJmNEtWUG0tSTN2WnVGYlhYRmoxNWRwQ1ZzTlBhRnJUQXE4emRrcGhpNlJISXlBXzB2QXhXUkhqTy1OU2oxbW50V2tJMWhRWU1MS2VNb3pPRGczcEdaRE80cTdiN2hnb3JVT3NFamZHMHhSS0M1c3R0LW5hZWxnQnNOUW1aS3FjVU53VU9haTRKSGY3Z0ZaclllOWhVUTVyX0pNUng3QmpWZ01JYTJwazAzbkg3a1Q1NzFJWWlYb3ZDZUExR0xfM0xqWDJzQ1JJLTlqRW9adw==
kind: Secret
metadata:
  annotations:
    kubernetes.io/service-account.name: admin
    kubernetes.io/service-account.uid: 25b7a6f2-6a8a-11e7-92c8-0eab4d74a79a
  creationTimestamp: 2017-07-17T00:52:02Z
  name: admin-token-8ngzl
  namespace: default
  resourceVersion: "60553"
  selfLink: /api/v1/namespaces/default/secrets/admin-token-8ngzl
  uid: 25b992d4-6a8a-11e7-92c8-0eab4d74a79a
type: kubernetes.io/service-account-token
[ec2-user@master01 kubernetes]$
[ec2-user@master01 kubernetes]$
[ec2-user@master01 kubernetes]$
curl https://10.96.0.1:443/ --header "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRlZmF1bHQtdG9rZW4tYzRubjYiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGVmYXVsdCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImMyMGZjM2E5LTY4NGEtMTFlNy05OGRmLTBlYWI0ZDc0YTc5YSIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZWZhdWx0OmRlZmF1bHQifQ.E66jH3p5poNpz7sYIt5MKrgjlFM_lybLBdFj_mU5m919rsszFILkJ9B19F7KxEW-DDqC7SPVJmXdCqP1bG4e6ONlAj5CasKo4tavuzQXEoiu9Sikcalc8DGC3L8O579igSG1I2p9HlAU4rpBEdW4eJhnWMYAq9ULHm-S83cN7Jv8aUodaVTsgAHfOcarrggoLL83877R-IJJVZujV68kXRhVKeNFsZ7i5n0ayls59czNjdogRH2JjMa5TQmBKyUjMnFTUtMi5pH9wm0Im-vBlAylomvQ33nJQ9KfdlvtFMAhcJkwXBpgYPyNQ4DbBUr86oe1tBrdlufClqpdPXUW_Q"
```
   

```
$ TOKEN_NAME=`kubectl get serviceaccount default -o jsonpath="{.secrets..name}"`
$ AUTH_TOKEN=`kubectl get secret $TOKEN_NAME -o jsonpath='{.data.token}' | base64 -d`
$ curl https://10.96.0.1:443/ --header "Authorization: Bearer $AUTH_TOKEN"
```