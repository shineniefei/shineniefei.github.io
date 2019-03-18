---
title: linux 压缩解压类 命令
---

# 压解压缩命令

## tar 命令

```
tar xf filename.tar.gz             //解压到当前目录
tar zxvf filename.tar.gz -C exist_folder //解压到指定目录
tar cf filename.tar.gz filename       //压缩文件
tar zcvf filename.tar.gz filename      //压缩文件
```

## unzip

```
unzip filename.zip                 //解压到当前目录  
unzip filename.zip -d folder          //解压到指定目录  
unzip -v filename.zip             //查看zip中文件  
unzip -t filename.zip           //测试是否成功解压，是否完整
```

## zip

```
zip filename.zip filename       //压缩文件  
zip -r filename.zip folder       //压缩文件夹  
zip -r file.zip folder filename.txt    //压缩文件夹和文件  
zip -d file.zip file1                //删除file1
```

## unrar 命令

```
unrar e test.rar               //解压文件到当前目录
unrar    x test.rar /path/to/extract //解压文件到指定目录
unrar l test.rar               //查看rar中的文件
unrar v test.rar               //查看rar文件详细
unrar t test.rar               //测试是否可以成功解压
```

# tar 参数

--------------------------------------------------------------------------------

tar<br>
-c: 建立压缩档案<br>
-x：解压<br>
-t：查看内容<br>
-r：向压缩归档文件末尾追加文件<br>
-u：更新原压缩包中的文件<br>
这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。<br>
-z：有gzip属性的<br>
-j：有bz2属性的<br>
-Z：有compress属性的<br>
-v：显示所有过程<br>
-O：将文件解开到标准输出<br>
下面的参数-f是必须的

## -f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。

```
tar -cf all.tar *.jpg    //将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。

tar -rf all.tar *.gif    //将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。  

tar -uf all.tar logo.gif    //更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。 

tar -tf all.tar    //列出all.tar包中所有文件，-t是列出文件的意思

tar -xf all.tar    //解出all.tar包中所有文件，-x是解开的意思  

tar vtf all.tar.gz  //查看all.tar.gz包中所有文件信息，详细内容
```

## 压缩

```
tar –cvf jpg.tar *.jpg //将目录里所有jpg文件打包成tar.jpg

tar –czf jpg.tar.gz *.jpg
//将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz

tar –cjf jpg.tar.bz2 *.jpg
//将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2

tar –cZf jpg.tar.Z *.jpg
//将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z
```

# rar

```
rar a jpg.rar *.jpg //rar格式的压缩，需要先下载rar for linux
```

# zip

```
zip jpg.zip *.jpg //zip格式的压缩，需要先下载zip for linux
解压
```

# tar

```
tar –xvf file.tar //解压 tar包

tar -xzvf file.tar.gz //解压tar.gz

tar -xjvf file.tar.bz2 //解压 tar.bz2

tar –xZvf file.tar.Z //解压tar.Z
```

# unrar

```
unrar e file.rar //解压rar
```

# unzip

```
unzip file.zip //解压zip
```

# 总结

--------------------------------------------------------------------------------

1. *.tar 用 tar –xvf 解压
2. *.gz 用 gzip -d或者gunzip 解压
3. _.tar.gz和_.tgz 用 tar –xzf 解压
4. *.bz2 用 bzip2 -d或者用bunzip2 解压
5. *.tar.bz2用tar –xjf 解压
6. *.Z 用 uncompress 解压
7. *.tar.Z 用tar –xZf 解压
8. *.rar 用 unrar e解压
9. *.zip 用 unzip 解压

--------------------------------------------------------------------------------

# zip unzip

1. 把/home目录下面的mydata目录压缩为mydata.zip

  ```
  zip -r mydata.zip mydata #压缩mydata目录
  ```

2. 把/home目录下面的mydata.zip解压到mydatabak目录里面

  ```
  unzip mydata.zip -d mydatabak
  ```

3. 把/home目录下面的abc文件夹和123.txt压缩成为abc123.zip

  ```
  zip -r abc123.zip abc 123.txt
  ```

4. 把/home目录下面的wwwroot.zip直接解压到/home目录里面

  ```
  unzip wwwroot.zip
  ```

5. 把/home目录下面的abc12.zip、abc23.zip、abc34.zip同时解压到/home目录里面

  ```
  unzip abc\*.zip
  ```

6. 查看把/home目录下面的wwwroot.zip里面的内容

  ```
  unzip -v wwwroot.zip
  ```

7. 验证/home目录下面的wwwroot.zip是否完整

  ```
  unzip -t wwwroot.zip
  ```

8. 把/home目录下面wwwroot.zip里面的所有文件解压到第一级目录

  ```
  unzip -j wwwroot.zip
  ```

--------------------------------------------------------------------------------

主要参数 -c：将解压缩的结果<br>
-l：显示压缩文件内所包含的文件<br>
-p：与-c参数类似，会将解压缩的结果显示到屏幕上，但不会执行任何的转换<br>
-t：检查压缩文件是否正确<br>
-u：与-f参数类似，但是除了更新现有的文件外，也会将压缩文件中的其它文件解压缩到目录中<br>
-v：执行是时显示详细的信息<br>
-z：仅显示压缩文件的备注文字<br>
-a：对文本文件进行必要的字符转换<br>
-b：不要对文本文件进行字符转换<br>
-C：压缩文件中的文件名称区分大小写<br>
-j：不处理压缩文件中原有的目录路径<br>
-L：将压缩文件中的全部文件名改为小写<br>
-M：将输出结果送到more程序处理<br>
-n：解压缩时不要覆盖原有的文件<br>
-o：不必先询问用户，unzip执行后覆盖原有文件<br>
-P：使用zip的密码选项<br>
-q：执行时不显示任何信息<br>
-s：将文件名中的空白字符转换为底线字符<br>
-V：保留VMS的文件版本信息<br>
-X：解压缩时同时回存文件原来的UID/GID
