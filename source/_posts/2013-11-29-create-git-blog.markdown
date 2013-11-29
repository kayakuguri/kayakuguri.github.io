---
layout: post
title: "Githubでblogをアップするまでのメモ"
date: 2013-11-29 13:05:27 +0900
comments: true
categories: 
---

ここの流れで作成させて頂きました。  
<http://morizyun.github.io/blog/octopress-gitpage-minimum-install-guide/>

もう一つ参考。  
<http://tokkonopapa.github.io/blog/2011/12/30/octopress-on-github-and-bitbucket/>

githubでリポジトリ作成。  
ファーストコミットをgithubの通りに。

そのフォルダに移動して、Octopressの最新版をpull

`bundle install`は、sudoで。

`bundle exec rake install`が実行できない。  
以下エラーが出る

  Could not find rake-0.9.2.2 in any of the sources
  Run `bundle install` to install missing gems.

・解決策(英語)  
[Rails 3.2.1 - Could not find rake-0.9.2.2 in any of the sources](http://stackoverflow.com/questions/9693445/rails-3-2-1-could-not-find-rake-0-9-2-2-in-any-of-the-sources)

**rvm install 1.9.3**らしい。

■RVMをインストール

[Mac book air (Lion) にRVMをインストールする](http://www.slowlydays.net/wordpress/?p=718)  
この方法だと、`rvm 1.24.4`になってる。  
新しすぎてダメ？

RVMを入れてから、もっかいbundle install。  
`sudo bundle install`

なんかエラー出たので、指示に従って、アップデート

  Gem::InstallError: liquid requires RubyGems version >= 1.3.7. Try 'gem update --system' to update RubyGems itself.
  An error occurred while installing liquid (2.3.0), and Bundler cannot continue.
  Make sure that `gem install liquid -v '2.3.0'` succeeds before bundling.

`sudo gem update --system`

もっかい`sudo bundle install`したらいけたっぽい。  
入ったもの一覧  

* rake (0.9.2.2)
* RedCloth (4.2.9)
* chunky_png (1.2.5)
* fast-stemmer (1.0.1)
* classifier (1.3.3)
* fssm (0.2.9)
* sass (3.2.9)
* compass (0.12.2)
* directory_watcher (1.4.1)
* haml (3.1.7)
* kramdown (0.13.8)
* liquid (2.3.0)
* syntax (1.0.0)
* maruku (0.6.1)
* posix-spawn (0.3.6)
* yajl-ruby (1.1.0)
* pygments.rb (0.3.4)
* jekyll (0.12.0)
* rack (1.5.2)
* rack-protection (1.5.0)
* rb-fsevent (0.9.1)
* rdiscount (2.0.7.3)
* rubypants (0.2.0)
* sass-globbing (1.0.0)
* tilt (1.3.7)
* sinatra (1.4.2)
* stringex (1.4.0)
* bundler (1.3.5)

そのうえでもっかいrakeをinstall。  
`sudo bundle exec rake install`

続いて、`sudo bundle exec rake setup_github_pages`とすると、  
`Repository url: `と聞かれたので、その上にある参考の通り、github上のリポジトリURLを入れた。

  https://github.com/your_username/your_username.github.io

[BitBucket](https://bitbucket.org/)にログイン、とあったので、githubアカウントでログイン。  
あとは参考サイトの通りにBitBucketでリポジトリを作成して、githubに関連？づける。

BitBucketでsshキーを登録しておく。  
アカウントの管理、から、SSHキー。  
すでに作成はしていたので、指示にある通り、以下のコマンドでコピー。

  pbcopy < ~/.ssh/id_rsa.pub

ラベルを、id_rsa.pubにしておいた。

で、記事を作ってみて、そのファイルを編集したい、、んだけど、読み取り専用で開いてしまう。  
権限がない。  
いちいちパーミッション変更してたらキリがない。ので、ルート権限でファイルを開く。  
そのプラグイン。  
[sudo.vim](http://sanrinsha.lolipop.jp/blog/2012/01/sudo-vim.html)

最初、`git push -u bitbucket source`をすると、上手く反映されなかったけど、  
上記、SSHキーを登録した後に再度試すと上手くいった。

---

`sudo rake gen_deploy`を実行するも反映されてないっぽい？  

<http://kayakuguri.github.io/>

`rake preview`しても反映されない。  
`rake aborted!`って出てる。

これ？  
<http://stackoverflow.com/questions/13778858/octopress-errors-rake-preview-watch-or-generate>

rubyを1.9.3にしないといけない？  
以下で？

  rvm install ruby-1.9.3-p392

だいぶ時間がかかったけど、アップデートできた。

  Install of ruby-1.9.3-p484 - #complete

次のエラー

  Could not find RedCloth-4.2.9 in any of the sources
  Run `bundle install` to install missing gems.

これ？  
<http://kazukiyunoue-tech.hatenablog.com/entry/2012/12/28/132115>  
違った。。

もっかい、`bundle install`してみると、入ったっぽい。rubyのバージョンを変えたから、  
もう一回インストールし直さないといけなかったのかな？

  Using rake (0.9.2.2)
  Installing RedCloth (4.2.9)
  Installing chunky_png (1.2.5)
  Installing fast-stemmer (1.0.1)
  Installing classifier (1.3.3)
  Installing fssm (0.2.9)
  Installing sass (3.2.9)
  Installing compass (0.12.2)
  Installing directory_watcher (1.4.1)
  Installing haml (3.1.7)
  Installing kramdown (0.13.8)
  Installing liquid (2.3.0)
  Installing syntax (1.0.0)
  Installing maruku (0.6.1)
  Installing posix-spawn (0.3.6)
  Installing yajl-ruby (1.1.0)
  Installing pygments.rb (0.3.4)
  Installing jekyll (0.12.0)
  Installing rack (1.5.2)
  Installing rack-protection (1.5.0)
  Installing rb-fsevent (0.9.1)
  Installing rdiscount (2.0.7.3)
  Installing rubypants (0.2.0)
  Installing sass-globbing (1.0.0)
  Installing tilt (1.3.7)
  Installing sinatra (1.4.2)
  Installing stringex (1.4.0)
  Using bundler (1.3.5)

これでようやく、`rake preview`でエラーが出なくなった！  
なので、<http://localhost:4000/>にアクセス、、するも、真っ白。  
コンソールに出てるログを見ると、404になってるっぽい。

  "GET / HTTP/1.1" 404 - 0.0237

どうやら権限がなくて成功してなかったっぽい。  
`sudo rake preview`で見ると、表示出来た！！

つぎに記事をアップしてみるも、権限エラー。。

  Could not read from remote repository.

公式のSSH作成・登録方法にもとづいて、やり直してみる。  
<https://help.github.com/articles/generating-ssh-keys>

手順にある、`ssh -T git@github.com`でのテストが上手くいかなかった。  
これは、[複数のアカウントでGithubに接続](http://dev.classmethod.jp/tool/github-ssh-sub-account-setting/)、の記事にあった方法を使用しているのだけれど、  
このconfigファイル内の設定で、hostの名前が、`github.com`になってたので、それを`git@github.com`に変更したところ、上手くつながった。

----

何故かどうしても上手くいかないので、  
冒頭のサイトの手順をもう一度やり直した。  
もしかしたら、リポジトリ作った後の最初のプッシュがだめなのかも。。。

どうやらやっぱり、最初のプッシュがダメだったよう。  
そことコンフリクトしていたようで、やり直してみると、上手く通ったっぽい。  
githubにもソース一式がプッシュされた。

しばらくすると反映された！！

やり直しの時には、権限も解消されていたのか、`sudo`もつけずにいけた。
