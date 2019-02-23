# ウェブサイト内のURL一覧を取得する
以下のコマンドでウェブサイト内のURL一覧を取得できる。  

```bash
$ wget $url --spider -F -nd -r -l 3 -R js,css,png,jpg,gif,txt,pdf,mp3,mp4,exe 2>&1 \
    | grep -Eo 'https?://[^ ]+' \
    | sed -e 's/\?.+$//g' \
    | sed -e 's/\/$//g' \
    | sort
    | uniq -i
```

## `--spider`
コンテンツの存在だけを確認する（HEADリクエストを投げる）。  

## `-l 3`
再帰的に取得する回数。  

## `-R js,css,...`
除外する拡張子一覧。  

## その他
`--wait`オプションや`--random-wait`オプションを使ってサーバーへの負荷を抑えられる。  

## 参考
- [wget - UNIX/Linuxコマンド - IT専科](http://www.itsenka.com/contents/development/unix-linux/wget.html)