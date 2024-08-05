## 在请求头中配置Bearer Token后仍然显示401 unauthorized解决方案

docker-compose.yml文件中配置环境变量

```shell
- AUTH_VALID_ISSUERS_LOCAL=http://<KEYCLOAK_HOST>:<KEYCLOAK_PORT>/realms/neone
#此处配置的是token发布者（issuer）地址，配置信任的token发布者
- AUTH_ISSUERS_LOCAL_PUBLICKEY_LOCATION=http://<KEYCLOAK_HOST>:<KEYCLOAK_PORT>/realms/neone/protocol/openid-connect/certs
#此处配置的是公钥的地址，用于验证token签名
```

**<KEYCLOAK_HOST>:<KEYCLOAK_PORT>替换为具体配置的Keycloak服务器ip+端口，如：192.168.40.121:8989**

> 注意：
>
>   1.确保`http://[keycloak-location]/realms/neone`和`http://[Keycloak-location]/realms/neone/protocol/openid-connect/certs`能够正常访问
>
> <img src="../images/public_key.png" style="zoom:50%;" alt="public_key" title="public_key">
>
> <div style="text-align: center">图1 访问/realms/neone/protocol/openid-connect/certs</div>
>
>   2.注意防火墙规则，允许外界NEONE访问NEONE和Keycloak
>
>   3.内网服务器需要注意配置端口映射或端口转发，以便与外界1R服务器通信（推荐使用端口映射）