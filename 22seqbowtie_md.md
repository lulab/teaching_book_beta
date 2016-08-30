# 2.2 序列比对 - Bowtie

**Bowtie 使用指南**




####0. 基础知识

---



**1. 存储raw reads的文件格式 **

**FASTQ Format** (*.fastq or *.fq)

Notations

	•	<fastq>, <blocks> and so on represents non-terminal symbols.
	•	Characters in red are regex-like operators.
	•	'\n' stands for the Return key.
Syntax

| **``<fastq>:=<block>+``** |
| -- |
| **``<block>:=@<seqname>\n<seq>\n+[<seqname>]\n<qual>\n ``**|
|**``<seqname>:=[A-Za-z0-9_.:-]+``**|
|**``<seq>:=[A-Za-z\n\.~]+``**|
| **``<qual>:=[!-~\n]+ ``**|




**2. 下载index好的基因组文件**

http://bowtie-bio.sourceforge.net/tutorial.shtml

**3.  更多基因组文件格式**
gtf/gff, bed, …
http://genome.ucsc.edu/FAQ/FAQformat.html

4.  bowtie程序下载 (可能已经安装好，尝试输入bowtie回车看看)

http://sourceforge.net/projects/bowtie-bio/files/bowtie/1.0.0/

x86_64:  bowtie-1.0.0-linux-x86_64.zip	
i386 or i686 (32): bowtie-1.0.0-linux-i386.zip
	（可以通过 uname –a 查看机器类型是64还是32位）



####I. Mapping using Bowtie （以酵母和e.coli基因组为例）

---
命令如下：

bowtie  -v  2  -m 10  --best  --strata  BowtieIndex/YeastGenome  -f  THA1.fa  -S  THA1.sam
        
bowtie  -v  1  -m 10  --best  --strata  bowtie-src/indexes/e_coli  -q  e_coli_1000_1.fq  -S e_coli_1000_1.sam

```
-v <int>         report end-to-end hits with <=v mismatches; ignore qualities

-m <int>        suppress all alignments if > <int> exist (def: no limit)	

-M <int>        like -m, but reports 1 random hit (MAPQ=0);  requires --best

--best             hits guaranteed best stratum; ties broken by quality

--strata           hits in sub-optimal strata aren't reported (requires --best)

-f           	raw reads文件 (fasta)

-q		raw reads  文件（fastaq)     

-S		输出文件名，格式为sam格式
```

####II. 格式转换（为了便于其它软件(例如IGB)处理，常将sam处理成Bed格式）：

---


        
perl     sam2bed.pl    

THA1.sam  >   THA1.bed

Note:  bed文件格式（tab分隔）：
1. chrom - The name of the chromosome (e.g. chr3, chrY, chr2_random) or scaffold (e.g. scaffold10671).
2. chromStart - The starting position of the feature in the chromosome or scaffold. The first base in a chromosome is numbered 0.
3. chromEnd - The ending position of the feature in the chromosome or scaffold. The chromEnd base is not included in the display of the feature. For example, the first 100 bases of a chromosome are defined as chromStart=0, chromEnd=100, and span the bases numbered 0-99.
The additional optional BED fields are:
4. name - Defines the name of the BED line. This label is displayed to the left of the BED line in the Genome Browser window when the track is open to full display mode or directly to the left of the item in pack mode.
5. score - A score between 0 and 1000.
…
上传bed文件到Genome Browser浏览时，如果文件过大，或者MT染色体不识别，可以用如下方法：

grep -v chrmt THA1.bed > THA1_new.bed   (输出一个不含chromosome MT的文件）

grep chrI THA1.bed > THA1_chrI.bed  （输出一个只chromosome I的文件）
