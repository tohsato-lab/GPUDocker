# GPUDocker 書きかけ

# 参考
 - [Ascender](https://github.com/cvpaperchallenge/Ascender) ココにエラーの解決策が書いてあるかも

# 使い方
 1. GPUサーバに自分のユーザーを登録しよう
 2. 登録したユーザーでdockerの権限を貰おう。サーバー管理の人に聞いてね
 3. ssh でGPUサーバーにアクセスしよう
```shell
 $ ssh {あなたのユーザー名}@GPUのipアドレス -p ポート番号
```
 4. GithubのSSH-keyを登録しよう
 5. 好きな場所このフォルダをクローンして、フォルダを移動しよう
```shell
$ git clone git@...
$ cd GPUDocker
```
 6. dockerファイルを編集しよう
 + GPUDocker/environments/gpu/docker-compose.yaml の３箇所を編集しよう
```
 services:
  YourUserName: # ←ここを{あなたのユーザー名}にしよう
    runtime: nvidia
    container_name: contanor　# ←ここを{あなたのユーザー名}にしよう
...
    ports:
        - hoge:hoge # ←カブらないようにしよう。特に同じユーザーネームのやつとはかぶらないように注意
 
```
 7. dockerのコンテナを立ち上げて中に入ろう
```shell
$ cd /environments/gpu/
$ docker compose up -d
$ docker compose exec {あなたのユーザー名} bash
```

 8. python3の環境を作ろう
```shell
challenger@153a9d49d0a3:~/ascender$ poetry init

This command will guide you through creating your pyproject.toml config.

Package name [ascender]:  ←そのままEnter
Version [0.1.0]:  ←そのままEnter
Description []:  ←そのままEnter
Author [None, n to skip]:  compbio ←好きな名前にしてこの記事では"compbio"
License []:  ←そのままEnter
Compatible Python versions [^3.9]:  ←必要なpython3のバージョン。今回は"3.10"
Would you like to define your main dependencies interactively? (yes/no) [yes] yes ←Yesと入力してEnter
You can specify a package in the following forms:
  - A single name (requests): this will search for matches on PyPI
  - A name and a constraint (requests@^2.23.0)
  - A git url (git+https://github.com/python-poetry/poetry.git)
  - A git url with a revision (git+https://github.com/python-poetry/poetry.git#develop)
  - A file path (../my-package/my-package.whl)
  - A directory (../my-package/)
  - A url (https://example.com/packages/my-package-0.1.0.tar.gz)

Package to add or search for (leave blank to skip): numpy ←パーケージを入れます。一旦Numpyを入れてみる
Found 20 packages matching numpy
Showing the first 10 matches

Enter package # to add, or the complete package name if it is not listed []:
 [ 0] numpy
 [ 1] numpy1
 [ 2] topas2numpy
 [ 3] numpy-serializer
 [ 4] mlphys-numpy
 [ 5] gdal2numpy
 [ 6] numpy-sugar
 [ 7] numpy-dataframe
 [ 8] numpy-ringbuffer
 [ 9] mapchete-numpy
 [ 10] 
 > 0　←NUmpyが複数見つかったので、ほしいやつを選ぶ。今回は0番目
Enter the version constraint to require (or leave blank to use the latest version): 
Using version ^1.26.2 for numpy

Add a package (leave blank to skip):  ←そのままEnter

Would you like to define your development dependencies interactively? (yes/no) [yes]  ←そのままEnter
Package to add or search for (leave blank to skip):  ←そのままEnter

Package to add or search for (leave blank to skip): 

Generated file

[tool.poetry]
name = "ascender"
version = "0.1.0"
description = ""
authors = ["compbio"]
readme = "README.md"

[tool.poetry.dependencies]
python = "3.10"
numpy = "^1.26.2"


[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"


Do you confirm generation? (yes/no) [yes] ←そのままEnter


 
```
