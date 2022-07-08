# gitlab-CI/CD

在gitLab CI/CD中，具体如何运行流水线，是由 .gitlab-ci.yml来管理的，这个文件放在项目仓库的根目录

```

stages:   全局关键词，用于定义当前流水线包含多少个阶段。它的值是一个数组，数组的顺序规定的每一个阶段的运行顺序
  - build
  - test
  - release
  - deploy

variables:  全局关键词，用于定义变量
  DOCKER_DRIVER: 
  
before_script: 执行script之前执行
 - *****

release: 这里可以随便定义
  stage: release 这个必须在上面有声明
  script:
    - ***
  only: 定义哪些分支和标签会被执行
    - ***
    
```

 

