# DOM & BOM

## DOM

> DOM (Document Object Model) is a tree-like structure that represents the structure of a document.
>> W3C推出的标准化DOM可以让任何一种程序设计语言对使用任何一种标记语言编写出来的任何一份文档进行操控。  
>> W3C对DOM的定义是：“一个与系统平台和编程语言无关的接口，程序和脚本可以通过这个接口动态地访问和修改文档的内容、结构和样式。”

* Tree of nodes/elements created by the browser
* JavaScript can be used to read/write/manipulate the DOM
* Object Oriented Representation

### node

node的类型:

* `Document`：整个文档树的顶层节点
* `DocumentType`：doctype标签（exp.`<!DOCTYPE html>`）
* `Element`：网页的各种HTML标签（exp.`<body>`、`<a>`等）
* `Attr`：网页元素的属性（exp.`class="right"`）
* `Text`：标签之间或标签包含的文本
* `Comment`：注释
* `DocumentFragment`：文档的片段

![DOM模型](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/DOM-model.svg/440px-DOM-model.svg.png)

除了根节点，其他节点都有三种层级关系。

* 父节点关系（parentNode）：直接的那个上级节点
* 子节点关系（childNodes）：直接的下级节点
* 同级节点关系（sibling）：拥有同一个父节点的节点

### node接口

#### 属性

!!! summary

    * `element.nodeType`：节点类型
        * `1`：`Element`
        * `2`：`Attr`
        * `3`：`Text`
        * `8`：`Comment`
        * `9`：`Document`
        * `10`：`DocumentType`
        * `11`：`DocumentFragment`
    * `element.nodeName`：节点名称
        * `文档节点（document）`：#document
        * `元素节点（element）`：大写的标签名
        * `属性节点（attr）`：属性的名称
        * `文本节点（text）`：#text
        * `文档片断节点（DocumentFragment）`：#document-fragment
        * `文档类型节点（DocumentType）`：文档的类型
        * `注释节点（Comment）`：#comment
    * `element.nodeValue`：节点的文本值(只有文本节点,注释节点,属性节点有)
    * `element.textContent`: 当前节点和所有后代节点的文本内容
    * `element.ownerDocument`: 所属文档

    <hr/>

    * `element.parentNode`: 父节点.对于一个节点来说，它的父节点只可能是三种类型：元素节点（element）、文档节点（document）和文档片段节点（documentfragment）
    * `element.childNodes`: returns the child nodes of the element
    * `element.children`: returns the children of the element
    * `element.childElementCount`: returns the number of child elements of the element
    * `element.firstChild`: returns the first child node of the element
    * `element.firstElementChild`: returns the first element child of the element
    * `element.lastChild`: returns the last child node of the element
    * `element.lastElementChild`: returns the last element child of the element
    * `element.nextSibling`: returns the next sibling of the element
    * `element.nextElementSibling`: returns the next element sibling of the element
    * `element.previousSibling`: returns the previous sibling of the element
    * `element.previousElementSibling`: returns the previous element sibling of the element

#### 方法

!!! summary

    * `element.createElement(tagName)`: creates an element of the specified tag name
    * `element.createTextNode(text)`: creates a text node with the specified text
    * `element.appendChild(child)`: appends the specified child to the element
    * `element.insertBefore(newChild, referenceChild)`: inserts the specified child before the specified reference child
    * `element.removeChild(child)`: removes the specified child from the element
    * `element.replaceChild(newChild, oldChild)`: replaces the specified old child with the specified new child
    * `element.hasChildNodes()`: returns true if the element has child nodes
    * `element.cloneNode(deep)`: returns a duplicate of the element
    * `element.contains(otherNode)`: returns true if the element contains the specified other node
    * `element.normalize()`: normalizes the element
    * `element.isEqualNode(otherNode)`: returns true if the element is the same node as the specified other node
    * `element.getrootNode()`: returns the root node of the document

### Document节点

!!! summary

    * `document`: the root node of the DOM tree
    * `document.body`: the body element of the document
    * `document.head`: the head element of the document
    * `document.documentElement`: the root element of the document
    * `document.title`: the title of the document
    * `document.location`: the location of the document
    * `document.URL`: the URL of the document
    * `document.referrer`: the referrer of the document
    * `document.cookie`: the cookie of the document
    * `document.lastModified`: the last modified date of the document
    * `document.characterSet`: the character set of the document
    * `document.dir`: the direction of the document
    * `document.doctype`: the doctype of the document
    * `document.all`: the collection of all elements in the document
    * `document.forms`: the collection of all forms in the document
    * `document.links`: the collection of all links in the document
    * `document.images`: the collection of all images in the document
    * ...

### Selectors

!!! summary

    * `document.querySelector(selector)`: returns the first element that matches the specified selector
    * `document.querySelectorAll(selector)`: returns a collection of elements that match the specified selector
    * `document.getElementById(id)`: returns the element with the specified id
    * `document.getElementsByTagName(tagName)`: returns a collection of elements with the specified tag name
    * `document.getElementsByClassName(className)`: returns a collection of elements with the specified class name
    * `document.getElementsByName(name)`: returns a collection of elements with the specified name

### Attributes

!!! summary

    * `element.getAttribute(name)`: returns the value of the specified attribute
    * `element.getAttributeNode(name)`: returns the specified attribute node
    * `element.setAttribute(name, value)`: sets the specified attribute to the specified value
    * `element.hasAttribute(name)`: returns true if the element has the specified attribute
    * `element.hasAttributes()`: returns true if the element has attributes
    * `element.removeAttribute(name)`: removes the specified attribute

### Events

## BOM

## 参考资料

* [🔗网道-JavaScript教程-DOM](https://wangdoc.com/javascript/dom/index.html)
* [🔗事件参考](https://developer.mozilla.org/zh-CN/docs/Web/Events)
