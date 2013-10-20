---
layout: post
title: "fedora19 on windows8.1 hyper-v"
description: "Windows 8.1のHyper-VにFedora19を入れる作業ログ"
category: "memo"
tags: [hyper-v, fedora]
---
{% include JB/setup %}

Windows 8.1のHyper-VにFedora19を入れる作業ログ。

1. Hyper-Vで仮想マシンを新規作成しようとしたら、第1世代と第2世代を選択するダイアログが。
こんなダイアログはWindows8のときにはなかったはず。
せっかくなので第2世代を選んでみる。

1. ディスクはあえてvhdx使います。

1. fedora19のnetwork install isoを使用。まずはそのままブート...secure boot failedだそうな。

1. 設定のファームウェアでセキュアブートを無効にして再起動。...Secure boot not enabledって言われて停止。あほか。

1. 第2世代はWindowsのことだけ考えて作られた感がするので、あきらめて第1世代で作ることに。

1. GUIが途中で死んだので、ブート時にtabキーを押してtextを追加。テキストモードでインストール。

1. ファイルシステムはbtrfs使っちゃう。

1. minimal installを選んだらエラーっぽいメッセージが表示されたけど、とりあえず無視。yumの依存関係チェックしてる時のエラーっぽい？

1. インストール開始。minimal installでも238個もパッケージ入るのか。

1. 問題なくインストール終了。

1. `ifconfig` そんなコマンドはない。あら。 `yum update` は動くからたぶんネットワークには繋がってると思うけど...

とりあえず動くようにはなったので、あとは必要なパッケージをyumで追加していきゃいいか。
