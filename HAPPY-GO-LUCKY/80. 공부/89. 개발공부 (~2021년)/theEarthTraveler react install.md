---
Created: Invalid date
Updated: Invalid date
---
1. react-native init

react-native init zamongly

cd zamongly

react-native run-ios  or Xcode build

2. git

git init

git remote add origin https://github.com/zuhern/zamongly.git

git pull origin master

git add *

git commit

git push origin master

3. webpack (추후에)

npm install -g webpack

4. babel (http://babeljs.io/docs/plugins/preset-react/\#basic-setup-with-the-cli-) (jsx를 위해)

npm install --save-dev babel-cli babel-preset-react

npm install --save-dev babel-cli babel-preset-es2015

echo '{ "presets": ["react"] }' > .babelrc

5. react-native-web (x)

https://github.com/necolas/react-native-web

npm install --save react@15.4 react-native-web

- mac simulator log: tail -f /var/log/system.log
- http://localhost:8081/debugger-ui

6. react-native debugger (사용법을 모르겠음.)

brew update && brew cask install react-native-debugger7. react-router-native (페이지 변환: 안씀.. navigator 적극 활용하려고 함)npm install --save react-router-native

8. reduxnpm install --save redux

9.firebasenpm install firebase --save