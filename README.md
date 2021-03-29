# v2ray-examples

这里是一些供参考的 V2Ray 配置示例，内容与时俱进，自动化脚本等请勿从这里拉取配置。

感谢 vTemplate 的作者 KiriKira、雨落无声和 Project V 的所有开发人员。

## 贡献指南

欢迎你将自己使用的配置制作模板，提交 PR。

模板应遵守以下标准：
- 缩进使用 4 个空格
- 方 (花) 括号不换行
- 不需要的字段应该移除
- `log` 部分只留 `loglevel`
- 对于 `outbounds`，客户端应有 `proxy` 和 `direct`，服务端应有 `direct` 和 `block`
- 除非是适用于特定场景的模板，否则应当将 `geoip:private` 路由到 `direct` 出站 (服务端配置路由到 `block` 出站)
- 除非是适用于特定场景的模板，否则配置文件中不应出现 DNS
- `uuid` 应留空，由用户自行填写。
- `routing` 中的 `domainStrategy` 保持默认，即 `AsIs`。

### 客户端

<!-- 此处 yaml 仅用作语法高亮，实际内容为 json -->
```yaml
{
    "log": {
        "loglevel": "debug"
    },
    "routing": {
        "domainStrategy": "AsIs",
        "rules": [
            {
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "direct",
                "type": "field"
            }
        ]
    },
    "inbounds": [  // useless but configuration required
        {
            "listen": "127.0.0.1",
            "port": 1080,
            "protocol": "socks",
            "settings": {
                "auth": "noauth",
                "ip": "127.0.0.1",
                "udp": true
            },
            "tag": "socks"
        }
    ],
    "outbounds": [
        {
            "protocol": "shadowsocks",
            ...,
            "tag": "proxy"

        },
        {
            "protocol": "freedom",
            "tag": "direct"
        }
    ]
}
```
