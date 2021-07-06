# Dockerとは
アプリケーションやミドルウェアがすでにセットアップされている状態の仮想環境を簡単に用意できるプロダクト。
Dockerを使わないと、仮想環境上に本番環境と同じOSをセットアップし、ドキュメントを参考にパッケージマネージャを操作して必要なものを入れていく・・・という面倒臭い作業をいちいち行わなければならない。
### コンテナ型仮想化技術
 Dockerはコンテナ型仮想化技術を利用している。この技術自体はDocker以前から存在している。コンテナ仮想化技術では仮想化ソフトウェアなしにOSのリソースを隔離し、仮想OSにする。この仮想OSをコンテナと呼ぶ。
 
### Dockerfileによるコンテナ情報のコード管理
``` Dockerfile
FROM ubuntu:16.04
​
COPY helloworld /usr/local/bin
RUN chmod +x /usr/local/bin/helloworld
​
CMD ["helloworld"]
```
```FROM ubuntu:16.04```
- ベースとなるDockerイメージ（OS）をFROMで定義。
​
`COPY helloworld /usr/local/bin`
- 作成したhelloworldをホスト側からDockerコンテナ内の/usr/local/binにコピーしている。
​
`RUN chmod +x /usr/local/bin/helloworld`
- Dockerコンテナ内で任意のコマンドを実行できる仕組み。FROMで定義したOSのなかで実行する命令と捉えている。
​
`CMD ["helloworld"]`
- 出来上がったイメージをDockerコンテナとして実行する前に行われるコマンドを定義している。事実上アプリケーションを実行するコマンドを指定することになる。
