FROM tomcat:8.5.49-jdk8-openjdk

# 必要なパッケージをインストールする
RUN apt-get update && \
    apt-get -y install expect patch

# shibbolethの設定ファイル生成用Dockerコンテナで生成されたファイルをコンテナにコピーする
ADD customized-shibboleth-idp /opt/shibboleth-idp

# Shibbolethのビルド用ファイルをコンテナにコピーする。
COPY bin/build.sh /usr/local/bin/

# ビルドの結果作成されたidp.warをTomcatのwebappsディレクトリにコピーする。
RUN chmod 755 /usr/local/bin/build.sh && \
    /usr/local/bin/build.sh && \
    cp /opt/shibboleth-idp/war/idp.war /usr/local/tomcat/webapps
