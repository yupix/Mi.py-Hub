# 注意事項

このページではmi.pyを使用するべきで注意すべき点を記しています。

## 受け取ったノートをそのまま送信する（画像がある場合）

!!! tip
    これはMisskeyのドライブで仕様上発生する問題です。

```python
async def on_message(ctx):
    await ctx.send()
```

受け取ったノートをそのままオウム返しにしたい場合があると思います。上記のコードで確かにオウム返しは可能です。
しかしながら、画像がある場合はどうでしょうか？Misskeyではアップロードした画像をユーザーが持っているDriveに関連付けて保存しています。
結果的にオウム返しを行おうとした際に自分のDriveに他人がアップロードした画像のIDが存在しないため、何かテキストやアンケート等の主要なコンテンツが存在しないと以下のようにエラーになります。

```python
async def on_message(ctx):
    await ctx.send()

>>> mi.exception.ContentRequired: ノートの送信にはtext, file, renote またはpollのいずれか1つが無くてはいけません
```

解決策は以下の通りです。

```python
async def on_message(ctx):
    await ctx.add_file(url=ctx.files[0].url).send()
```
`files[0]`の`[0]`は複数ファイルがある場合は先頭のファイルになってしまいますが、今回は1つの画像のみ対応という体で話を進ませていただきます。
そこから、urlを取得し、`add_file`メソッドに`url`引数で渡しそのnoteオブジェクトを送信することで画像が入っていてもオウム返しができるようになります。

!!! todo
    この問題はいずれFrameWork側で対処できるようにする予定があります
