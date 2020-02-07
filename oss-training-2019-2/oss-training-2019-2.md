# 第２回勉強会 Githubハンズオン


---

## 目次

- アカウント作成
- 公開鍵の登録
- リポジトリ作成
- コード公開
- Issue作成
- PR作成

---

# アカウント作成

---

## アカウント作成①

https://github.com/join にアクセスする。
![](/oss-training-2019-2/img/1-01.PNG)

---

## アカウント作成②

以下の情報を入力し、「Select a plan」ボタンをクリックする。
- Username: 任意のユーザ名
- Email address: メールアドレス
- Password: 任意のパスワード

---

## アカウント作成③

「Individual」料金プランの「Choose Free」ボタンをクリックする。
![](/oss-training-2019-2/img/1-02.PNG)

---

## アカウント作成④

アンケートに回答して「Complete setup」ボタンをクリックする。
![](/oss-training-2019-2/img/1-03.PNG)

---

## アカウント作成⑤

![](/oss-training-2019-2/img/1-04.PNG)
↑の画面が表示されるので、「アカウント作成①」で入力したメールアドレス宛に送信されたメールの「Verify email address」をクリックする。

---

# 公開鍵の登録

---

## 公開鍵の登録①

gitコマンドを使える環境で、以下のコマンドを実行してSSH Keyを作成する。

```
$ ssh-keygen -t rsa -C "<「アカウント作成①」で入力したメールアドレス>"
```

---

## 公開鍵の登録②

https://github.com/settings/keys にアクセスして、「New SSH key」をクリックする。
![](/oss-training-2019-2/img/1-05.PNG)

---

## 公開鍵の登録③

以下の情報を入力し、「Add SSH key」ボタンをクリックする。
- Title: 任意の公開鍵の名前
- Key: 「公開鍵の登録①」で作成された `~/.ssh/id_rsa.pub` の内容

---

# 公開鍵の登録④

公開鍵が登録されていることを確認する。
![](/oss-training-2019-2/img/1-06.PNG)

---

# リポジトリ作成

---

## リポジトリ作成①

画面右上の「＋」→「New Repository」をクリックする。
![](/oss-training-2019-2/img/2-01.PNG)

---

## リポジトリ作成②

以下の情報を入力し、「Create repository」ボタンをクリックする。
- Repository name: 任意のリポジトリ名。例）test-repo1
- Description: リポジトリの説明（オプション）
- Public/Private: リポジトリの公開/非公開設定。今回は「Public」を選択する。プライベートリポジトリは1人1個のみ無料で作成可能。
- Initialize this repository with a README : チェックを入れるとREADMEファイルが自動で生成される。今回はチェックを **入れない** 。

---

# コード公開

---

## コード公開①

以下のコマンドを実行して、ユーザ設定を行う。
```
$ git config --global user.name <ユーザ名>
$ git config --global user.email <メールアドレス>
```
以下のコマンドを実行して、プロキシ設定を行う。
```
$ git config --global http.proxy http://proxy.example.com:8080
$ git config --global https.proxy http://proxy.example.com:8080
```

---

## コード公開②

以下のコマンドを実行して、作成したリポジトリをcloneする。
```
$ git clone https://github.com/<ユーザ名>/<リポジトリ名>.git
```

---

## コード公開③

`README.md` ファイルを作成する。
```
hello, world!
```

---

## コード公開④

作成した `README.md` をコミットする。
```
$ git init
$ git add README.md
$ git commit -m "my 1st commit"
```
リモートリポジトリにpushする
```
$ git push origin master
```

---

## コード公開⑤

https://github.com/<ユーザ名>/<リポジトリ名> にアクセスし、 `README.md` が作成されていることを確認する。

---

# issue作成

---

## issue作成①

issueとは、バグや追加機能などを管理するためのもの。
バグ報告や追加機能提案などを行いたい場合は、issueの作成を行う。

---

## issue作成②

