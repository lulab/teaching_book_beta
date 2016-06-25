#Linux基础

**Linux基础和基因组注释文件解读**

###I. 上机任务
---

####1. 了解基因组注释文件 (gff/gtf)

**1.1 了解gff和gtf文件格式**

[http://www.genome.ucsc.edu/FAQ/FAQformat.html](http://www.genome.ucsc.edu/FAQ/FAQformat.html)

**1.2 下载yeast的基因组注释文件**

首先
```bash
wget ftp://ftp.ensembl.org/pub/mnt2/release-77/gtf/saccharomyces_cerevisiae/*.gtf.gz
或者
wget ftp://ftp.ensembl.org/pub/mnt2/release-77/gtf/saccharomyces_cerevisiae/*
```

然后
```bash
gunzip *.gtf.gz
```



**1.3 统计所下载gff/gtf文件的大小，行数和exon数目**

命令示范：

```bash
man ls
ls -al *.gtfwc -l *.gtfcut -f 3 *.gtf | sort | uniq -c
```


####2. 学会使用一个文本编辑器(vi, nano, emacs)编辑新的文件

写一个可执行文件，寻找长度最长的3个exon, 汇报其长度。

命令示范：       

```vi run.sh``` -->

rush.sh的文件内容：
    
    #!/bin/bash  （可能系统不同有差异，也可尝试省略次行语句）
```bash
grep exon *.gtf | awk '{print $5-$4+1}' | sort -n | tail -3
chmod +x run.sh./run.sh
```



###II. 上机作业：
---

1. 查找、理解并注释上述每一个语句和参数的意义

2. 解释gtf/gff文件中$5和$4代表什么，exon长度应该是$5-$4+1还是$5-$4？

3. 有新的方法加分，但必须注释清楚每个语句和参数的意义和结果。

