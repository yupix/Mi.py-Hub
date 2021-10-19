# よくある質問

これは `Mi.py` や拡張モジュールに対しての来るであろう質問などをまとめたものです。プルリクエストなどによって追加なども是非是非お願いします。

## 質問

- Q. on_messageを使用したらcogに登録しているコマンドが動かなくなりました
    - A. これは[v0.2.6](/changelogs/v0.2.5_to_v0.2.6/)から発生するようになった物です。 commandFrameWorkで`on_message`を使用するとMi.
      py側の`on_message`にあるデフォルトの動作が上書きされ消えてしまうことによりこの問題が発生します。解決するにはコードを以下のように変更してください。
```python
async def on_message(self, ctx: Note):
  await self.process_commands(ctx) # 一番うしろに付け足す
```
    

