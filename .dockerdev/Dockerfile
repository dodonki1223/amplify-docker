# 「Vue.jsアプリケーションを Docker 化する」のページを参考にしてDocker化する
#   https://jp.vuejs.org/v2/cookbook/dockerize-vuejs-app.html
FROM node:lts-alpine

# appディレクトリを作成してカレントワーキングディレクトリとして `app` フォルダを指定する
RUN mkdir -p /app
WORKDIR /app

# `package.json` と `package-lock.json` （あれば）を両方コピーする
COPY package*.json ./

# プロジェクトの依存ライブラリをインストールする
RUN npm install

# Amplify CLI のインストール
RUN npm install -g @aws-amplify/cli@4.27.0

# Amplify Mockingで OpenJDK が必要なためJavaのインストールを行う
RUN wget -O /etc/apk/keys/amazoncorretto.rsa.pub  https://apk.corretto.aws/amazoncorretto.rsa.pub \
    && echo "https://apk.corretto.aws/" >> /etc/apk/repositories

# hadolint ignore=DL3018
RUN apk update && apk --no-cache add \
    amazon-corretto-8   

# カレントワーキングディレクトリ(つまり 'app' フォルダ)にプロジェクトのファイルやフォルダをコピーする
COPY . .
