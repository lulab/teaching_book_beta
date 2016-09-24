# 2.2 序列比对 - Bowtie

**Bowtie 使用指南**




####I. 基础知识

---



**1. 存储raw reads的文件格式 **

**FASTQ Format** (*.fastq or *.fq)


`
FASTQ format stores sequences and Phred qualities in a single file. It is concise and compact. FASTQ is first widely used in the Sanger Institute and therefore we usually take the Sanger specification and the standard FASTQ format, or simply FASTQ format. Although Solexa/Illumina read file looks pretty much like FASTQ, they are different in that the qualities are scaled differently. In the quality string, if you can see a character with its ASCII code higher than 90, probably your file is in the Solexa/Illumina format.
`

***Example***

```
@EAS54_6_R1_2_1_413_324

CCCTTCTTGTCTTCAGCGTTTCTCC

+

;;3;;;;;;;;;;;;7;;;;;;;88

```
  





**2. 下载index好的基因组文件**

[Download link](http://bowtie-bio.sourceforge.net/tutorial.shtml)

**3.  更多基因组文件格式**

gtf/gff, bed, …

详见
[Reference link](http://genome.ucsc.edu/FAQ/FAQformat.html)

**4.  bowtie程序下载 **

可能已经安装好，尝试输入bowtie回车看看

若未安装，可点击[Download link](http://sourceforge.net/projects/bowtie-bio/files/bowtie/1.0.0/)进行安装



x86_64:  bowtie-1.0.0-linux-x86_64.zip	
i386 or i686 (32): bowtie-1.0.0-linux-i386.zip



####II. Mapping using Bowtie 

---
**以酵母和e.coli基因组为例**

当前工作目录：/home/cs/Bioinfo_Lab/1.Sequence/1.seq_align/bowtie/

命令如下：

```
bowtie  -v  2  -m 10  --best  --strata  ./BowtieIndex/YeastGenome  -f  THA1.fa  -S  THA1.sam
        
bowtie  -v  1  -m 10  --best  --strata  ./bowtie-src/indexes/e_coli  -q  e_coli_1000_1.fq  -S e_coli_1000_1.sam
```


*-v <int>         report end-to-end hits with <=v mismatches; ignore qualities*

*-m <int>        suppress all alignments if > <int> exist (def: no limit)	*

*-M <int>        like -m, but reports 1 random hit (MAPQ=0);  requires --best*

*--best             hits guaranteed best stratum; ties broken by quality*

*--strata           hits in sub-optimal strata aren't reported (requires --best)
*

*-f           	raw reads文件 (fasta)
*

*-q		raw reads  文件（fastaq)     
*

*-S		输出文件名，格式为sam格式
*

####III. 格式转换


---
**
为了便于其它软件(例如IGB)处理，常将sam处理成Bed格式**

命令如下：
 
``` 
perl sam2bed.pl THA1.sam > HA1.bed
```






上传bed文件到Genome Browser浏览时，如果文件过大，或者MT染色体不识别，可以用如下方法：

```
grep -v chrmt THA1.bed > THA1_new.bed   #输出一个不含chromosome MT的文件

grep chrI THA1.bed > THA1_chrI.bed      #输出一个只有chromosome I的文件
```

bed文件格式（tab分隔）：

1. chrom - The name of the chromosome (e.g. chr3, chrY, chr2_random) or scaffold (e.g. scaffold10671).
2. chromStart - The starting position of the feature in the chromosome or scaffold. The first base in a chromosome is numbered 0.
3. chromEnd - The ending position of the feature in the chromosome or scaffold. The chromEnd base is not included in the display of the feature. For example, the first 100 bases of a chromosome are defined as chromStart=0, chromEnd=100, and span the bases numbered 0-99.
The additional optional BED fields are:
4. name - Defines the name of the BED line. This label is displayed to the left of the BED line in the Genome Browser window when the track is open to full display mode or directly to the left of the item in pack mode.
5. score - A score between 0 and 1000. 

