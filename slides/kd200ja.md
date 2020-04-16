Kubernetes Dashboard 2.0.0 リリース!!
=====================================

![Shu Muto](/img/ShuMuto2020-64.png)

2020-4-X [Shu Muto](https://shu-mutou.github.io)

Note:
* [スライドショーで表示](https://shu-mutou.github.io/slideshow.html?md=/slides/kd200ja.md&title=Slideshow&theme=https://shu-mutou.github.io/revealjs-custom-jp.css)

---

## 紹介

* 前回の v1.10 リリースから 1 年半ほどかけて、Angular の 1.x から最新の 9 への移行や、最新の Kubernetes v1.18.1、CRD、HPA、metrics server 対応などを行ってきました。
* また、開発環境コンテナや CI、国際化ワークフローの再構築、ドキュメントの更新なども行ってきました。
* この度、新しい Kubernetes Dashboard v2.0.0 をご紹介できることを大変嬉しく思います。

---

## コンテナーイメージ

* 公式の Kubernetes Dashboard イメージは `k8s.gcr.io` レジストリから Docker Hub の [`kubernetesui/dashboard`](https://hub.docker.com/r/kubernetesui/dashboard) に移動しています。
* また、開発版の `head` イメージもコミットごとに Travis CI から [`kubernetesdashboarddev/dashboard`](https://hub.docker.com/r/kubernetesdashboarddev/dashboard) レジストリに自動でプッシュされます。

---

## インストール

新しい Dashboard をインストールする前に、以前のバージョンを使用していたネームスペースをごと削除します。
```
kubectl delete ns kubernetes-dashboard
```
その後、新しいバージョンの Dashboard をデプロイします。
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

---

## 重要な更新

* Kubernetes Dashboard のフロントエンドは Angular 9 を使用して、完全に書き換えられました。
* Kubernetes v1.18.1 に対応して、依存関係が更新されています。
* ドキュメントは更新の上、[`/docs`](https://github.com/kubernetes/dashboard/tree/master/docs) に移動しました。
* ネームスペースを `kube-system` から `kubernetes-dashboard` に変更しました。
* [`metrics-server`](https://github.com/kubernetes-incubator/metrics-server) からのメトリクスの収集は、新たに作成された [`dashboard-metrics-scraper`](https://github.com/kubernetes-sigs/dashboard-metrics-scraper)` を介して行われます。

---

## 新機能

* Custom Resource Definitions のサポートが追加されました。
* フロントエンドのプラグインサポートが追加されました。[#4094](https://github.com/kubernetes/dashboard/pull/4094), [#4276](https://github.com/kubernetes/dashboard/pull/4276)
* CronJobs の起動オプションが追加されました。
* Horizontal Pod Autoscalers の一覧がデプロイメントの詳細画面に追加されました。[#4625](https://github.com/kubernetes/dashboard/pull/4625)
* グループリソースの画面は非同期で更新されるようになりました。
* リソースの画面更新間隔を設定画面で設定できるようになりました。

---

## セキュリティ

* `Secret` と `ConfigMap` の `CREATE` 権限が削除されました。
* 認証プロキシを使用したときのなりすましヘッダーに対応しました。[#4082](https://github.com/kubernetes/dashboard/pull/4082)
* ログ画面の XSS 脆弱性を解消しました。[#4232](https://github.com/kubernetes/dashboard/pull/4232)
* サーチエンジンのインデキシングをブロックするようになりました。[#4457](https://github.com/kubernetes/dashboard/pull/4457)
* クッキーの `sameSite` に `strict` を設定し、セキュアクッキーを使用するようにしました。[#4877](https://github.com/kubernetes/dashboard/pull/4877)
* TLS の最低バージョンを v1.2 に設定しました。[#5013](https://github.com/kubernetes/dashboard/pull/5013)

---

## 国際化

* 国際化のためのワークフローを Angular と `xliffmerge` を使用して再構築しました。
* 現在サポートされている言語は、フランス語、日本語、韓国語、中国語（簡体字、繁体字）、ドイツ語です。

---

## その他

* 様々なツールを同梱した、ダッシュボードのローカル開発環境を Docker イメージで提供しています。

---

## 謝辞

[2.0.0](https://github.com/kubernetes/dashboard/releases/tag/v2.0.0) のリリースに貢献していただいた、たくさんの[コントリビューター](https://github.com/kubernetes/dashboard/graphs/contributors?from=2018-12-22&to=2020-04-07&type=c)の皆様に心より感謝を捧げます！！

---

## 今後の計画

[2.1.0](https://github.com/kubernetes/dashboard/milestone/2) のマイルストーンが設定されています。
* ログインに使用する kubeconfig にコンテキストが設定されている場合に、これを切り替えられるようにします。[#4522](https://github.com/kubernetes/dashboard/issues/4522), [#4534](https://github.com/kubernetes/dashboard/pull/4534)
* 翻訳対象を ts ファイルまで拡張します。[#4699](https://github.com/kubernetes/dashboard/issues/4699), [#4871](https://github.com/kubernetes/dashboard/issues/4871)

---

# Thanks!

![Shu Muto](/img/QR_shu-mutou.github.io_icon.png)

[Shu Muto](https://shu-mutou.github.io)
