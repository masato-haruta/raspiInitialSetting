# raspiInitialSetting
Ansibleで以下の内容がRaspberry Piに反映されるサンプルです。

- apt-get update, dist-upgrade, autoremove, autoclean
- install pkgs
  -  git
  - vim
  - wget
  - wicd-curses
  - tightvncserver
  - screen
  - tree
  - hdparm
  - speedtest-cli
- local:ja_JP.UTF-8
- timezone: Asia/Tokyo
- memory split: 16
- hostname: raspberrypi
- wifi country: JP

## Requirement
- ansible 2.3 or later

## Usage
以下URLのRaspbianをインストールしたRaspberry Piを準備する
http://ftp.jaist.ac.jp/pub/raspberrypi/raspbian/images/raspbian-2018-06-29/

本プロジェクトをクローン
```
git clone https://github.com/masato-haruta/raspiInitialSetting.git
cd raspiInitialSetting
```

初期設定のままなので必要に応じてIPアドレスやhostnameに書き換える

```conf:inventory
[raspberrypi]
raspberrypi.local # set your environment(exsample: 192.168.3.2 etc..)
```

ssh関連も初期設定のままなので必要に応じて書き換える

```conf:inventory
[raspberrypi:vars]
ansible_ssh_port=22 # set your environment
ansible_ssh_user=pi # set your environment
ansible_ssh_pass=raspberry # set your environment
```

以下でAnsible実行

```
ansible-playbook site.yml -v
```

ansible sshpass errorが出た場合は以下をインストール

```
brew install http://git.io/sshpass.rb
```

インストールパッケージの追加修正削除は`roles/apt/defaults/main.yml`で行う

raspbianのシステム設定に関する追加修正削除は`roles/sys/defaults/main.yml`で行う
