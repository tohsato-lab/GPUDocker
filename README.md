# GPUDocker
## Project Organization

```
    ├── .github/           <- Settings for GitHub.
    │
    ├── data/              <- Datasets.
    │
    ├── environments/       <- Provision depends on environments.
    │
    ├── models/            <- Pretrained and serialized models.
    │
    ├── notebooks/         <- Jupyter notebooks.
    │
    ├── outputs/           <- Outputs.
    │
    ├── src/               <- Source code. This sould be Python module.
    │
    ├── tests/             <- Test codes.
    │
    ├── .flake8            <- Setting file for Flake8.
    ├── .dockerignore
    ├── .gitignore
    ├── LICENSE
    ├── Makefile           <- Makefile used as task runner.
    ├── poetry.lock        <- Lock file. DON'T edit this file manually.
    ├── poetry.toml        <- Setting file for Poetry.
    ├── pyproject.toml     <- Setting file for Project. (Poetry, Black, isort, Mypy)
    └── README.md          <- The top-level README for developers.

```

# 参考
 - [Ascender](https://github.com/cvpaperchallenge/Ascender) ココにエラーの解決策が書いてあるかも

# 使い方
 1. GPUサーバに自分のユーザーを登録しよう
 2. 登録したユーザーでdockerの権限を貰おう。サーバー管理の人に聞いてね
 3. ssh でGPUサーバーにアクセスしよう
 ```
 $ ssh {あなたのユーザー名}@133.19.72.168 -p 1109
 ```
 4. GithubのSSH-keyを登録しよう
 5. 好きな場所このフォルダをクローンして、フォルダを移動しよう
 ```
$ git clone git@...
$ cd GPUDocker
 ```
 6. 

