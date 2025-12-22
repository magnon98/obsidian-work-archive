```
$ npm install appcenter appcenter-analytics appcenter-crashes --save-exact  
$ react-native link
```
       
```
Windows 에서 아래와 같은 메시지 출력 후 멈추는 경우 아래 명령으로 inquirer 재설치  
iOS App Secret is already set in ios/sample02/AppCenter-Config.plist
```
   

```
$ rd /s /q node_modules\inquirer  
$ npm i -d inquirer
```
   

```
-d 옵션은 아래 참고  
[https://docs.npmjs.com/misc/config#shorthands-and-other-cli-niceties](https://docs.npmjs.com/misc/config#shorthands-and-other-cli-niceties)
```