https://github.com/YuikoTakada/oss-training-20200306/issues にアクセスし、「New issue」ボタンをクリックする。
![](/oss-training-2019-2/img/3-01.PNG)

---

## issue作成③

以下の情報を入力し、「Submit new issue」ボタンをクリックする。
- Title: 任意のタイトル。例）test issue 1
- Leave a comment: issueの内容。
    - 例）
    ```
    - [ ] no `file1.txt`
    - [ ] no `file2.txt`
    ```
    - コメントはmarkdown記法で書くことが可能。「Preview」タブで表示を確認することができる。

---

# PR作成

---

## PR作成①

PRとはPull Requestの略。バグ修正や機能追加のコードをリポジトリに取り込んでほしい場合は、PRの作成を行う。

---

## PR作成②

PR投稿先のリポジトリをフォークする。
https://github.com/YuikoTakada/oss-training-20200306 にアクセスし、画面右の「Fork」ボタンをクリックする。
![](/oss-training-2019-2/img/4-01.PNG)

---

## PR作成③

「Clone or download」ボタンをクリックし、表示されるURLをコピーする（URLの横のボタンをクリックするとコピーできる）
![](/oss-training-2019-2/img/4-01.PNG)
以下のコマンドを実行して、作成したforkをローカルにcloneする。
```
$ git clone ↑でコピーしたリポジトリのURL
$ cd oss-training-20200306/
```

---

## PR作成④

PR投稿先のリポジトリを「upstream」という名前でリモートリポジトリに登録する。
```
$ git remote add upstream \
https://github.com/YuikoTakada/oss-training-2019-2.git
```
「uptream」に直接pushしないように設定する。
```
$ git remote set-url --push upstream no_push
```
確認。
```
$ git remote -v
origin  https://github.com/<ユーザ名>/oss-training-20200306.git (fetch)
origin  https://github.com/<ユーザ名>/oss-training-20200306.git (push)
upstream        https://github.com/kubernetes/kubernetes.git (fetch)
upstream        no_push (push)
```

---

## PR作成⑤

以下のコマンドを実行してローカルのmasterブランチを最新にする。
```
$ git fetch upstream
$ git checkout master
$ git rebase upstream/master
```

---

## PR作成⑥

以下のコマンドを実行してブランチを作成する。
```
$ git checkout -b fix-issue1
```

---

## PR作成⑦

以下のコマンドを実行して、作成したブランチとupstreamブランチを同期する。
```
$ git fetch upstream
$ git rebase upstream/master
```

---

## PR作成⑧

file1.txtを作成する。
```
file1
```
file2.txtを作成する。
```
file2
```

---

## PR作成⑨

以下のコマンドを実行して、作成したファイルをコミット対象にする。
```
$ git add file1.txt file2.txt
```

---

## PR作成⑩

以下のコマンドを実行して、作成したファイルをリポジトリにローカルリポジトリにコミットする。

```
$ git commit -m "Fix issue #1"
```

---

## PR作成⑪

以下のコマンドを実行して、作成したファイルをリモートリポジトリに送信する。
```
$ git push origin fix-issue1
```

---

## PR作成⑫

表示されたURLにアクセスして、以下の情報を入力し、「Submit new pull request」ボタンをクリックする。
- Title: 任意のタイトル
- Leave a comment: PRの内容。
    - 例）
    ```
    Close: #<issueの番号>
    ```
![](/oss-training-2019-2/img/4-03.PNG)

---

## 付録①

githubの認証をSSH鍵で行いたい場合は、`.ssh/config` ファイルを作成する。
```
Host github.com
    User git
    HostName ssh.github.com
    IdentityFile ~/.ssh/id_rsa
    Port 443
    ProxyCommand nc --proxy-type http --proxy proxy.example.com:8080 %h %p
```

---

## 付録②

githubでは2要素認証を設定することが可能です。詳細は下記をご参照ください。

https://help.github.com/ja/github/authenticating-to-github/configuring-two-factor-authentication

---