# 基础风格

## TypeScript

TypeScript(和 JavaScript)的代码风格上统一使用
[prettier 风格](https://prettier.io) + [airbnb 规范](http://airbnb.io/javascript/)，
并用[standard 规范](https://standardjs.com/)加以补充。
标准间有冲突时，优先级是 prettier > airbnb > standard 。

- Airbnb 规范 ES6 版中文参考：<https://github.com/yuche/javascript>
- Standard 规范中文参考：<https://standardjs.com/rules-zhcn.html>

### tslint 基础配置

```json
{
  "extends": ["tslint-config-standard", "tslint-config-airbnb", "tslint-config-prettier"]
}
```
