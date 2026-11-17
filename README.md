# Proxy-Config

个人使用的 Shadowrocket（小火箭）配置。

## 导入方式

Shadowrocket → 配置 → 右上角 `+` → 输入下面的链接 → 下载后点选使用：

```
https://raw.githubusercontent.com/aidzhou/Proxy-Config/main/shadowrocket.conf
```

> 规则集托管在 `raw.githubusercontent.com`，首次需要先有一个可用节点才能下载远程规则。

## 设计思路

| 项目 | 做法 |
| --- | --- |
| 分流 | 国内直连（ChinaMax + `GEOIP,CN`），其余走代理（`FINAL,PROXY`） |
| 广告 | BlackMatrix7 `AdvertisingLite` 拦截 |
| AI 服务 | 本地写明域名规则，不订阅第三方 AI 规则（OpenAI / Anthropic / Google / Perplexity / Cursor 等） |
| Apple | 常用域名直连 |
| DNS | 国内用国内：DNSPod、阿里 DoH 解析直连域名；国外用国外：代理域名由节点远端解析，Google、Cloudflare DoH 经代理作备用 |
| 隐私 | 关闭 MITM、关闭 IPv6、拦截 53 端口明文 DNS、STUN 回应占位地址、不支持 UDP 时拒绝 |

## 可调项

- DNS：`dns-server` 为国内 DoH（`doh.pub`、`dns.alidns.com`），`fallback-dns-server` 为境外 DoH（`#proxy`）。若遇到个别境外域名被污染，可把境外 DoH 挪到 `dns-server` 前面。
- AI 规则：新增服务时在 `[Rule]` 的 AI 区块加一行 `DOMAIN-SUFFIX,xxx.com,PROXY` 即可。
- 想要更严格的去广告，可把 `AdvertisingLite` 换成 `Advertising`（误杀概率更高）。

## 文件

- `shadowrocket.conf`：主配置
