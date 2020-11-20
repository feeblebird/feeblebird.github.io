---
title: 不渲染md或html
date: 2020-11-20 08:55:07
tags:
---

# 不渲染md文件

如果想保留原 md 文件后缀要怎么做呢？这就需要在 站点配置文件`_config.yml` 中配置，找到 `skip_render` 参数，开始匹配的位置是基于你的 source_dir 的，一般来说，是你的 source 文件夹下。下面我分别列举几种常见的情况进行说明：

* `skip_render: test/*` 单个文件夹下全部文件

* `skip_render: test/*.md` 单个文件夹下指定类型文件

* `skip_render: test/**` 单个文件夹下全部文件以及子目录

* 多个文件夹以及各种复杂情况：

  ```yaml
  skip_render: README.md
    - `test1/*.html`
    - `test2/**`
  ```

# 不渲染html文件

在不想被渲染的 html 文件最上面添加如下代码:

```html
---
layout:false
---
```

