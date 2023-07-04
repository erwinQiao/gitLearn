# CellRanger 学习使用

## CellRanger 安装

Cell Ranger 具体的请自行浏览10X Genomics官网 (https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/installation)

### Download and install

Step 1 – Download and unpack the cellranger-7.1.0.tar.gz tar file in any location. In this example, we unpack it in a directory called /opt.
下载安装包，并解压
```
cd /opt

curl -o cellranger-7.1.0.tar.gz "https://cf.10xgenomics.com/releases/cell-exp/cellranger-7.1.0.tar.gz?Expires=1688395510&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9jZi4xMHhnZW5vbWljcy5jb20vcmVsZWFzZXMvY2VsbC1leHAvY2VsbHJhbmdlci03LjEuMC50YXIuZ3oiLCJDb25kaXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE2ODgzOTU1MTB9fX1dfQ__&Signature=QX5o4IxNshixrejV02f2vah81Gp06EoMuYBADTEfTKU-mhjuibhbNOKG1snxM4UU~atVFnrZj1dtWy9-2vYzWi7qk2f5jg9prDMULQsd3W7tIh9PAOb~3U3Wy7p7eRsbKZ7E4yYBEf7~qkyVaVgWcy9EOQJjCZdVMEIVzvW0r6FCCSKB00MinUFxyHvx7iscQCFiIAPcJqs2Wk0HAz0s~Ts25JJthv-3WKU-~2yyk0UCmFP32mLT0uFW9G5KgNvkYIZUTW8A-zJ8Q28-lK82Gn6DUREhTQU0dSteSRiecTSqfqfVQyn~xb8gzT03bFVCTXhyOcdvedRCueuiSxmDPw__&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA"

tar -xzvf cellranger-7.1.0.tar.gz
```

Step 2 – Download and unpack any of the reference data files in a convenient location
下载参考reference
```
#human
curl -O https://cf.10xgenomics.com/supp/cell-exp/refdata-gex-GRCh38-2020-A.tar.gz
 tar -xzvf refdata-gex-GRCh38-2020-A.tar.gz

#Mouse
curl -O https://cf.10xgenomics.com/supp/cell-exp/refdata-gex-mm10-2020-A.tar.gz
tar -xzvf  refdata-gex-mm10-2020-A.tar.gz
```

Step 3 – Prepend the Cell Ranger directory to your $PATH. This will allow you to invoke the cellranger command.
添加路径
```
export PATH=/opt/cellranger-7.1.0:$PATH
```

### Site check script
检验
```
cellranger sitecheck > sitecheck.txt
cellranger upload your@email.edu sitecheck.txt
```

### Verify installation
进行基础测试
```
cellranger testrun --id=tiny

```

