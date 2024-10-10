# 表单 Form
## 1.概述

在现代 Web 开发中，表单是用户输入和交互的重要组成部分。Vue 3 提供了强大的工具来创建动态表单，支持双向数据绑定、表单验证和异步提交。结合 TypeScript，可以增强代码的可读性和可维护性。

## 2.基本结构

### 1. 创建基本表单

下面是一个简单的表单示例，包括用户名、邮箱和密码字段：

```vue
<template>
  <form @submit.prevent="handleSubmit">
    <div>
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="form.username" required />
    </div>
    
    <div>
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="form.email" required />
    </div>
    
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="form.password" required />
    </div>
    
    <button type="submit">Submit</button>
  </form>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  setup() {
    const form = ref({
      username: '',
      email: '',
      password: ''
    });

    const handleSubmit = () => {
      console.log('Form submitted:', form.value);
    };

    return { form, handleSubmit };
  }
});
</script>

<style scoped>
/* 添加样式 */
</style>
```

### 2. 表单的基本结构解析

- **`<form>`**: 用于包裹输入元素，处理提交。
- **`@submit.prevent`**: 阻止默认提交行为，允许我们自定义逻辑。
- **`v-model`**: 实现数据的双向绑定，使得表单和 Vue 数据保持同步。

## 3.属性

### 常用属性

- **`required`**: 指定该输入项为必填项。
- **`type`**: 定义输入的类型（如 `text`, `email`, `password` 等）。
- **`id`**: 为每个输入元素分配唯一标识符，以便与 `<label>` 关联。

### 示例：添加属性

```vue
<input type="text" id="username" v-model="form.username" required placeholder="Enter your username" />
```

### 自定义属性

你还可以使用 `v-bind` 指令来绑定动态属性，如下所示：

```vue
<input :type="isPasswordVisible ? 'text' : 'password'" v-model="form.password" />
```

## 4.事件

### 常用事件

- **`@submit`**: 表单提交事件。
- **`@input`**: 输入变化事件，用于实时获取用户输入。
- **`@focus` / `@blur`**: 聚焦和失去焦点事件，用于验证或提示信息。

### 示例：处理事件

```vue
<input
  type="text"
  id="username"
  v-model="form.username"
  @input="handleInputChange"
/>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  setup() {
    const form = ref({
      username: '',
      email: '',
      password: ''
    });

    const handleInputChange = () => {
      console.log('Input changed:', form.value.username);
    };

    return { form, handleInputChange };
  }
});
</script>
```

### 事件组合

你可以组合多个事件处理程序，例如：

```vue
<button @click="handleSubmit" @mouseover="handleMouseOver">Submit</button>
```

## 5.使用示例

以下是一个增强版的表单示例，添加了表单验证和状态管理：

```vue
<template>
  <form @submit.prevent="handleSubmit">
    <div>
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="form.username" required />
      <span v-if="errors.username">{{ errors.username }}</span>
    </div>
    
    <div>
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="form.email" required />
      <span v-if="errors.email">{{ errors.email }}</span>
    </div>
    
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="form.password" required />
      <span v-if="errors.password">{{ errors.password }}</span>
    </div>
    
    <button type="submit">Submit</button>
  </form>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  setup() {
    const form = ref({
      username: '',
      email: '',
      password: ''
    });
    
    const errors = ref({
      username: '',
      email: '',
      password: ''
    });

    const validateForm = () => {
      errors.value.username = form.value.username ? '' : 'Username is required';
      errors.value.email = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.value.email) ? '' : 'Invalid email';
      errors.value.password = form.value.password.length >= 6 ? '' : 'Password must be at least 6 characters';
      
      return !errors.value.username && !errors.value.email && !errors.value.password;
    };

    const handleSubmit = () => {
      if (validateForm()) {
        console.log('Form submitted:', form.value);
      } else {
        console.log('Validation errors:', errors.value);
      }
    };

    return { form, errors, handleSubmit };
  }
});
</script>

<style scoped>
span {
  color: red;
}
</style>
```

## 6.总结

通过本学习文档，你了解了如何在 Vue 3 + TypeScript 中创建和管理表单，包括基本结构、常用属性和事件的使用。此外，示例中展示了如何实现表单验证，以确保用户输入的有效性。掌握这些基本知识后，你可以构建更加复杂和动态的用户输入界面，提升用户体验。希望这份文档对你的学习有所帮助！