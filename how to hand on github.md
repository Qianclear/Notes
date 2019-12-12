# 安装略过....

.

首先看文件夹位置（可称之为仓库）  

使用

>git init(初始化仓库)  

在仓库里创建文件...  

打开git gui....再打开git bash并输入

>git status  

使用

>git add 文件名  

点击GUI里的commit提交，然后在bash 里输入

>git commit -m “必要的文字说明”  

再次键入

>git status  

## 下一步推送

在文件生成目录>.ssh里用bash键入  

> ssh-keygen -t rsa -C "email@email.com"  

  

## 建立密匙

将id_rsa.pub里文字输入，保存

## 上传

bash里分别键入

> git remote add....
>
> git push....

(建立密匙成功后...or push an existing ........下的两行东西)

## 刷新 OVER

