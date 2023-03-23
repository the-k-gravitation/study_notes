#github #git

1. 在本地针对每个账号生成一个 SSH Key：

```bash
ssh-keygen -t rsa -C '账号的邮箱地址' -f ~/.ssh/密钥文件名
```

2. 添加私钥

```sh
ssh-add ~/.ssh/所有创建的密钥
```

3. 创建 config 文件
   在 `~/.ssh` 文件夹创建 `config` 文件，并添加如下内容：

```
# 第一个账号
Host 第一个账号名.github.com
HostName github.com
IdentityFile ~/.ssh/第一个账号对象的密钥文件
User git

# 第二个账号
Host 第二个账号名.github.com
HostName github.com
IdentityFile ~/.ssh/第二个账号对象的密钥文件
User git
```

4. 在 github.com 中每个账号上部署上各自的 SSH Key
   分别登陆到各自的 github 账号中，进入 **Personal settings** –> **SSH and GPG keys** 进行部署。

5. 远程测试 sh

```sh
ssh -T 第一个账号名.github.com

ssh -T 第二个账号名.github.com
```

6. 使用
   clone 库到本地：

```sh
# 原本的写：
git clone git@github.com:第一个账号名/库名.git

#改成：
git clone git@第一个账号名.github.com:第一个账号名/库名.git

git clone git@第二个账号名.github.com:第一个账号名/库名.git
```

进入到本地的库中，设置局部的用户名和邮箱：

```hs
git config user.name "第一个账号名";
git config user.email "第一个账号名的注册邮箱";
```
