# 命名

统一的命名风格能让我们快速地了解某个名字代表的含义，而不需要去查找原始声明。

## 命名格式规范

| 类型                  | 代码命名      | 举例                                        |
| --------------------- | ------------- | ------------------------------------------- |
| 类 (class)            | 大写驼峰      | `class FooBar {...}`                        |
| 类成员 (class member) | 小写驼峰      | `private fooBar: number = 0;`               |
| 类方法 (class method) | 小写驼峰      | `private fooBar(): boolean {...}`           |
| 函数 (function)       | 小写驼峰      | `function fooBar(): boolean {...}`          |
| 参数 (parameter)      | 小写驼峰      | `private do(fooBar: number): boolean {...}` |
| 变量 (variable)       | 小写驼峰      | `const fooBar = 0;`                         |
| 常量 (constant)       | 全大写+下划线 | `const FOO_BAR = 0;`                        |
| 枚举 (enumeration)    | 大写驼峰+单数 | `enum FooBar { FOO_BAR };`                  |
| 接口 (interface)      | 大写驼峰+单数 | `interface FooBar {...};`                   |
| 类型 (type)           | 大写驼峰+单数 | `type FooBar = int;`                        |

## 命名约定

### 通用规则

命名要具有描述性，只使用人尽皆知的缩写，不要担心过长，让代码易于新读者理解更重要。

```js
// GOOD
const window;
const numOfCompletedQuestions;
const failedRoundCount;
class FlipCoinGameController {}
const clientIp; // 人人都知道IP是什么意思

// BAD
const w; // 毫无意义
const countCmp; // 含糊不清的缩写
const failedRdCnt; // 删减字母后难以理解
class FCGameCtl {} // FC有很多种解释，只有作者才能理解
```

### 类（class），接口（Interface），类型（type）

面向对象编程中，对象代表着一个具体的事物，而类是对象的模版，用来统一表示一种类型的事物，所以类的命名要以描述这一类型的事物为目的。接口和类型与类相似。

对类命名时，

- 后缀应表示事物的根本类型，以名词结尾；
- 前缀对后缀所表示的事物进行修饰，进一步限制含义。

```js
// GOOD
class EnrollmentManagerTestSuite {} // EnrollmentManager的测试用例
class ReviewConfigCsvParser extends CsvParser {} // 用于ReviewConfig的csv解析器

// BAD
class TestEnrollmentManager {} // 后缀没有表示事物的根本类型是测试用例，而不是Manager
class ReviewConfigParse extends CsvParser {} // 不能以动词结尾
```

### 方法（method），函数（function）

方法和函数代表着一段执行逻辑，需以动词开头，动词后附加描述来进一步限定含义。

```js
// GOOD
authService.loginWithWechat(code);
submitLoginForm(formData);
moveUpAndDown(node);

// BAD
authService.wechatLogin(); // 没有动词开头
formSubmit(formData); // 没有动词开头
jump(node); // 没有限定jump的目的，jumpToXxx会更明确；或作为方法名时，node.jump()可以理解。
```

几种常见有特殊意义的函数/方法名前缀，只应在特定的情况下使用。

| 命名                                | 例子                               | 解释                            |
| ----------------------------------- | ---------------------------------- | ------------------------------- |
| `isXxx`                             | `isInteger`                        | 检查类型并返回 boolean          |
| `checkXxx`                          | `checkParams`                      | 检查内容并返回 boolean          |
| `validateXxx`                       | `validateParams`                   | 校验类型/内容，失败抛出异常     |
| `convertToXxx` / `toXxx`            | `convertToString` / `toString`     | 转换类型/格式为 Xxx             |
| `onXxxx`                            | `onClicked`                        | Xxx 事件的响应逻辑（handler）   |
| `willXxx` / `aaaWillXxx` / `preXxx` | `componentWillMount` / `preRender` | Xxx 事件发生前的钩子（prehook） |
| `didXxx` / `aaaDidXxx` / `postXxx`  | `componentDidMount` / `postRender` | Xxx 事件发生前的钩子（prehook） |
