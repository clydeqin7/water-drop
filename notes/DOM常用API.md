# DOM常用API

## 基本概念

### DOM

**DOM**( **Document Object Mode**)，**文档对象模型**。它是一种跨平台的、独立于编程语言的API，它把HTML、XHTML或XML文档当作一个树结构，而每个节点视为一个对象，这些对象可以被编程语言操作，进而改变文档的结构，映射到文档的显示。

> MDN:[文档对象模型 (DOM) ](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Introduction)是HTML和XML文档的编程接口。它提供了对文档的结构化的表述，并定义了一种方式可以使从程序中对该结构进行访问，从而改变文档的结构，样式和内容。DOM 将文档解析为一个由节点和对象（包含属性和方法的对象）组成的结构集合。简言之，它会将web页面和脚本或程序语言连接起来。
>
> API (web 或 XML 页面) = DOM + JS (脚本语言)

### Node

Node是一个接口，许多DOM类型从这个接口继承，继承其方法和属性如`Document`, `Element`。

#### 重要属性

**Node.nodeType**属性可用来区分不同类型的节点，比如 [`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element), [`文本`](https://developer.mozilla.org/zh-CN/docs/Web/API/Text) 和 [`注释`](https://developer.mozilla.org/zh-CN/docs/Web/API/Comment)。

| 常量                                 | 值    | 描述                                       |
| ---------------------------------- | ---- | ---------------------------------------- |
| `Node.ELEMENT_NODE`                | `1`  | 一个 [`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 节点，例如 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p) 和 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div)。 |
| `Node.TEXT_NODE`                   | `3`  | [`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 或者 [`Attr`](https://developer.mozilla.org/zh-CN/docs/Web/API/Attr) 中实际的  [`文字`](https://developer.mozilla.org/zh-CN/docs/Web/API/Text) |
| `Node.PROCESSING_INSTRUCTION_NODE` | `7`  | 一个用于XML文档的 [`ProcessingInstruction`](https://developer.mozilla.org/zh-CN/docs/Web/API/ProcessingInstruction) ，例如 `<?xml-stylesheet ... ?>` 声明。 |
| `Node.COMMENT_NODE`                | `8`  | 一个 [`Comment`](https://developer.mozilla.org/zh-CN/docs/Web/API/Comment) 节点。 |
| `Node.DOCUMENT_NODE`               | `9`  | 一个 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 节点。 |
| `Node.DOCUMENT_TYPE_NODE`          | `10` | 描述文档类型的 [`DocumentType`](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentType) 节点。例如 `<!DOCTYPE html>`  就是用于 HTML5 的。 |
| `Node.DOCUMENT_FRAGMENT_NODE`      | `11` | 一个 [`DocumentFragment`](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentFragment) 节点 |



> http://luopq.com/2015/11/30/javascript-dom/
>
> https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Introduction
>
> https://zhuanlan.zhihu.com/p/22184194
>
> http://harttle.land/2015/10/01/javascript-dom-api.html	