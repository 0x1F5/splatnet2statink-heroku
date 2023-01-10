# s3s-heroku

## 概要

[heroku](https://jp.heroku.com/home)上で[s3s](https://github.com/frozenpandaman/s3s)を定期実行してSplatoon 3の戦績を[stat.ink](https://stat.ink/)へ自動送信します

このリポジトリは[splatnet2statink-heroku](https://github.com/proshunsuke/splatnet2statink-heroku)をs3s用に改変しました

**splatnet2statink-herokuと違い、iminkAPIを使用するので注意して下さい！**

## 特徴

* ✅ 無料
* ✅ 完全自動

## herokuについて

* [herokuとは？](https://jp.heroku.com/what)を参照
* Freeプランでは小さなアプリケーションを[Free Dyno Hours](https://devcenter.heroku.com/articles/free-dyno-hours)の間使用可能
  * splatnet2statink-herokuを動かしているだけであればFree Dyno Hoursを超えないはず

## s3sについて

* [s3s](https://github.com/frozenpandaman/s3s)を参照

## 使用方法

### s3sに必要な情報を取得する

* [Setup instructions](https://github.com/frozenpandaman/splatnet2statink#setup-instructions)を参考に、一度ローカルでs3sを動かす
* 出力された `config.txt` の内容をherokuでの設定で使用する

### herokuを使用する

* このリポジトリをForkする
* herokuアカウントを作成する
* [Create new app](https://dashboard.heroku.com/new-app)から名前を付けてherokuアプリを作成する
* `Connect to GitHub` から先程Forkしたリポジトリを指定する
* `Settings` タブから
  * `Config Vars` に`config.txt`の内容を登録する
    * `api_key`
    * `acc_loc`
    * `gtoken`
    * `bullettoken`
    * `session_token`
    * `f_gen`
  * `Buildpacks` に `https://github.com/grauwoelfchen/heroku-buildpack-gettext.git` を追加する
* `Resources` タブから
  * `Find more add-ons` より `Heroku Scheduler` を探して追加する
* `Heroku Scheduler` の設定から
  * `Schedule` に `Every 10 minutes` を指定
  * `Run Command` に `./main` を指定
