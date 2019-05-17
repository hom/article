#### 在 CentOS、Fedora 和 RHEL上
```bash
$ curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
```

#### 接下來你可以很簡單的使用以下指令安裝
```bash
$ sudo yum install yarn
## 或是 ##
$ sudo dnf install yarn
```

#### 執行命令來測試 Yarn 是否安裝：
```bash
$ yarn --version
```