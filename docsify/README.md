
# 看官网



<!-- tabs:start -->
#### **官网地址**
```javascript
https://docsify.js.org/#/plugins
```
#### **我做好的配置**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="description" content="Description">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0">
  <!-- <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css"> -->
  <!-- Theme: Simple -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple.css">
  
<style>
  :root {
    /**分页标签样式*/
    --docsifytabs-border-color: #ededed;
    --docsifytabs-tab-highlight-color: purple;

    /**
     下面是左右分栏的自定义样式
    */
      /* Document */
        --docsify-example-panels-document-width: 90%;

      /* Wrapper */
      --docsify-example-panels-wrapper-width: 100%;

      /* Standards */
      --docsify-example-panels-padding-inner : 8px 16px;
      --docsify-example-panels-padding-surroundings : 0px;

      /* Panel Left */
      --docsify-example-panels-left-panel-background : transparent;
      --docsify-example-panels-left-panel-width : 60%;

      /* Panel Right */
      --docsify-example-panels-right-panel-background : transparent;
      --docsify-example-panels-right-panel-width : 40%;

      /* Titles */
      --docsify-example-panels-title-background: transparent;
  }
</style>

</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: '',
      repo: '',
      maxLevel: 3,
      tabs: {
        persist    : true,      // default
        sync       : true,      // default
        /**
        theme
            Type: string|boolean
            Accepts: 'classic', 'material', false
            Default: 'classic'
        */
        theme      : 'material', // default
        tabComments: true,      // default
        tabHeadings: true       // default
      },
      pagination: {
        previousText: '上一章节',
        nextText: '下一章节',
        crossChapter: true,
        crossChapterText: true,
      },
      search: {
        maxAge: 86400000, // 过期时间，单位毫秒，默认一天
        // 支持本地化
        placeholder: '搜索',
        noData: '没有数据',
        // 搜索标题的最大程级, 1 - 6
        depth: 3
      }
    }
  </script>
  <!-- Docsify v4 -->
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>

    <!-- docsify-tabs tab分页标签 (latest v1.x.x) -->
  <script src="https://cdn.jsdelivr.net/npm/docsify-tabs@1"></script>

  <!-- docsify-example-panels 左右分栏 (latest) -->
  <script src="https://cdn.jsdelivr.net/npm/docsify-example-panels"></script>

    <!-- docsify-pagination 前后一页  -->
    <script src="//unpkg.com/docsify-pagination/dist/docsify-pagination.min.js"></script>

    <!--搜索-->
    <script src="//unpkg.com/docsify/lib/plugins/search.js"></script>
    
</body>
</html>

```

<!-- tabs:end -->

<br/>
<br/>
<br/>
**Docsify 的各种第三方工具 直接官网（非常齐全）**