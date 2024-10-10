# 表格 Table

## 概述

在现代 Web 应用程序中，表格是展示和管理数据的重要组件。Vue 3 提供了一种简洁的方式来创建动态表格，支持数据的呈现、排序、过滤和分页。结合 TypeScript，可以提高代码的类型安全性和可维护性。

## 基本结构

### 1. 创建基本表格

下面是一个简单的表格示例，用于显示用户信息：

```vue
<template>
  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>用户名</th>
        <th>邮箱</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="user in users" :key="user.id">
        <td>{{ user.id }}</td>
        <td>{{ user.username }}</td>
        <td>{{ user.email }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

interface User {
  id: number;
  username: string;
  email: string;
}

export default defineComponent({
  setup() {
    const users = ref<User[]>([
      { id: 1, username: 'Alice', email: 'alice@example.com' },
      { id: 2, username: 'Bob', email: 'bob@example.com' },
      { id: 3, username: 'Charlie', email: 'charlie@example.com' }
    ]);

    return { users };
  }
});
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
}

th {
  background-color: #f2f2f2;
}
</style>
```

### 2. 表格的基本结构解析

- **`<table>`**: 用于创建表格。
- **`<thead>`**: 表头部分，定义列标题。
- **`<tbody>`**: 表体部分，包含数据行。
- **`v-for`**: 循环渲染每一行数据。

## 属性

### 常用属性

- **`border`**: 表示是否显示边框（HTML属性）。
- **`cellspacing`**: 定义单元格之间的空白（HTML属性）。
- **`cellpadding`**: 定义单元格内容与边框之间的空白（HTML属性）。

### 示例：添加属性

```vue
<table border="1" cellpadding="10">
```

## 事件

### 常用事件

- **`@click`**: 点击事件，可以用于行点击处理。
- **`@mouseover` / `@mouseout`**: 鼠标悬停和移出事件，可用于高亮行等效果。

### 示例：处理事件

```vue
<tr v-for="user in users" :key="user.id" @click="handleRowClick(user)">
  <td>{{ user.id }}</td>
  <td>{{ user.username }}</td>
  <td>{{ user.email }}</td>
</tr>

<script lang="ts">
const handleRowClick = (user: User) => {
  console.log('Selected user:', user);
};
</script>
```

## 高级特性

### 1. 排序功能

可以添加排序功能，通过点击表头进行排序：

```vue
<th @click="sortBy('username')">用户名</th>

<script lang="ts">
const sortBy = (key: keyof User) => {
  users.value.sort((a, b) => (a[key] > b[key] ? 1 : -1));
};
</script>
```

### 2. 过滤功能

通过输入框过滤表格数据：

```vue
<input type="text" v-model="searchTerm" placeholder="搜索用户" />

<tbody>
  <tr v-for="user in filteredUsers" :key="user.id">
    <td>{{ user.id }}</td>
    <td>{{ user.username }}</td>
    <td>{{ user.email }}</td>
  </tr>
</tbody>

<script lang="ts">
const searchTerm = ref('');

const filteredUsers = computed(() => {
  return users.value.filter(user =>
    user.username.toLowerCase().includes(searchTerm.value.toLowerCase())
  );
});
</script>
```

## 使用示例

以下是一个增强版的表格示例，添加了排序和搜索功能：

```vue
<template>
  <div>
    <input type="text" v-model="searchTerm" placeholder="搜索用户" />
    <table>
      <thead>
        <tr>
          <th @click="sortBy('id')">ID</th>
          <th @click="sortBy('username')">用户名</th>
          <th @click="sortBy('email')">邮箱</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in filteredUsers" :key="user.id" @click="handleRowClick(user)">
          <td>{{ user.id }}</td>
          <td>{{ user.username }}</td>
          <td>{{ user.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue';

interface User {
  id: number;
  username: string;
  email: string;
}

export default defineComponent({
  setup() {
    const users = ref<User[]>([
      { id: 1, username: 'Alice', email: 'alice@example.com' },
      { id: 2, username: 'Bob', email: 'bob@example.com' },
      { id: 3, username: 'Charlie', email: 'charlie@example.com' }
    ]);
    
    const searchTerm = ref('');

    const filteredUsers = computed(() => {
      return users.value.filter(user =>
        user.username.toLowerCase().includes(searchTerm.value.toLowerCase())
      );
    });

    const sortBy = (key: keyof User) => {
      users.value.sort((a, b) => (a[key] > b[key] ? 1 : -1));
    };

    const handleRowClick = (user: User) => {
      console.log('Selected user:', user);
    };

    return { users, searchTerm, filteredUsers, sortBy, handleRowClick };
  }
});
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
}

th {
  background-color: #f2f2f2;
  cursor: pointer;
}

th:hover {
  background-color: #e0e0e0;
}
</style>
```

## 总结

通过本学习文档，你了解了如何在 Vue 3 + TypeScript 中创建和管理表格，包括基本结构、常用属性和事件的使用。此外，示例中展示了如何实现排序和过滤功能，以增强用户体验。掌握这些基本知识后，你可以构建更加复杂和动态的数据展示界面，提升用户交互体验。希望这份文档对你的学习有所帮助！