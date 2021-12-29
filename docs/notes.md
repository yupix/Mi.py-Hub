# 注意事項

このページではmi.pyを使用するべきで注意すべき点を記しています。

## on_mentionを作成した際にmention_commandが動かない

!!! warning
    この機能はv2.0.0で追加されます

以下のようなコードがある場合 `mention_command` デコレーターで作成したコマンドが正常に動作しなくなります。

```python

async def on_mention(self, mention):
    pass

...

@commands.mention_command(regex=r'おはよう(.*)さん')
async def hello_user(self, ctx):
    pass
```

この問題が発生するのは `on_mention` イベントを上書きした際にコマンドを実行するための呼び出しがなくなるためです。
そのため、以下のコードを付け足すことで解消できます

```python
async def on_mention(self, mention):
    ...
    await self.progress_command(mention)
```