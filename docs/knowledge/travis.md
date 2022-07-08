# travis-CI/CD 
travis则是github的合作伙伴，提供云端的机器帮我门运行云端的脚本。


``` 

language: node_js  # 设置语言
node_js: 10  # 指定node.js版本
script: npm run test # 脚本
notifications: # 接收测试结果通知
  email: false
```

 

