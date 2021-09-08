# Search 搜索

### 介绍

用于搜索场景的输入框组件。

### 引入

```tsx
import { Search } from "@taroify/core"
```

## 代码演示

### 基础用法

`value` 用于控制搜索框中的文字，`onChange` 可以获得改变的值。

```tsx
function BasicSearch() {
  const [value, setValue] = useState("")
  return (
    <Search
      value={value}
      placeholder="请输入搜索关键词"
      onChange={(e) => setValue(e.detail.value)}
    />
  )
}
```

### 事件监听

Search 组件提供了 `onSearch` 和 `onCancel` 事件，`onSearch` 事件在点击键盘上的搜索/回车按钮后触发，`onCancel` 事件在点击搜索框右侧取消按钮时触发。

```tsx
function SearchWithEvents() {
  const [value, setValue] = useState("")
  const [open, setOpen] = useState(false)

  return (
    <>
      <Toast open={open} onClose={() => setOpen(false)}>
        取消
      </Toast>
      <Search
        value={value}
        placeholder="请输入搜索关键词"
        action
        onChange={(e) => setValue(e.detail.value)}
        onCancel={() => setOpen(true)}
      />
    </>
  )
}

```

### 搜索框内容对齐

通过 `inputAlign` 属性设置搜索框内容的对齐方式，可选值为 `center`、`right`。

```tsx
function InputCenterSearch() {
  const [value, setValue] = useState("")
  return (
    <Search
      value={value}
      placeholder="请输入搜索关键词"
      inputAlign="center"
      onChange={(e) => setValue(e.detail.value)}
    />
  )
}
```

### 禁用搜索框

通过 `disabled` 属性禁用搜索框。

```tsx
<Search disabled placeholder="请输入搜索关键词" />
```

### 自定义背景色

通过 `className` 属性可以设置搜索框外部的背景色，通过 `shape` 属性设置搜索框的形状，可选值为 `round`。

```tsx
<Search className="background" shape="round" disabled placeholder="请输入搜索关键词" />
```

```scss
.background {
  background: #4fc08d;
}
```

### 自定义按钮

使用 `action` 插槽可以自定义右侧按钮的内容。使用插槽后，`cancel` 事件将不再触发。

```tsx
function CustomSearch() {
  const [value, setValue] = useState("")
  const [open, setOpen] = useState(false)
  return (
    <>
      <Toast open={open} onClose={() => setOpen(false)}>
        搜索
      </Toast>
      <Search
        value={value}
        label="地址"
        placeholder="请输入搜索关键词"
        action={<View onClick={() => setOpen(true)}>搜索</View>}
        onChange={(e) => setValue(e.detail.value)}
      />
    </>
  )
}
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| label | 搜索框左侧文本 | _string_ | - |
| shape | 搜索框形状，可选值为 `round` | _string_ | `square` |
| maxlength | 输入的最大字符数 | _number \| string_ | - |
| placeholder | 占位提示文字 | _string_ | - |
| clearable | 是否启用清除图标，点击清除图标后会清空输入框 | _boolean_ | `true` |
| clearIcon| 清除图标 | _string_ | `<Clear />` |
| clearTrigger | 显示清除图标的时机，`always` 表示输入框不为空时展示，<br>`focus` 表示输入框聚焦且不为空时展示 | _string_ | `focus` |
| autofocus | 是否自动聚焦，iOS 系统不支持该属性 | _boolean_ | `false` |
| action | 是否在搜索框右侧显示取消按钮 | _boolean \| ReactNode_ | `false` |
| disabled | 是否禁用输入框 | _boolean_ | `false` |
| readonly | 是否将输入框设为只读状态，只读状态下无法输入内容 | _boolean_ | `false` |
| error | 是否将输入内容标红 | _boolean_ | `false` |
| message | 底部错误提示文案，为空时不展示 | _string_ | - |
| inputAlign | 输入框内容对齐方式，可选值为 `center` `right` | _string_ | `left` |
| icon | 输入框左侧图标 | _ReactNode_ | `<Search />` |
| rightIcon | 输入框右侧图标 | _ReactNode_ | - |

### Events

| 事件名             | 说明                 | 回调参数                       |
| ------------------ | -------------------- | ------------------------------ |
| onSearch             | 确定搜索时触发      | _event: BaseEventOrig<InputProps.inputValueEventDetail>_ |
| onChange             | 输入框内容变化时触发 | _event: BaseEventOrig<InputProps.inputEventDetail>_ |
| onFocus              | 输入框获得焦点时触发 | _event: BaseEventOrig<InputProps.inputForceEventDetail>_ |
| onBlur               | 输入框失去焦点时触发 | _event: BaseEventOrig<InputProps.inputForceEventDetail>_ |
| onClear              | 点击清除按钮后触发   | _event: event: ITouchEvent_                              |
| onCancel             | 点击取消按钮时触发   | _event: event: ITouchEvent_                              |