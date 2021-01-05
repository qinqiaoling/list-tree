# list-tree-
list结构转换成tree结构

### 数组数据
```
var list = [
　　{id:1,pid:0,name:'一级'},
　　{id:2,pid:1,name:'一级1'},
　　{id:3,pid:1,name:'一级2'},
　　{id:4,pid:2,name:'一级1-1'}
]
```

### 核心代码：
```
// 数组转treefunction composeTree(list = []) {
  const data = JSON.parse(JSON.stringify(list)) // 浅拷贝不改变源数据
  const result = []
  if (!Array.isArray(data)) {
    return result
  }
  data.forEach(item => {
    delete item.children
  })
  const map = {}
  data.forEach(item => {
    map[item.id] = item
  })
  data.forEach(item => {
    const parent = map[item.pid]
    if (parent) {
      (parent.children || (parent.children = [])).push(item)
    } else {
      result.push(item)
    }
  })
  return result
}
```

### 调用方法：
let tree = composeTree(list)

### 打印tree:
```
console.log(tree) // [{"id":1,"pid":0,"name":"一级","children":[{"id":2,"pid":1,"name":"一级1","children":[{"id":4,"pid":2,"name":"一级1-1"}]},{"id":3,"pid":1,"name":"一级2"}]}]
```

![转换tree结构的图片](https://img2018.cnblogs.com/blog/1170608/201907/1170608-20190705093403150-381463261.png)

