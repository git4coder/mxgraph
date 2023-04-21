# mxGraph for Vue.js

改动：

* 将 mxPopupMenu 和 mxToolTip 移入 .container (默认添加在 body 中，在 Vue 项目中看不到)

## 用法

```shell
yarn add mxgraph4vue
```

```html
<div ref="graph_container" class="graph-container"></div>

<style lang="scss" scoped>
.graph-container {
  position: relative;
  height: 400px;
}
</style>
```

```js
import * as mxgraph from 'mxgraph4vue';
import 'mxgraph4vue/javascript/src/css/common.css';
const {
  mxGraph,
  mxUtils,
  mxHierarchicalLayout,
  mxCellOverlay,
  mxEvent,
  mxRubberband,
  mxKeyHandler,
  mxConstants,
  mxImage,
} = mxgraph();

export default {
  mounted() {
    let graph = new mxGraph(this.$refs.graph_container);
    let root = graph.getDefaultParent();
    graph.getModel().beginUpdate();
    try
    {
      let v1 = graph.insertVertex(root, null, 'Hello,', 20, 20, 80, 30);
      let v2 = graph.insertVertex(root, null, 'World!', 200, 150, 80, 30);
      let e1 = graph.insertEdge(root, null, '', v1, v2);
    }
    finally
    {
      graph.getModel().endUpdate();
    }
  },
}
```

Vue 3:

1. 将`import * as mxgraph from 'mxgraph4vue';`改为`import mxgraph from 'mxgraph4vue';`，build 后需要到编译后的`.js`文件中搜索`=mxgraph$1()`替换为`=mxgraph$1.default()`。

1. 需要在入口 index.html 中添加（防止出现 `ReferenceError: * is not defined` 导致项目跑不起来）：

```
window.mxLoadResources = null;
window.mxForceIncludes = null;
window.mxResourceExtension = null;
window.mxLoadStylesheets = null;
```

----
----

*NOTE 09.11.2020* : Development on mxGraph has now stopped, this repo is effectively end of life.

Known forks:

https://github.com/jsGraph/mxgraph

https://github.com/process-analytics/mxgraph

mxGraph
=======

mxGraph is a fully client side JavaScript diagramming library that uses SVG and HTML for rendering.

The PHP model was deprecated after release 4.0.3 and the archive can be found [here](https://github.com/jgraph/mxgraph-php).

The unmaintained npm build is [here](https://www.npmjs.com/package/mxgraph)

We don't support Typescript, but there is a [project to implement this](https://github.com/process-analytics/mxgraph-road-to-DefinitelyTyped), with [this repo](https://github.com/hungtcs/mxgraph-type-definitions) currently used as the lead repo.

The mxGraph library uses no third-party software, it requires no plugins and can be integrated in virtually any framework (it's vanilla JS).

Getting Started
===============

In the root folder there is an index.html file that contains links to all resources. You can view the documentation online on the [Github pages branch](https://jgraph.github.io/mxgraph/). The key resources are the JavaScript user manual, the JavaScript examples and the JavaScript API specificiation.

Support
=======

There is a [mxgraph tag on Stack Overflow](http://stackoverflow.com/questions/tagged/mxgraph). Please ensure your questions adhere to the [SO guidelines](http://stackoverflow.com/help/on-topic), otherwise it is likely to be closed.

If you are looking for active support, your better route is one of the commercial diagramming tools, like [yFiles](https://www.yworks.com/products/yfiles-for-html) or [GoJS](https://gojs.net/latest/index.html).

History
=======

We created mxGraph in 2005 as a commercial project and it ran through to 2016 that way. Our USP was the support for non-SVG browsers, when that advantage expired we moved onto commercial activity around draw.io. mxGraph is pretty much feature complete, production tested in many large enterprises and stable for many years.

Over time you can expect this codebase will break features against new browser releases, it's not advised to start new projects against this codebase for that reason.
