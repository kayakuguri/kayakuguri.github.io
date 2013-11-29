---
layout: post
title: "Gitblogに投稿するまでの手順メモ"
date: 2013-11-29 13:30:48 +0900
comments: true
categories: 
---

**新しい記事を作成**

  rake new_post['post title']

※ここでのタイトルに日本語は使えない。また、ページのURLにもなる。  
`source/_post/YYYY-MM-DD-title.markdown`というデータが出来上がるので、  
中編集して記事を作成。

**プレビュー**

  rake preview

<http://localhost:4000/>にアクセスすると見れる。`Ctrl+c`で終了。

**記事のアップ**

  rake generate
  rake deploy

または上記２つを１つに

  rake gen_deploy

**ソースをBitbucketにバックアップ**

  git add -A
  git commit -m "add post"
  git push -u bitbucket source


