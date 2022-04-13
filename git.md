####  本地文件上传github

- **step1**： D:\data\Flink>git init

> Initialized empty Git repository in D:/data/Flink/.git/

- **step2**： D:\data\Flink>git add .

> warning: LF will be replaced by CRLF in src/main /resources/log4j.properties.
> The file will have its original line endings in your working directory

- **step3**  ：D:\data\Flink>git commit -m "flink demo upload"

> [master (root-commit) ee53d45] flink demo upload
>  11 files changed, 476 insertions(+)
>  create mo de 100644 .idea/.gitignore
>  create mode 100644 .idea/codeStyles/codeStyleConfig.xml
>  create mode 100644 .idea/compiler.xml
>  create mode 100644 .idea/encodings.xml
>  create mode 100644 .idea/misc.xml
>  create mode 100644 .idea/scala_compiler.xml
>  create mode 100644 Flink.iml
>  create mode 100644 pom.xml
>  create mode 100644 src/main/resources/log4j.properties
>  create mode 100644 src/main/scala/com/zwj/BatchJob.scala
>  create mode 100644 src/main/scala/com/zwj/StreamingJob.scala



- **step4**： 进入github主页，新建repository，后生成链接，并复制链接
- **step5**：D:\data\Flink>git remote add origin git@github.com:xiaoyuJane/flink.git

- **step6**：D:\data\Flink>git push -u origin master

> Enumerating objects: 21, done.
> Counting objects: 100% (21/21), done.
> Delta compr ession using up to 8 threads
> Compressing objects: 100% (15/15), done.
> Writing objects: 100% (21/21), 6.22 KiB | 1.04 MiB/s, done.
> Total 21 (delta 1), reused 0 (delta 0), pack-reused 0
> remote: Resolving deltas: 100% (1/1), done.
> To github.com:xiaoyuJane/flink.git

> - [new branch]      master -> master
>   Branch 'master' set up to track remote branch 'master' from 'origin'.