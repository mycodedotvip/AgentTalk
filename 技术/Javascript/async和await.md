`async` 和 `await` 是 JavaScript 中用于处理异步操作的语法，让代码更像同步执行的结构，便于理解和维护。

### 基本概念

- **`async` 关键字**：用于声明一个异步函数，函数返回一个 `Promise` 对象。
- **`await` 关键字**：只能在 `async` 函数内部使用，用于等待一个 `Promise` 完成，直到异步操作完成后再继续执行后续代码。

### 使用场景

- 异步函数通过 `async` 声明，用 `await` 使异步代码看起来像同步代码。
- 常用于等待网络请求、文件读写等需要异步处理的操作。

### 案例 1：最简单的 `async` 和 `await`

```javascript
async function fetchData() {
  return "数据加载成功";
}

async function displayData() {
  const data = await fetchData();  // 等待 fetchData 执行完成
  console.log(data);
}

displayData(); // 输出：数据加载成功
```

在这里，`fetchData` 是一个异步函数，直接返回 `"数据加载成功"` 字符串，但会自动转换为 `Promise`。`displayData` 中用 `await` 等待 `fetchData` 执行完成。

### 案例 2：`await` 等待异步操作

下面是一个实际的异步操作案例，比如模拟等待一个网络请求：

```javascript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getData() {
  console.log("开始请求数据...");
  await delay(2000);  // 等待 2 秒
  console.log("数据获取成功");
}

getData();
```

输出结果：
```
开始请求数据...
（等待 2 秒）
数据获取成功
```

这里的 `delay` 函数会等待一段时间，通过 `await delay(2000);` 暂停 2 秒，让代码显得更像同步执行。`await` 使 `getData` 函数等待 2 秒再执行后面的代码。

### 案例 3：处理 API 请求

以下代码展示了如何用 `async` 和 `await` 处理 API 请求：

```javascript
const fetch = require("node-fetch"); // 使用 node-fetch 模拟网络请求

async function fetchData() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    const data = await response.json();  // 等待解析 JSON 数据
    console.log("获取的数据:", data);
  } catch (error) {
    console.error("获取数据出错:", error);
  }
}

fetchData();
```

在这里：
1. `await fetch()` 发送请求并等待响应。
2. `await response.json()` 解析响应数据为 JSON。
3. `try...catch` 捕获错误，处理请求失败的情况。

### 案例 4：多个 `await` 的顺序执行

如果有多个异步操作，可以使用多个 `await` 顺序执行：

```javascript
async function sequentialTasks() {
  console.log("开始任务 1");
  await delay(1000);
  console.log("任务 1 完成");

  console.log("开始任务 2");
  await delay(2000);
  console.log("任务 2 完成");

  console.log("所有任务完成");
}

sequentialTasks();
```

### 案例 5：并行执行多个异步操作

多个异步任务可以并行执行以节省时间，用 `Promise.all` 来处理：

```javascript
async function parallelTasks() {
  const task1 = delay(1000).then(() => console.log("任务 1 完成"));
  const task2 = delay(2000).then(() => console.log("任务 2 完成"));
  
  await Promise.all([task1, task2]);
  console.log("所有任务完成");
}

parallelTasks();
```

在这里，`task1` 和 `task2` 同时开始，不需要等待彼此。最终输出的顺序为 `任务 1 完成` -> `任务 2 完成` -> `所有任务完成`。
