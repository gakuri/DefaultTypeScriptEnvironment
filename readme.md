## 前提

* node.js インストール済み
* typescript をグローバルでインストール済み

## 手順

### 1. package.jsonの用意

Ctrl + @ でターミナル起動

```terminal
npm init -y
```

### 2. tsconfig.jsonの用意

```terminal
tsc --init
```

### tsconfig.json の修正

debugの有効化  
"sourceMap": true のコメントアウトを解除

### 4. ビルドタスクの設定

vscメニューの`terminal` -> `configure Default Build Task` を選択し、  
`tsc: build - tsconfig.json`を選択

できあがった`tasks.json`のtasks要素に`"label": "build", `を追加する

```json
{
    "tasks": [
        {
+            "label": "build", // 追加
            "type": "typescript",
            "tsconfig": "tsconfig.json",
            "problemMatcher": [
                "$tsc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

### 5. 起動設定

左の右向き三角形＋虫マークのボタンを押し、`create a launch.json file`をクリックし、
node.jsを選択する

launch.jsonに`"preLaunchTask": "build"`を追加する

```json:launch.json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "program": "${workspaceFolder}\\index.js",
+            "preLaunchTask": "build"
        }
    ]
}
```