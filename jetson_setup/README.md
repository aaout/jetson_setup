# jetson_setup

[こちら](https://github.com/dusty-nv/jetson-containers)を参考に作成した docker を用いての jetson 環境構築方法です。

以下のパッケージを含む環境を構築することができます。

```python
tensorflow==2.3.1+nv20.11
TensorRT==7.1.3.0
PyCUDA==2020.1
numpy==1.18.5
v4l2
```

全体の流れは[Jetson セットアップマニュアル](https://docs.google.com/presentation/d/1_k0xrD2JAzbs0CmXLibpOElClcySRwRvlrgityWFmZU/edit#slide=id.gd2481a1571_0_26)に記載してあります。

# 手順

1. まず GitHub から clone してファイルをダウンロードします。

   ```bash
   $ git clone https://github.com/Hutzper-inc/jetson_setup.git
   $ cd jetson_setup
   ```

1. ダウンロードしたファイルに実行権限を与えます。

   ```bash
   $ chmod 700 -R scripts run.sh
   ```

1. 追加でパッケージをインストールする必要がある場合はここで Dockerfile を編集してください。

1. 用意された Dockerfile をビルドします。

   ```bash
   $ ./scripts/docker_build_ml.sh tensorflow
   ```

   "Successfully built xxx"と表示されていればビルド完了です。

   最後に"Successfuly tagged yyy:zzz"と表記されており yyy がイメージ名、zzz がタグ名となっています。

1. 次にビルドしたイメージが上手く動作するかテストします。

   第一引数にテストする環境の名前、第二引数にイメージ名:タグ名を指定すると自動でテストが開始され、パッケージが上手くインストールされているか確認できます。

   ```bash
   $ ./scripts/docker_test_ml.sh tensorflow l4t-tensorflow:r32.5.0-tf2.3-py3
   ```

1. 最後にコンテナを走らせて環境構築完了です。

   ```bash
   $ ./run.sh l4t-tensorflow:r32.5.0-tf2.3-py3
   ```

1. 終了する際は以下のコマンドを実行してください。
   ```
   $ exit
   ```
