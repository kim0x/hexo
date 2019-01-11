---
title: Hexo主题Next配置过程
date: 2019-01-11 14:37:01
tags:
  - hexo
page_name: hexo-theme-configure
---
- Next主题是Hexo最受欢迎的主题，主题地址<https://github.com/iissnan/hexo-theme-next>
- 首先在hexo文档中安装Next主题`git clone https://github.com/iissnan/hexo-theme-next.git themes/next `
- 启用next主题,打开文档根目录下的`_config.yml`文件，定位到`theme:`将原主题注释掉，新增`theme: next`保存

<!--more-->

## 配置过程

### 站点配置

- 该过程主要配置文件为根目录下的`_config.yml`文件
  1. 定位到`Site`，根据站点的实际内容修改；
  2. 在设置固定链接时，在`permalink`的最后，新增一项`page_name`用于个性化现实文章的url;
  3. 设置deploy:
  ```
  deploy:
    - type: git
    - repo: git@github.com:kim0x/kim0x.github.io.git
    - branck: master
  ```
  
### 主题配置

- 主题配置主要使用的文件是`themes/next/_config.yml`
1. 修改网站的favicon
  - 将icon文件存放到主题根目录中的sources/images文件夹中
2. 修改网站菜单
  - 定位到Menu Setting,分别启用`home about archives`
  - 在hexo文档根目录中创建一个新的页面`hexo new page about`,将about/index.md的layout设置为page
3. 选择网站布局
  - Next主题提供了4种网站布局`Muse/Mist/Pisces/Gemini`,可以根据需要选择并将其他的布局注释
4. 侧边栏设置
  - 侧边栏可以根据需要开启社交链接和头像avatar
5. 开启文章字数统计功能
  - 安装`hexo-wordcount`在hexo文档根目录下执行`npm install hexo-wordcount`
6. 开启文章版权
   - 文章版权可以使用`CC BY ND 4.0`,协议地址<http://creativecommons.org/licenses/by-nd/4.0>
   - 在文件`layout/_macro/post.swig`的`post-body`末尾处添加以下代码：
```
<div>    
 {# 表示如果不在索引列表中加入后续的HTML代码 #}
 {% if not is_index %}
    <ul class="post-copyright">
      <li class="post-copyright-author">
          <strong>本文作者：</strong>{{ theme.author }}
      </li>
      <li class="post-copyright-link">
        <strong>本文链接：</strong>
        <a href="{{ url_for(page.path) }}" title="{{ page.title }}">{{ page.path }}</a>
      </li>
      <li class="post-copyright-license">
        <strong>版权声明： </strong>
        本网站所有文章除特别声明外，均采用<a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/">知识共享署名-禁止演绎 4.0 国际许可协议</a>进行许可。
      </li>
    </ul>
    <a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nd/4.0/88x31.png" /></a><br />
  {% endif %}
</div>
```
  - 在文件`source/css/_custom/custom.styl`中添加以下代码:
```
.post-copyright {
    margin: 2em 0 0;
    padding: 0.5em 1em;
    border-left: 3px solid #ff1700;
    background-color: #f9f9f9;
    list-style: none;
}
```
7. 设置代码配色方案
  - 代码配色有`noemal|night|night wighties|night blue|night bruight`几种,可以选择`night`模式
8. 开启网站访问统计
  - 使用Leancloud来储存访问信息，在Leancloud中新建一个Counter类，将`app_id`和`app_key`分别填写到配置文件中
9. 开启本地搜索支持
  - 安装支持`npm install hexo-generator-searchdb`
