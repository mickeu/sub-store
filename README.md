# Sub-Store 脚本

个人用的 Sub-Store 脚本合集，供订阅远程引用。

## add-suffix.js — 节点名加后缀

给订阅内所有节点名追加后缀，解决两个机场节点同名冲突（客户端只显示一个机场节点）的问题。

**使用**：Sub-Store 订阅编辑页 → 节点操作 → 添加「脚本操作」→ 填脚本 URL：

```
https://raw.githubusercontent.com/mickeu/sub-store/main/add-suffix.js#suffix=A机场
```

**参数**：
| 参数 | 说明 | 默认 |
|------|------|------|
| `suffix` | 要追加的后缀 | `A机场` |
| `sep` | 节点名与后缀的分隔符 | 空格 |
| `overwrite` | `true` 强制追加（即使已包含后缀）；默认自动跳过 | `false` |

## availability.js — 节点测活过滤（xream 社区版）

拉取订阅时对每个节点做连通性检测，失败/超时节点自动过滤，只保留可用节点。仅支持 Surge / Loon / Egern 环境。

**使用**：同上，填脚本 URL：

```
https://raw.githubusercontent.com/mickeu/sub-store/main/availability.js#timeout=2000&retries=1&retry_delay=1000&concurrency=10&show_latency=true&keep_incompatible=true
```

**关键参数**：
| 参数 | 说明 | 默认 |
|------|------|------|
| `timeout` | 单次请求超时（毫秒） | `5000` |
| `retries` / `retry_delay` | 重试次数 / 重试延时（毫秒） | `1` / `1000` |
| `concurrency` | 并发数 | `10` |
| `url` | 测速 URL | `http://connectivitycheck.platform.hicloud.com/generate_204` |
| `status` | 期望状态码正则 | `204` |
| `method` | 请求方法（head/get） | `head` |
| `show_latency` | 节点名前显示延迟 `[123] 节点名` | 不显示 |
| `keep_incompatible` | 保留当前客户端不兼容的协议 | 不保留 |
| `cache` | 开启测活缓存，配合定时处理订阅预热 | 不缓存 |

## 叠加使用

两个操作可同时添加到同一订阅（操作按顺序执行），例如先「加后缀」再「测活」，输出节点名带后缀且均为可用节点。

## 参考

- Sub-Store 官方文档：https://sub-store-org.github.io/doc/script/examples.html
- 测活脚本原作者 xream：https://github.com/xream/scripts