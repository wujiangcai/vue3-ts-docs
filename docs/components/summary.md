# 组件基础
### 定义一个组件

当使用构建步骤时，我们一般会将 Vue 组件定义在一个单独的 `.vue` 文件中，这被称为单文件组件 (SFC)：

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">You clicked me {{ count }} times.</button>
</template>
```

当不使用构建步骤时，Vue 组件则以一个包含 Vue 特定选项的 JavaScript 对象来定义：

```javascript
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)
    return { count }
  },
  template: `
    <button @click="count++">
      You clicked me {{ count }} times.
    </button>`
  // 也可以针对一个 DOM 内联模板：
  // template: '#my-template-element'
}
```

这里的模板是一个内联的 JavaScript 字符串，Vue 将在运行时编译它。也可以使用 ID 选择器指向一个元素（通常是原生的 `<template>` 元素），Vue 将使用其内容作为模板来源。

上面的例子中定义了一个组件，并在一个 `.js` 文件里默认导出了它。你也可以通过具名导出在一个文件中导出多个组件。

### 使用组件

**提示**  
我们将在接下来的指引中使用单文件组件语法。无论是否使用构建步骤，组件相关概念都是相同的。示例部分展示了两种场景中的组件使用情况。

要使用一个子组件，我们需要在父组件中导入它。假设我们把计数器组件放在一个叫做 `ButtonCounter.vue` 的文件中，这个组件将以默认导出的形式暴露给外部：

```vue
<script setup>
import ButtonCounter from './ButtonCounter.vue'
</script>

<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
</template>
```

通过 `<script setup>`，导入的组件在模板中直接可用。

当然，你也可以全局地注册一个组件，使得它在当前应用中的任何组件上都可以使用，而无需额外再导入。关于组件的全局注册和局部注册的利弊，我们将在组件注册章节中专门讨论。

组件可以被重用任意多次：

```vue
<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
  <ButtonCounter />
  <ButtonCounter />
</template>
```

每当点击这些按钮时，每个组件都维护着自己的状态，并且 `count` 是不同的。这是因为每次使用组件时，都会创建一个新的实例。

在单文件组件中，推荐为子组件使用 PascalCase 的标签名，以此来和原生 HTML 元素区分。尽管原生 HTML 标签名是不区分大小写的，但 Vue 单文件组件可以在编译中区分大小写。我们也可以使用自闭合标签的形式。

如果你是在 DOM 中书写模板（例如原生 `<template>` 元素的内容），模板的编译需要遵循浏览器中的 HTML 解析行为。在这种情况下，应使用 kebab-case 形式并显式关闭这些组件的标签：

```html
<!-- 如果是在 DOM 中书写该模板 -->
<button-counter></button-counter>
<button-counter></button-counter>
<button-counter></button-counter>
```
