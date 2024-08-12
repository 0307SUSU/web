###  递归

>  给定一个值，根据这个值去数组中找出对应的元素，将对应元素中的所有id属性值以数组的形式输出，并且数组元素id的顺序按由外到内的顺序排列

- 要从嵌套数组中找到给定值对应的元素，并提取其所有 `id` 属性值按由外到内的顺序排列，我们可以使用递归方法遍历数组。

```js
const data = [{
    id: 330000,
    parentId: null,
    areaName: "浙江省",
    areaPath: "/浙江省/",
    childNode: [{
        id: 330100,
        parentId: 330000,
        areaName: "杭州市",
        areaPath: "/浙江省/杭州市/",
        childNode: [{
            areaName: "上城区",
            areaPath: "/浙江省/杭州市/上城区/",
            childNode: [],
            id: 330102,
            parentId: 330100
        }]
    }]
}];

function findPathById(arr, targetId) {
    let path = [];
    
    function findNode(node, targetId) {
        if (node.id === targetId) {
            path.unshift(node.id);
            return true;
        }
        if (node.childNode) {
            for (let child of node.childNode) {
                if (findNode(child, targetId)) {
                    path.unshift(node.id);
                    return true;
                }
            }
        }
        return false;
    }
    
    for (let item of arr) {
        if (findNode(item, targetId)) {
            break;
        }
    }
    return path;
}

const targetId = 330102;
const result = findPathById(data, targetId);
console.log(result); // [330000, 330100, 330102]
```

### 数组的各种方法

