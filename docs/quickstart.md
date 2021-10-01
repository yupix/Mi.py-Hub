# クイックスタート

このページではcommandFrameWorkを使わない小規模に向いている方法を用いて簡潔にBotを作成します。

```python
import mi

client = mi.Client()

@client.event
async def on_ready(ws):
    print(f'{client.i.name}にログインしました')

@client.listener
async def on_message(ctx):
    print(f'{ctx.author.name}さんがノートしました: {ctx.text}')

if __name__ == '__main__':
    client = client.run(uri='url', token='token')
```

めんどくさいという方のためにまず最初に完成品を起きました。このコードが意味するのは以下の通りです。  
1. 3行目でclientインスタンスを作成しています。  
2. 5, 6行目ではeventデコレーターを用いてbotの起動を知らせるための `on_ready` 関数を用意しています
3. 9, 10行目ではlistenerデコレーターを用いてノートが投稿された際に発火する`on_message`関数を用意しています  
4. 最後に`client.run`でBotを起動します

これで簡単なBotが作成できるはずです。