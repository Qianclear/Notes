

# Apache的下载安装

1. 进入官网http://httpd.apache.org/download.cgi

2. 点击  a number of third party vendors 

   <img src="ipic/1636790042514.png" alt="1636790042514" style="zoom:67%;" />

3.  找到Downloading Apache for Windows

   点击ApacheHaus链接

   <img src="ipic/1636790119579.png" alt="1636790119579" style="zoom:67%;" />

4. 选择x64，下载

   <img src="ipic/1636790215884.png" alt="1636790215884" style="zoom:67%;" />

5.  保存到想要保存的位置，解压压缩包

6.  打开httpd.conf文件(D:\devInstall\Apache24\conf路径下)

   修改Apache安装目录 

   <img src="ipic/1636790676999.png" alt="1636790676999" style="zoom:67%;" />

7. 管理员身份cmd，然后

   ```"D:\devInstall\Apache24\bin\httpd.exe" -k install -n apache```

   <img src="ipic/1636790921459.png" alt="1636790921459" style="zoom:67%;" />

8. 出现了一旦问题，端口占用

9. 进入```D:\devInstall\Apache24\logs``` ，打开日志文件install.log，查看443，发现是ssl端口

   再进入```D:\devInstall\Apache24\conf``` ，打开 httpd.conf ，查找ssl，

   <img src="ipic/1636806300967.png" alt="1636806300967" style="zoom:67%;" /> 

   发现引用了httpd-ahssl.conf文件，打开那个文件，查找443

   <img src="ipic/1636806505509.png" alt="1636806505509" style="zoom:67%;" />

   <img src="ipic/1636806485732.png" alt="1636806485732" style="zoom:67%;" />

   全部更改为442，保存退出

10. 本来啊，依照教程本来该

    ```
    卸载:
    	httpd -k uninstall
    安装:
    	httpd -k install
    ```

    诶嘿，但是呢，又出bug了，卸载出了问题，它找不到卸载对象。。。

11. 最后的最后，我进服务里面刷新了一下，它居然又能用了！

    