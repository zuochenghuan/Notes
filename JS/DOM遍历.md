---
title: DOM遍历.md
date: 2018-04-05 01:05:40
tags: JS
---

# DOM遍历

DOM的遍历分为先序遍历，中序遍历， 后序遍历，是三种不同的顺序的遍历方法

三种方法的区别以及原理请参考：

[https://www.jianshu.com/p/456af5480cee](https://www.jianshu.com/p/456af5480cee)

[http://blog.csdn.net/u013468917/article/details/69556547](http://blog.csdn.net/u013468917/article/details/69556547)

**先序：**考察到一个节点后，即刻输出该节点的值，并继续遍历其左右子树。\(根左右\)

**中序：**考察到一个节点后，将其暂存，遍历完左子树后，再输出该节点的值，然后遍历右子树。\(左根右\)

**后序：**考察到一个节点后，将其暂存，遍历完左右子树后，再输出该节点的值。\(左右根\)

这里只说一下用来遍历的方法：这篇[博文](http://www.cnblogs.com/tracylin/p/5220867.html)写了五种先序遍历的方法，优先使用DOM中提供的两个专门用来遍历的方法。

这两个方法在《JavaScript高程》中有详细的介绍：可以参考第12章12.3

## NodeIterator


![](/assets/traversal1.png)



```js
/**
 * 使用DOM2的"Traversal"模块提供的NodeIterator先序遍历DOM树
 * @param node  根节点
 */
function traversalUsingNodeIterator(node){
    var iterator = document.createNodeIterator(node, NodeFilter.SHOW_ELEMENT,null,false);
    var node = iterator.nextNode();
    while(node != null){
        console.log(node.tagName);
        node = iterator.nextNode();
    }
}
```

## TreeWalker

NodeIterator更高级的一个版本，主要使用的`nextNode()`方法

![](/assets/traversal2.png)

```js
/**
 * 使用DOM2的"Traversal"模块提供的TreeWalker先序遍历DOM树
 * @param node  根节点
 */
function traversalUsingTreeWalker(node){
    var treeWalker = document.createTreeWalker(node, NodeFilter.SHOW_ELEMENT,null,false);
    if(node && node.nodeType === 1){
        console.log(node.tagName);
    }
    var node = treeWalker.nextNode();
    while(node != null){
        console.log(node.tagName);
        node = treeWalker.nextNode();
    }
}
```

## 使用DOM扩展的Element Traversal API，递归遍历DOM树

```js
/**
 * 使用DOM扩展的Traversal API提供的新的接口先序遍历DOM树
 * @param node 根节点
 */
function traversalUsingTraversalAPI(node){
    if(node && node.nodeType === 1){
        console.log(node.tagName);
    }
    var i = 0,len = node.childElementCount, child = node.firstElementChild;
    for(; i < len ; i++){
        traversalUsingTraversalAPI(child);
        child = child.nextElementSibling;
    }
}
```



