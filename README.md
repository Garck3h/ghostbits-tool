# GhostBits - 幽灵比特编解码工具

GhostBits 是一个用于安全研究的幽灵比特（Ghost Bits）编解码工具，演示 Java `char→byte` 高位截断导致的 WAF 绕过技术。

## 原理

Java 中 `char` 为 16 位，`(byte)char` 强制转换时只保留低 8 位，丢弃高 8 位。攻击者可利用这一特性，将 ASCII 字符替换为低 8 位相同的 Unicode 字符（如 CJK 汉字），使 WAF 的 ASCII 正则检测失效，而 Java 后端仍能还原原始 Payload。

```
编码: ghost = charCode | mask
解码: ascii = charCode & 0xFF
```

## 功能

- **编码器** — 将 ASCII 文本转换为幽灵字符
- **解码器** — 将幽灵字符还原为 ASCII
- **逐字符分解** — 可视化每个字符的 16 位二进制分解（高位/低位标注）
- **WAF 视角对比** — 直观展示 WAF 拦截 vs 放行的差异
- **双重编码** — 叠加 `%uXXXX` (IIS-Style Unicode) 形成双重绕过
- **预设 Payload** — 内置路径穿越、SQL 注入、SpEL RCE 等研究用例

## 使用

直接在浏览器中打开 `index.html` 即可使用，无需安装任何依赖。

## 免责声明

本工具仅供安全研究与教学目的。使用者需遵守所在地区的法律法规，严禁用于任何未授权的渗透测试或攻击行为。作者不对因使用本工具造成的任何后果承担责任。

## License

MIT
