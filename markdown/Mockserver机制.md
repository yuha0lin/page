## Mockserver

1. 匹配机制:
   当MockServer接收到一个请求时,它会遍历所有的Active Expectations,寻找与该请求匹配的规则。
2. 响应生成:
   一旦找到匹配的expectation,MockServer就会根据该expectation中定义的响应内容生成一个响应。

```shell
version: "3"

services:
  mockserver:
    image: mockserver/mockserver:5.15.0
    ports:
      - "1080:1080"
    volumes:
      - "../../test/resources/mockserver.properties:/config/mockserver.properties"
      - "../../test/resources/mockserver/:/mockserver/"
    environment:
      - MOCKSERVER_PROPERTY_FILE=/config/mockserver.properties
      - MOCKSERVER_INITIALIZATION_JSON_PATH=/config/*.json
      
```

如上文中卷（volumes）配置中

将`../../test/resources/mockserver.properties`文件挂载到容器内的`/config/mockserver.properties`

将`../../test/resources/mockserver/`挂载到容器内的`/mockserver/`

挂载的文件用于初始化端点

指定`MOCKSERVER_PROPERTY_FILE`属性文件的位置为`/config/mockserver.properties`

指定MOCKSERVER_INITIALIZATION_JSON_PATH`初始化JSON文件的路径为`/config/`路径下的所有.json文件



