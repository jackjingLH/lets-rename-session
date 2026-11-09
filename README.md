# lets-rename-session

一个轻量的 Pi 扩展：在当前会话完成前 4 条普通用户消息后，使用当前模型生成简短标题并写入会话名称。

## 当前行为

- 在第 4 条普通用户消息对应的 `agent_settled` 后触发。
- 只发送前 4 条用户消息，不发送助手消息、工具结果或思考内容。
- 使用当前选中的 Pi 模型。
- 命名请求独立执行，不向主会话追加消息，不增加主会话上下文。
- 标题最多 32 个字符。
- 清理逗号、句号、冒号、引号和解释文本。
- 模型请求失败时不提示用户，最多静默重试一次。
- 成功命名后不再重复更新。
- 不检查已有手动名称，自动结果可能覆盖已有名称。

## 自用

测试单次运行：

```bash
pi -e ./index.ts
```

全局使用时，将 `index.ts` 放入：

```text
~/.pi/agent/extensions/lets-rename-session.ts
```

然后重启 Pi 或执行：

```text
/reload
```

## 安装

当前尚未发布到 npm。后续发布后使用：

```bash
pi install npm:lets-rename-session
```

## 隐私

命名请求会把前 4 条用户消息发送给当前配置的模型服务商。扩展不会发送助手消息、工具结果或思考内容，也不会向主会话写入命名请求。

## 开发

扩展直接使用 TypeScript 源码运行。发布前检查：

```bash
npm pack --dry-run
npm publish --dry-run
```
