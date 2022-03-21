# Anaconda

## 参考資料

* [conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/packages.html)

## command not found (Mac)

```bash
vi ~/.zshrc

export PATH=~/username/anaconda3/bin:$PATH

source ~/.zshrc
```

## パッケージ

### 一覧

`conda list`

### インストール

`conda install <pkg name>`

`conda install -c <channel name> <pkg name>`

## 仮想環境

### 作る

`conda create --name <environment name> python=<python version>`

### 仮想環境一覧

`conda env list`

### activate

`source activate <environment name>`

### deactivate

`source deactivate`

## 設定値

### channel一覧

`conda config --show channels`

### channel追加

`conda config -add channels <channel name>`

### channel優先順位

`conda config --get channels`
