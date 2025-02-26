---
Created: Invalid date
Updated: Invalid date
---
***** platform과 plugins만 지웠을 때

rm -rf /platform

rm -rf /plugins

cordova plugin add cordova-plugin-contacts@2.1.0

ionic state restore

***** 처음 설치

ionic start devdactic-android-push

ionic add ionic-platform-web-client  
ionic plugin add phonegap-plugin-push  
ionic io init  
ionic state restore --platform  

ionic state restore --plugins

// 사진 관련  
cordova plugin add cordova-plugin-file-transfer  
cordova plugin add cordova-plugin-file  

cordova plugin add cordoba-plugin-camera

cordova plugin add cordova-plugin-contacts

cordova plugin list  
ionic serve  
ionic build ios  
- deploy  

ionic upload --note='친구목록 업데이트' --deploy=staging

**

[Build failed, Error code 65 for command: xcodebuild](https://forum.ionicframework.com/t/build-failed-error-code-65-for-command-xcodebuild/41915)

ionic platform update ios

이나 platform, plugins 지우고 새로 깔기

**

Error: [$injector:nomod] Module 'ionic.service.core' is not available!

ionic config build