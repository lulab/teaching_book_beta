# 2.1 序列比对 - Blast


**Blast 使用指南**

---



####0. 基础知识

**1. 存储sequence的常用文件格式**

**FASTA格式** （*.fasta or *.fa )

\>gi|47115317|emb|CAG28618.1| VIM [Homo sapiens]   MSTRSVSSSSYRRMFGGPGTASRPSSSRSYVTTSTRTYSLGSALRPSTSRSLYASSPGGVYATRSSAVRL

`
The word following the ">" symbol is the identifier of the sequence, and the rest of the line is the description (optional). Normally, identifiers are simply protein accession, name or Entrez gi's (e.g., Q5I7T1, AG10B_HUMAN, 129295), but a bar-separated NCBI sequence identifier (e.g., gi|129295) will also be accepted. Any arbitrary user-specified sequence identifier can also be used (e.g., CLONE00073452).
`

**2. 安装blast及其子程序 **

(可能已经安装好，尝试输入blastn回车看看)

blastn, blastp，blastx, …
    
**安装方式1 **（自动安装，推荐方式）：

Linux自动安装软件方法： sudo apt-get install  软件名称  （密码：cs）

比如：   sudo apt-get install ncbi-blast+   (密码：cs)

**安装方式2 **（手动下载安装文件）：

下载链接：[ ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/]( ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/)

寻找类似如下文件：

a. 32位计算机（老机器）安装文件：如 ncbi-blast-2.2.28+-ia32-linux.tar.gz   

b. 64位机器安装文件： 如   ncbi-blast-2.2.28+-x64-linux.tar.gz

（可以通过 uname –a 查看机器类型是64还是32位）

**3. 阅读命令帮助**

一般下载的程序：   blastn –h， or  blastn --help

Linux原生命令或程序：  man ls

**4. 进入工作目录**

进入工作目录的方法:

		cd          （cd后面为空时，进入默认家目录）
        
		cd 工作目录名称     （推荐时常敲敲TAB键盘）
        
一般的程序后面都要输入文件位置和名称，告知程序输入和输出是什么：

	    ./filename   (当前目录下的文件)
             
		../filename  （上一级目录下的文件）  ../../filename  （上两级目录下的文件）
        
####I. Pairwise alignment (两条序列比对)

---



** Protein sequence alignment**

Note：VIM.fasta 与 NMD.fasta 分别是金属beta酶家族的两个亚种酶的序列

文件位置：/home/cs/Bioinfo_Lab/1.Sequence/1.seq_align/blast/protein/


```
blastp  -query ./VIM.fasta  -subject   ./NMD.fasta   -out output.blastp
```

** DNA sequence alignment**

Note：H1N1-HA.fasta 与H7N9-HA.fasta 是流感病毒序列文件

文件位置：/home/cs/Bioinfo_Lab/1.Sequence/1.seq_align/blast/dna

``
blastn  -query ./H1N1-HA.fasta -subject ./H7N9-HA.fasta  -out output.blastn
``


####II.  一条序列与远程序列库比对

** Protein sequence alignment  比对远程pdb数据库**

blastp  -query    ./protein/VIM.fasta  -db   pdb      -remote -out protein_remote.blastp
	
** DNA sequence alignment  比对远程nr数据库**

blastn  -query    ./dna/H1N1-HA.fasta    -db  nr    -remote   -out dna_remote.blastn


###III. 一条序列在自定义的序列库里比对 
---


(例如：在yeast基因组序列中搜索)：




**Step 1: 建库**


(先清空一下之前的残留文件： rm database/*)    

makeblastdb -dbtype nucl -in dna/YeastGenome.fa -out database/YeastGenome


        -dbtype:待建库的类型 （nucl, prot)  
        -in:待建库的序列文件     
        -out:序列库名前缀

**Step 2: 比对**

      blastn -query ./dna/Yeast.fasta -db database/YeastGenome -out Yeast.blastn
