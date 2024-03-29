# Rubyをインストール
FROM ruby:2.6

# 必要なパッケージをインストール
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs

# 公式では以下のコマンドを推奨しているが、nodeのバージョンが低くBootstrapが使えない
# RUN apt-get update -qq && apt-get install -y nodejs

# 環境変数を設定
ENV APP_HOME /app

# ディレクトリの作成と移動
WORKDIR $APP_HOME

# ホストのGemfileなどをコンテナへコピー
COPY Gemfile $APP_HOME/Gemfile
COPY Gemfile.lock $APP_HOME/Gemfile.lock

# BundlerでGemをインストール
RUN bundle install

# Railsアプリを作成（既存のアプリをマウントする場合は不要）
RUN rails new . --database=mysql

# 設定ファイル書き換え（既存のアプリをマウントする場合は不要）
COPY ./config $APP_HOME/config

# マウントできるように公開
VOLUME /app/public
VOLUME /app/tmp

# コンテナ起動時にRailsサーバを起動
CMD ["rails", "server"]
