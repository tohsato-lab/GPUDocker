# GPUDocker

# 参考
 - [Ascender](https://github.com/cvpaperchallenge/Ascender) ココにエラーの解決策が書いてあるかも

# 使い方
 1. GPUサーバにユーザーを登録しよう。{あなたのユーザー名}がこの時のユーザー名になるよ。
 2. 登録したユーザーでdockerの権限を貰おう。サーバー管理の人に聞いてね
 3. ssh でGPUサーバーにアクセスしよう
```shell
 $ ssh {あなたのユーザー名}@GPUのipアドレス -p ポート番号
```
 4. GithubのSSH-keyを登録しよう[参考サイト]( https://qiita.com/shizuma/items/2b2f873a0034839e47ce)
 5. 好きな場所に、このフォルダをクローンして、そこに移動しよう
```shell
$ git clone git@...
$ cd GPUDocker
```
 6. dockerファイルを編集しよう
 + GPUDocker/environments/gpu/docker-compose.yaml の3箇所を編集しよう
```
 services:
  {あなたのユーザー名}: # ←ここを{あなたのユーザー名}にしよう
    runtime: nvidia
    container_name:  {あなたのユーザー名}　# ←ここを{あなたのユーザー名}にしよう
...
    ports:
        - hoge:hoge # ←カブらないようにしよう。特に同じユーザーネームのやつとはかぶらないように注意
 
```
 7. dockerのイメージの作成とコンテナを立ち上げて中に入ろう
```shell
$ cd ./environments/gpu/
$ docker compose build --build-arg USER_NAME={あなたのユーザー名} --build-arg UID="$(id -u)" --build-arg GID="$(id -g)"
$ docker compose up -d
$ docker compose exec {あなたのユーザー名} bash
```

 8. poetryの環境ファイルを作ろう
```shell
:~/ProjectCompbio$ poetry init

This command will guide you through creating your pyproject.toml config.

Package name [ascender]:  ←そのままEnter
Version [0.1.0]:  ←そのままEnter
Description []:  ←そのままEnter
Author [None, n to skip]: compbio ←ユーザー名を入れよう今回は"compbio"そのままEnter
License []:  ←そのままEnter
Compatible Python versions [^3.9]:  ←必要なPython3のバージョンを入れようデフォルトは3.9が入るよ

Would you like to define your main dependencies interactively? (yes/no) [yes] 
You can specify a package in the following forms:
  - A single name (requests): this will search for matches on PyPI
  - A name and a constraint (requests@^2.23.0)
  - A git url (git+https://github.com/python-poetry/poetry.git)
  - A git url with a revision (git+https://github.com/python-poetry/poetry.git#develop)
  - A file path (../my-package/my-package.whl)
  - A directory (../my-package/)
  - A url (https://example.com/packages/my-package-0.1.0.tar.gz)

Package to add or search for (leave blank to skip): ←そのままEnter

Would you like to define your development dependencies interactively? (yes/no) [yes] ←そのままEnter
Package to add or search for (leave blank to skip): ←そのままEnter

Generated file

[tool.poetry]
name = "ascender"
version = "0.1.0"
description = ""
authors = ["compbio"]
readme = "README.md"

[tool.poetry.dependencies]
python = "^3.9" # ここはあなたが指定したバージョンになる


[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"


Do you confirm generation? (yes/no) [yes] ←そのままEnter
```

 9. poetryの実行環境を作ろう
```shell
~/ProjectCompbio$ poetry install --no-root
```

 10. poetryに必要なpythonのパッケージを入れよう。たくさんあると思うが頑張って
```shell
~/ProjectCompbio$ poetry add {必要なPythonのパッケージ名、例：numpy, pandas}
```
 11. poetryを実行しよう
```shell
~/ProjectCompbio$ poetry run python3 {python3のファイル、例：train.py, test.py}
```

