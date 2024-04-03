# FROM ruby:2.7.4
# RUN apt-get update -qq && \
#     apt-get install -y build-essential \
#                        libpq-dev \
#                        nodejs

# RUN mkdir /app
# WORKDIR /app
# COPY Gemfile /app/Gemfile
# COPY Gemfile.lock /app/Gemfile.lock
# RUN gem install bundler
# RUN bundle install --without test development
# ADD . /app
# EXPOSE 3000

# 使用するRubyのバージョンを指定
FROM ruby:2.7.4

# 必要なパッケージのインストール
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

# アプリケーションディレクトリを作成
WORKDIR /myapp

# ホストのGemfileとGemfile.lockをコンテナにコピー
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock

# Bundlerを介してGemをインストール
RUN bundle install --without test development

# ホストの現在のディレクトリからコンテナの作業ディレクトリにファイルをコピー
COPY . /myapp

# コンテナがリッスンするポート番号を指定
EXPOSE 3000

CMD ["/bin/sh", "-c", "bundle exec rails db:create && bundle exec rails db:migrate && bundle exec unicorn -p 3000 -c /app/config/unicorn.rb -E production"]