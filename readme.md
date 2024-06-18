# Lua Language Server用 AviUtl関連ライブラリ定義ファイル
https://github.com/LuaLS/lua-language-server で使うための、拡張編集などが提供するライブラリの定義ファイルです

## 使い方
[VSCodeの Lua 拡張機能](https://marketplace.visualstudio.com/items?itemName=sumneko.lua) は既にインストールされていますね？

ワークスペースの`settings.json`に以下を加えると良い感じです
```json
{
  "files.associations": {
    "*.anm": "lua",
    "*.cam": "lua",
    "*.obj": "lua",
    "*.scn": "lua",
    "*.tra": "lua",
  },
  "[lua]": {
    "files.encoding": "shiftjis"
  },
  "Lua.workspace.library": [
    "exedit.luaなどへのパス"
  ],
  "Lua.runtime.version": "LuaJIT"
}
```

## 注
複数の任意引数を取る`obj.draw`のような関数を以下のように定義しています
#### 意図
```
obj.draw([x[,y[,z]]])
```
#### 定義
```lua
function obj.draw()end

---@param x number
function obj.draw(x)end

---@param x number
---@param y number
function obj.draw(x,y)end

---@param x number
---@param y number
---@param z number
function obj.draw(x,y,z)end
```
これは、`x?`を使うと*Lua Language Server*に`nil`を許すことにされるからで、拡張編集はこれを許さないために一つ一つ定義することにしています


## ライセンス
WTFPL2
