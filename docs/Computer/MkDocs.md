---
title: MkDocs 用你的markdown文档生成静态网站
tags: [computer]
---

## MkDocs介绍
MkDocs is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file. 
用于给markdown格式的项目文档创建静态网站.  
官网地址:https://www.mkdocs.org/

### Material for MkDocs is a powerful documentation framework on top of MkDocs, a static site generator for project documentation
In 2016, Material for MkDocs started out as a simple theme for MkDocs, but over the course of several years, it's now much more than that – with the many built-in plugins, settings, and countless customization abilities, Material for MkDocs is now one of the simplest and most powerful frameworks for creating documentation for your project.  
官网地址:https://squidfunk.github.io/mkdocs-material/

### Installation 安装
```
pip install mkdocs-material
```
### Creating your site 创建站点
```
mkdocs new .
```
This will create the following structure:
```
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

### Configuration 配置
Simply add the following lines to mkdocs.yml to enable the theme:
```
theme:
  name: material
```
### Previewing as you write 预览
```
mkdocs serve 
```
### Building your site 生成站点
```
mkdocs build
```



### 以下是我安装的插件及配置
安装两个额外的插件mermaid2、roamlink
```
pip install mkdocs-mermaid2-plugin
pip install mkdocs-roamlinks-plugin
```

修改mkdocs.yml
```yaml
site_name: NgaanWai

copyright: Copyright © 2024
theme:
  name: material

  palette:
    # Palette toggle for automatic mode
    - media: "(prefers-color-scheme)"
      toggle:
        icon: material/link
        name: Switch to light mode

    # Palette toggle for light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: grey
      toggle:
        icon: material/toggle-switch
        name: Switch to dark mode

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: black
      toggle:
        icon: material/toggle-switch-off
        name: Switch to system preference

  features:
    - content.code.annotate
    - content.code.copy
    - search.highlight
    - search.share
    - search.suggest

plugins:
  - search
  - roamlinks

extra:
  generator: false

markdown_extensions:
  - pymdownx.superfences:
      # make exceptions to highlighting of code:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:mermaid2.fence_mermaid_custom

```

### github自动部署
Using GitHub Actions you can automate the deployment of your project documentation. At the root of your repository, create a new GitHub Actions workflow, e.g. .github/workflows/ci.yml, and copy and paste the following contents:
```
name: ci 
on:
  push:
    branches:
      - master 
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
      - uses: actions/cache@v4
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material 
      - run: pip install mkdocs-mermaid2-plugin
      - run: pip install mkdocs-roamlinks-plugin
      - run: mkdocs gh-deploy --force
```


### see also 相关参考
#### tags 标签页面
实现tags功能只需要两步:
1. 在`mkdocs.yml`中添加
```yml
plugins:
  - tags:
      tags_file: tags.md
```
2. 在docs文件夹下新建`tags.md`文件