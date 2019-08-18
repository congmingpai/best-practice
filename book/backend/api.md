# API 开发

## 错误处理

### ctx.throw

例如：<https://github.com/gregwym/smartpi-server/pull/1423>
全局修复: <https://github.com/gregwym/smartpi-server/pull/1436>

```js
// GOOD
ctx.throw(400, 'Sku ID is required');
ctx.throw(400, 'Sku ID is required');

// BAD
ctx.throw('Sku ID is required'); // 默认500
ctx.throw(400); // Sentry只会收到Bad Request的错误消息，没有具体信息
```
