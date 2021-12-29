# CommandFrameWorkを用いたBot開発

さて、このページではCommandFrameWorkを用いたBotの開発方法をご紹介します。

## どんな人に向いているのか

- 大規模なBot Projectである
- [quickstart](/quickstart)のやり方では満足できない
- ファイルを分けたい

!!!tip
    Discord.pyを過去に使用したことがある人なら何一つ違和感なく使用することができると思います。

## 例

ファイル構造

```
project ┬ main.py  
        ┴ cogs ─ basic.py
```

main.py

```python
from mi.ext.commands import Bot

INITAL_EXTENSIONS = ["cogs.basic"]


class ExampleBot(Bot):
    def __init__(self, command_prefix:str):
        super().__init__(command_prefix=command_prefix)
        for cog in INITAL_EXTENSIONS:
            self.load_extension(cog)

    async def on_ready(self, ws):
        print(f'{client.i.username}にログインしました')

    async def on_message(self, note):
        print(note.content)

if __name__ == '__main__':
    bot = ExampleBot('!')

```

cogs/basic.py

```python
from mi import Note
from mi.ext import commands


class BasicCog(commands.Cog):
    def __init__(self, bot):
        self.bot = bot

    @commands.mention_command(regex=r'おはよう(.*)さん')
    async def hey(self, ctx: Note):
        print(ctx.content)

    @commands.Cog.listener()
    async def on_message(self, ctx):
        print(ctx.text)


def setup(bot):
    bot.add_cog(BasicCog(bot))
```

これで ノート `!hey テキスト` が来た際にテキストを表示することができました