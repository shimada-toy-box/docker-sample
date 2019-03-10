FROM mailhog/mailhog:v1.0.0

# メールデータを保存するボリュームをアタッチするディレクトリを作成する
# ボリュームをアタッチしただけだと書き込み権限がないため、事前にディレクトリを作成して権限を与えておく
RUN mkdir /tmp/mailhog \
 && chmod 777 /tmp/mailhog
