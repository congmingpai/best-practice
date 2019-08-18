# JSX 开发（React&Taro 通用）

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
