# blasr-installation
1、下载源文件
$git clone https://github.com/PacificBiosciences/pitchfork.git

2、安装
$ cd pitchfork
$ make PREFIX=/path/to/install/ blasr

3、加载环境变量和测试
$source setup-env.sh  #可以加到.bashrc文件里
$ blasr -version
$ bam2bax --version
$ bax2bam --version

4、使用

先把 bax.h5文件转换成 bam文件

确保叫 *.metadata.xml的文件在 所有*.bax.h5文件的上一层，开始转换：

$bax2bam *1.bax.h5 *2.bax.h5 *3.bax.h5 -o out

当所有的bax.h5文件生成一个bam文件完后，运行比对

$blasr out.bam  reference.fasta --bam --clipping soft --out alignments.bam --nproc 16

得到比对完的文件alignments.bam

5、用igv查看文件前的准备工作

先用samtools把bam文件排序。

$samtools sort alignments.bam -o aln.sort.bam

index bam文件:

$samtools index aln.sort.bam

6、导入reference.fasta和aaln.sort.bam文件到igv，就可以查看了。
