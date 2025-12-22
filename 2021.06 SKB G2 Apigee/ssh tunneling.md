```
 ssh -L 9000:localhost:9000 -o ProxyCommand="ssh -vvv -q -x root@175.113.150.8 -W %h:%p" root@10.10.214.116
```