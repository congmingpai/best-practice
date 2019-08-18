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

1. 命名要具有描述性；
1. 只使用人尽皆知的缩写，不要担心过长，让代码易于新读者理解更重要；
1. 避免增加无附加意义的词语；
1. 不要使用系统保留词语，如 `return` `switch` 或 Cocos 中的 `start` `update`。

```js
// GOOD
const window;
const completedQuestionCount;
const failedRoundCount;
class FlipCoinGameController {}
const clientIp; // 人人都知道IP是什么意思

// BAD
const w; // 毫无意义
const countCmp; // 含糊不清的缩写
const failedRdCnt; // 删减字母后难以理解
class FCGameCtl {} // FC有很多种解释，只有作者才能理解

// More BAD
const data; // 各种东西都可以是data
const userInfo = findUser(); // user已经足够具体，Info没有给命名增加额外信息。
function doCreateObject() {}; // do是个没有明确意义的动词，所以应该省略；createObject足够具体清晰。
```

### 类 (class)，接口 (Interface)，类型 (type)，枚举 (enumeration)

> [!TIP]
> 面向对象编程中，对象代表着一个具体的事物，而类是对象的模版，用来统一表示一种类型的事物，所以类的命名要以描述这一事物类型为目的。接口和类型同理。

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

### 方法 (method)，函数 (function)

方法和函数的命名是用于描述一段逻辑。命名需以动词开头，动词后附加细节来进一步限定含义。

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

| 命名                                | 例子                               | 解释                           |
| ----------------------------------- | ---------------------------------- | ------------------------------ |
| `isXxx`                             | `isInteger`                        | 检查类型并返回 boolean         |
| `checkXxx`                          | `checkParams`                      | 检查内容并返回 boolean         |
| `validateXxx`                       | `validateParams`                   | 校验类型/内容，失败抛出异常    |
| `convertToXxx` / `toXxx`            | `convertToString` / `toString`     | 转换类型/格式为 Xxx            |
| `setXxx`                            | `setGameSpeed`                     | 设定某个 property 的值         |
| `getXxx`                            | `getDuration`                      | 获取某个 property 的值         |
| `onXxxx`                            | `onClicked`                        | Xxx 事件的响应逻辑 (handler)   |
| `willXxx` / `aaaWillXxx` / `preXxx` | `componentWillMount` / `preRender` | Xxx 事件发生前的钩子 (prehook) |
| `didXxx` / `aaaDidXxx` / `postXxx`  | `componentDidMount` / `postRender` | Xxx 事件发生前的钩子 (prehook) |

### 变量 (variable)，类成员 (class member)，常量 (constant)

变量和类成员命名时，应以名词结尾，辅以细节修饰。常见情况有，

| 情况              | 方法                         | 例子                                                      |
| ----------------- | ---------------------------- | --------------------------------------------------------- |
| 引用一个对象      | 以对象的类型为结尾           | `const newUser = new User()`                              |
| 对象数组/集合     | 以对象的类型为结尾，复数(+s) | `const users = findUsers()`                               |
| 过滤过的数组/集合 | 增加前缀修饰                 | `const activeUsers = users.filter(user => user.isActive)` |
| 计数              | 以 count 结尾                | `const userCount = users.length`                          |
| 映射              | 以 map 结尾                  | `const idToUserMap = new Map<number, User>()`             |
| 集合              | 以 set 结尾                  | `const userSet = new Set(users)`                          |

```js
// GOOD
const stagePrefab: cc.Prefab;
const stageNode = this.loadNextStageNode(stagePrefab);
const tableRows = table.rows;

// BAD
const stage: cc.Prefab; // 没有体现stage的类型是cc.Prefab
const stage = this.loadNextStage(this.stage); // 1. 没有体现stage的类型是cc.Node 2. 本地变量stage和this.stage重名但引用了不同的对象+类型
const rowList = table.rows; // 列表应以复数命名结尾，不应用List。
```

几种常见有特殊意义的变量前缀，只应在特定的情况下使用。

| 命名     | 例子                                    | 解释                    |
| -------- | --------------------------------------- | ----------------------- |
| `isXxx`  | `const isValidUser = checkUser(user);`  | 记录检查结果的 boolean  |
| `hasXxx` | `const hasEnoughMoney = money > price;` | 表示拥有 xxx 的 boolean |
