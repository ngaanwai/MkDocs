---
title: MkDocs
tags: [computer]
---

## MkDocs介绍
MkDocs is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file. 
用于给markdown格式的项目文档创建静态网站.

## let's do!项目搭建
### 在github创建仓库
我这里创建的仓库名为:MkDocs

### 新建文件夹
```
mkdir Mkdocs
cd Mkdocs
```
### 本地仓库
```
echo "# MkDocs" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:ngaanwai/MkDocs.git
git push -u origin main
```
新建`.gitignore`文件忽略除docs、mkdocs.yml、.gitignore、.github之外的所有文件
```
vim .gitignore
```
```
/*
!/docs
!/mkdocs.yml
!/.gitignore
!/.github
```

### 虚拟环境
```
python3 -m venv ~/documents/mkdocs
source ~/Documents/mkdocs/bin/activate
```
### mkdocs
```
pip install mkdocs-material
mkdocs new .
```

安装插件mermaid2
```
pip install mkdocs-mermaid2-plugin
```
安装插件roamlink
```
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




### 自动部署
在mkdocs目录新建`.github/workflows/github_actions.yml`
```
mkdir -p ~/documents/mkdocs/.github/workflows
vim ~/documents/mkdocs/.github/workflows/github_actions.yml
```
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
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
      - uses: actions/cache@v3
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

### git push
```
git add .
git commit -m '2nd deploy'
git push
```


## see also 相关参考
### tags 标签页面
实现tags功能只需要两步:
1. 在`mkdocs.yml`中添加
```yml
plugins:
  - tags:
      tags_file: tags.md
```
2. 在docs文件夹下新建`tags.md`文件