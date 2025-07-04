# Terraform_Tutorial
macでの操作を前提
NGINXサーバー立ち上げまで

### homebrewによるインストール
```
$ brew tap hashicorp/tap
$ brew install hashicorp/tap/terraform
```

### 最新のTerraformにしたいなら
```
$ brew update
$ brew upgrade hashicorp/tap/terraform
```

### タブ補完の有効化
```
$ terraform -install-autocomplete
```

### docker起動
```
$ open -a Docker
```

### 任意のフォルダ作成
```
$ mkdir learn-terraform-docker-container
$ cd learn-terraform-docker-container
```

### terraform設定ファイル作成
```main.tf
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.13.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 8000
  }
}
```

### プロジェクト初期化
```
$ terraform init
```

### NGINXサーバーのコンテナをセットアップ
「yes」を入力
```
$ terraform apply
```
