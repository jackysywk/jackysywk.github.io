# 使用 hexo git 备忘录

##  創建新文章
hexo new "文章標題"

```
---
title: 文章標題
date: 2025-04-07 12:00:00
tags: [標籤1, 標籤2]
categories: [分類]
---

這裡寫文章內容...
```

## 啟動本地服務器
hexo server

## 訪問 http://localhost:4000 預覽

## 一鍵部署
hexo clean && hexo generate && hexo deploy

## 或分步執行
hexo clean      # 清理舊文件
hexo generate   # 生成新文件
hexo deploy     # 部署到 GitHub

## 保存源文件到 Git
git add .
git commit -m "更新: 新文章"
git push