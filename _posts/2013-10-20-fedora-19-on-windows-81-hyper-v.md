---
layout: post
title: "fedora19 on windows8.1 hyper-v"
description: "Windows 8.1のHyper-VにFedora19を入れる作業ログ"
category: "memo"
tags: [hyper-v, fedora]
---
{% include JB/setup %}

Windows 8.1のHyper-VにFedora19を入れる作業ログ。

インストール
------------

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

そして問題なくインストール終了。

設定
----

1.  `ifconfig` そんなコマンドはない。あら。 `yum update` は動くからたぶんネットワークには繋がってると思うけど...
とりあえず動くようにはなったので、あとは必要なパッケージをyumで追加していきゃいいか。

1. `yum install net-tools` で `ifconfig` が使えるように。

1. なんとなく `yum install yum-plugin-fastestmirror`

1. ホスト名なおす。/etc/hostnameと/etc/hosts

1. IPアドレス固定する。/etc/sysconfig/network-scripts/ifcfg-eth0 に、もともとDHCPで設定してる内容に追記する。 

        BOOTPROTO=none
        NETMASK=255.255.255.0
        IPADDR=***ひみつ***
        USERCTL=no

    既存のに書いてあった `BOOTPROTO="dhcp"` はコメントアウト。

1. sshの公開鍵を設定、ログインできることを確認した上で、sshdはパスワード認証を不許可に。

とりあえずこんなところ...あとは適当に
