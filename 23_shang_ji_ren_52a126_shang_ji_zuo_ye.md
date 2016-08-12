# 2.3 上机任务&上机作业

###I. 上机任务：


---



####1. 了解序列文件（fasta和fastq）

http://en.wikipedia.org/wiki/FASTA_format
http://en.wikipedia.org/wiki/FASTQ_format

####2. 学会在Terminal中运行blast和bowtie
####3. 写一个脚本文件 (run.sh)自动并连续运行一个blast任务和一个bowtie任务。
####4.把sam格式转换为bed格式，并在UCSC Genome Browser上浏览。
http://samtools.sourceforge.net/
http://www.genome.ucsc.edu/FAQ/FAQformat.html

https://genome.ucsc.edu/cgi-bin/hgGateway


###II. 上机作业：


---


####1.解释fasta和fastq文件的格式；  并指出两者有什么不同。 
####2. 解释blast输出的结果。
####3. 学会在UCSC Genome Browser上浏览自己上传的bed文件，上交截图。

**注：上传bed文件到Genome Browser浏览时，如果文件过大，或者MT染色体不识别，可以用如下方法：**

``
grep -v chrmt THA1.bed > THA1_new.bed   (输出一个不含chromosome MT的文件）
``

``
grep chrI THA1.bed > THA1_chrI.bed  （输出一个只含chromosome I的文件）
``
