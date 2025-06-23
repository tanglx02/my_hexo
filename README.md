# my_hexo

**快速恢复我的博客与备份博客**

1、安装 node与npm

2、安装Hexo

```
npm install hexo-cli -g
```

3、安装插件

```
npm install hexo-deployer-git --save

npm i --save hexo-wordcount
```

4、配置git密钥

把JGY里面的ssh密钥文件放到系统家目录`.ssh`下面

查看文件是否存在

```
cat ~/.ssh/id_rsa.pub
```

检查是否配置成功

`ssh -T git@gitee.com`

5、克隆我的hexo

```
git clone git@github.com:tanglx02/my_hexo.git
```

6、复制文章到hexo下

从JGY把source软链接到hexo下

7、创建博客备份脚本

在`~/.bashrc`或`~/.zshrc`中添加

```
alias hs='hexo clean && hexo g && hexo s'
alias hd='hexo clean && hexo g && hexo d && git add . && git commit -m "update" && git push origin main'
```

