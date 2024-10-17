如果不使用 Jinja2 模板，而是实现前后端分离的解决方案，你可以通过 Flask 提供 API 接口，前端使用框架（如 React、Vue.js 或 Angular）来构建用户界面。以下是实现步骤：

### 1. 创建 Flask API

在 Flask 中，定义 RESTful API 接口以处理前端请求。例如：

```python
from flask import Flask, jsonify, request

app = Flask(__name__)

# 示例数据
data = [
    {"id": 1, "name": "Item 1"},
    {"id": 2, "name": "Item 2"},
]

@app.route('/api/items', methods=['GET'])
def get_items():
    return jsonify(data)

@app.route('/api/items', methods=['POST'])
def add_item():
    new_item = request.json
    data.append(new_item)
    return jsonify(new_item), 201

if __name__ == '__main__':
    app.run(debug=True)
```

### 2. 前端应用

使用前端框架（如 Vue.js 或 React）创建用户界面。这些框架通过 HTTP 请求调用 Flask 提供的 API。

#### 示例使用 Vue.js

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>前端应用</title>
</head>
<body>
    <div id="app">
        <ul>
            <li v-for="item in items" :key="item.id">{{ item.name }}</li>
        </ul>
        <button @click="addItem">添加项</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                items: []
            },
            mounted() {
                this.fetchItems();
            },
            methods: {
                fetchItems() {
                    fetch('/api/items')
                        .then(response => response.json())
                        .then(data => {
                            this.items = data;
                        });
                },
                addItem() {
                    const newItem = { id: this.items.length + 1, name: `Item ${this.items.length + 1}` };
                    fetch('/api/items', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                        },
                        body: JSON.stringify(newItem),
                    }).then(() => {
                        this.fetchItems();
                    });
                }
            }
        });
    </script>
</body>
</html>
```

### 3. 部署

- 在生产环境中，可以将 Flask 和前端应用分别部署在不同的服务器或同一服务器的不同端口。
- 使用代理（如 Nginx）来处理跨域请求和静态文件服务。

### 4. 处理跨域问题

如果前后端分离，前端和后端可能在不同域下，需处理跨域请求（CORS）。可以使用 Flask-CORS：

```bash
pip install flask-cors
```

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # 启用 CORS
```

### 总结

通过以上步骤，你可以在 Flask 中实现前后端分离的架构，使用 Flask 提供 API 接口，前端框架负责用户界面的渲染和交互。这种方式具有更好的灵活性和可扩展性。
