# 按钮 Button

## 1. 概述
按钮组件是用户界面中的基础组件之一，通常用于触发特定操作，例如提交表单、打开模态框或导航到其他页面。通过自定义样式和功能，按钮组件可以提升用户体验。

## 2. 基本结构

### 2.1 组件创建
首先，创建一个新的 Vue 组件 `Button.vue`。

```vue
<template>
  <button
    :class="['btn', btnType, { 'is-disabled': isDisabled }]"
    :disabled="isDisabled"
    @click="handleClick"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    btnType: {
      type: String,
      default: 'primary' // 支持类型：primary, secondary, danger 等
    },
    isDisabled: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleClick(event) {
      if (!this.isDisabled) {
        this.$emit('click', event);
      }
    }
  }
}
</script>

<style scoped>
.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.primary {
  background-color: #007bff;
  color: white;
}

.secondary {
  background-color: #6c757d;
  color: white;
}

.danger {
  background-color: #dc3545;
  color: white;
}

.is-disabled {
  background-color: #e0e0e0;
  cursor: not-allowed;
}
</style>
```

## 3. 组件属性

### 3.1 `btnType`
- **类型**: `String`
- **默认值**: `primary`
- **描述**: 定义按钮的样式类型，可以是 `primary`、`secondary`、`danger` 等。

### 3.2 `isDisabled`
- **类型**: `Boolean`
- **默认值**: `false`
- **描述**: 控制按钮是否禁用，禁用状态下按钮不可点击。

## 4. 事件
按钮组件会在点击时触发 `click` 事件，除非按钮处于禁用状态。这使得父组件能够监听按钮点击事件。

## 5. 使用示例

### 5.1 基本使用
在父组件中使用按钮组件：

```vue
<template>
  <div>
    <Button 
      btnType="primary" 
      @click="handlePrimaryClick"
    >
      Primary Button
    </Button>
    <Button 
      btnType="secondary" 
      :isDisabled="true"
    >
      Disabled Button
    </Button>
  </div>
</template>

<script>
import Button from './Button.vue';

export default {
  components: {
    Button
  },
  methods: {
    handlePrimaryClick() {
      alert('Primary button clicked!');
    }
  }
}
</script>
```

### 5.2 样式自定义
你可以通过传递不同的样式类来扩展按钮的样式。例如，添加一个新的样式类：

```vue
<template>
  <Button btnType="danger">Danger Button</Button>
</template>
```

### 5.3 插槽使用
按钮组件支持插槽，使得按钮内容可以灵活设置：

```vue
<Button btnType="primary">
  <span icon class="icon">🔍</span>
  Search
</Button>
```

## 6. 总结
按钮组件是构建用户交互的重要部分，通过合理的设计和实现，可以提升应用的可用性和用户体验。在实际开发中，可以根据项目需求扩展更多属性和事件，提高组件的灵活性和适应性。