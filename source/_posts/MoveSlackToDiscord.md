---
title: 如何將Slack頻道和對話紀錄轉移到Discord
date: 2024-05-19 21:47:42
tags:
  - Discord
  - 腳本
  - 機器人
thumbnail: https://firebasestorage.googleapis.com/v0/b/camila-dev-blog.appspot.com/o/DALL%C2%B7E%202024-05-26%2019.12.12%20-%20A%20modern%20digital%20banner%20illustrating%20the%20process%20of%20transferring%20Slack%20channels%20and%20conversations%20to%20Discord.%20The%20banner%20features%20logos%20of%20Slack%20and%20D.webp?alt=media&token=d05d43dc-fbe6-4669-b6e0-ccad7f521a56

excerpt: 如何將 Slack 頻道和對話紀錄轉移到 Discord。內容包括前置準備步驟、建立 Discord 機器人、導出 Slack 資料以及使用 Python 腳本將頻道和對話轉移的過程。
---

說明如何將 Slack 頻道和對話紀錄轉移到 Discord，包含步驟、腳本以及遇到的問題和解決方案。


## 1. 前置準備

#### **下載並安裝 Python 3.x**

[Python 官方網站](https://www.python.org/downloads/)

## **安裝所需的 Python 庫**

打開終端並運行以下命令以安裝必要的 Python 庫：

```bash
pip install discord.py aiohttp certifi
```

## 2. 建立 Discord 機器人

1. 前往 Discord Developer Portal。
2. 點擊「New Application」，創建一個新的應用。
3. 在左側菜單中選擇「Bot」，然後點擊「Add Bot」。
4. 複製機器人的 Token，這將在腳本中使用。

## 3. 導出 Slack 資料

1. 登錄到 Slack 工作區。
2. **前往 `Workspace Settings`**：
    - 點擊工作區名稱以打開Menu，選擇 **`Settings & administration`**，然後點擊 **`Workspace settings`**。
3. **選擇 `Import/Export Data`**：
    - 在 **`Settings`** 頁面中，找到 **`Import/Export Data`** 選項並點擊。
4. **選擇 `Export`**：
    - 選擇要導出的日期範圍，然後點擊 **`Start Export`** 按鈕。這會生成一個包含 JSON 文件的壓縮包。
5. **下載導出的文件**：
    - 將生成的壓縮包下載到電腦，解壓縮後應該會看到包含 **`channels.json`** 等文件。

## 4. 頻道/伺服器腳本

### 攥寫Python腳本

創建一個新的 Python 文件（例如 **`create_discord_channels.py`**），並將以下代碼粘貼到其中。這個腳本將會將 Slack 的頻道和對話轉移到 Discord。

```python
import json
import discord
from discord.ext import commands
import aiohttp
import ssl
import certifi
import asyncio

# 定義你的 Discord 機器人 Token
TOKEN = 'YOUR_DISCORD_BOT_TOKEN'
# 定義你的伺服器 ID
GUILD_ID = 'YOUR_GUILD_ID'  # 替換成你的伺服器 ID

# 讀取 channels.json 文件 # 替換成你的channels.json
with open('path_to_channels.json', 'r') as f:
    channels_data = json.load(f)

# 設置機器人
intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix='!', intents=intents)

# 設置 SSL 上下文以使用最新的憑證
ssl_context = ssl.create_default_context(cafile=certifi.where())

# 自定義的 aiohttp 客戶端會話
async def create_custom_session():
    conn = aiohttp.TCPConnector(ssl=ssl_context)
    session = aiohttp.ClientSession(connector=conn)
    return session

@bot.event
async def on_ready():
    print(f'Logged in as {bot.user}')

    # 打印機器人已加入的所有伺服器名稱
    print("Guilds:")
    for guild in bot.guilds:
        print(f'- {guild.name} (ID: {guild.id})')

    # 獲取目標伺服器
    guild = bot.get_guild(GUILD_ID)
    if guild:
        # 創建頻道
        for channel in channels_data:
            try:
                channel_name = channel.get('name')
                channel_topic = channel.get('topic', '')
                
                # 確保 channel_topic 是字符串
                if isinstance(channel_topic, dict):
                    channel_topic = channel_topic.get('value', '')

                if channel_name:
                    # 檢查頻道是否已存在
                    existing_channel = discord.utils.get(guild.channels, name=channel_name)
                    if not existing_channel:
                        print(f'Creating channel: {channel_name}')
                        await guild.create_text_channel(name=channel_name, topic=channel_topic)
                        print(f'Successfully created channel: {channel_name}')
                    else:
                        print(f'Channel {channel_name} already exists')
            except Exception as e:
                print(f'Failed to create channel {channel_name}: {e}')
    else:
        print('Guild not found')

    # 完成後關閉機器人
    await bot.close()

# 使用自定義會話啟動機器人
async def main():
    session = await create_custom_session()
    try:
        bot.http._HTTPClient__session = session
        await bot.login(TOKEN)
        await bot.connect()
    finally:
        await session.close()

# 啟動事件循環並運行主程序
asyncio.run(main())

```

在終端中運行以下命令來運行腳本：

```bash
python create_discord_channels.py
```

## 5. 常見錯誤

### **1. SSL 憑證錯誤**

如果遇到 SSL 憑證錯誤，請運行以下命令來安裝最新的憑證：

```bash
/Applications/Python\ 3.x/Install\ Certificates.command
```

### **2. 伺服器未找到**

確保已經正確設置了 **`GUILD_ID`**，並在腳本中打印所有伺服器名稱和 ID，以確認機器人已成功加入伺服器。

### **3. 無效的表單主體**

這個錯誤通常是由於 **`topic`** 欄位的值格式不正確導致的。確保 **`topic`** 欄位的值是字符串。如果 **`topic`** 是字典，請提取 **`value`** 欄位中的值。
