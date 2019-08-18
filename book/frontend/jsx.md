# JSX 开发（React&Taro 通用）

## 状态管理

`state` 用于保存组件中会发生变化的状态值，一般是会由外因导致变化的值（如用户操作/输入）。组件设计开发时应避免过多的 `state`，以免组件的状态难以跟踪。
只负责数据展示的 presentation 组件不需要状态。

### 不要将数据保存在成员变量中

只有 `props` 和 `state` 的变化会触发重新渲染，将数据保存在成员变量中会导致页面不会渲染最新的数据。

### 不要用 `state` 保存渲染的中间状态

任何通过原始数据计算或重组以供渲染用的中间状态应作为 `render` 的本地变量，在每次渲染时重新计算。

```jsx
// GOOD
function XxxComponent(props) {
  const itermediateValues = props.vals.map(val => { ... });
  return <div>{itermediateValues}</div>
}

// BAD
class XxxComponent {
  componentDidMount() {
    const itermediateValues = props.vals.map(val => { ... });
    this.setState({
      itermediateValues
    });
  }

  render() {
    return <div>{this.state.itermediateValues}</div>
  }
}
```

## 渲染优化

### 通过循环渲染一系列子组件时，不要用下标(index)作为`key`

```jsx
// GOOD: 使用来源数据的ID作为key
{
  props.items.map(item => <span key={item.id}>{item.value}</span>);
}

// GOOD: 使用来源数据中的某个唯一值作为key
{
  props.items.map(item => <span key={item.uniqueValue}>{item.value}</span>);
}

// GOOD: 使用来源数据中的多个值拼成的唯一值作为key
{
  props.items.map(item => <span key={`${item.v1}${item.v2}`}>{item.value}</span>);
}

// BAD: 使用下标作为key是反优化
{
  props.items.map((item, i) => <span key={i}>{item.value}</span>);
}
```
