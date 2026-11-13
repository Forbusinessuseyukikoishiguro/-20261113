# コマンドの手引き（Ubuntu・WSL・Windows・VS Code）

## A. 準備（一度だけ）
### Ubuntu / WSL（Ubuntu）
```bash
sudo apt-get update
sudo apt-get install -y python3 python3-venv python3-pip git
python3 --version            # 3.9 以上
```
### Windows（PowerShell）
1. https://www.python.org/ から Python 3.12 以上を入れる（**Add python.exe to PATH** を有効に）
2. 確認：`py --version` または `python --version`
3. Microsoft Store の python が開く場合は、上のインストーラーで入れ直す

## B. Python の仮想環境（プロジェクトごとに作る）
### Ubuntu / WSL
```bash
cd api-testing-kit
python3 -m venv .venv
source .venv/bin/activate        # 終了は deactivate
python -m pip install --upgrade pip
pip install playwright           # 画面の試験を使う場合だけ（任意）
python -m playwright install chromium
```
### Windows（PowerShell）
```powershell
cd api-testing-kit
py -m venv .venv
.\.venv\Scripts\Activate.ps1     # 実行できない場合：Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
python -m pip install --upgrade pip
pip install playwright
python -m playwright install chromium
```

## C. 模倣サーバーを起動する
```bash
# Ubuntu / WSL
python3 server/mock_chat_server.py                 # 既定：127.0.0.1:8790
PORT=8790 MOCK_FAIL=429 python3 server/mock_chat_server.py   # 失敗を再現（429・500・slow・badjson・nochoices）
```
```powershell
# Windows（PowerShell）
python server\mock_chat_server.py
$env:MOCK_FAIL="429"; python server\mock_chat_server.py     # 失敗を再現
```
止める：`Ctrl + C`

## D. 動作を確かめる（別の端末で）
```bash
# Ubuntu / WSL
curl -s -X POST http://127.0.0.1:8790/v1/chat/completions \
  -H "Authorization: Bearer test-key" -H "Content-Type: application/json" \
  -d '{"model":"mock-model","messages":[{"role":"user","content":"こんにちは"}]}'

curl -s -i -X POST http://127.0.0.1:8790/v1/chat/completions -H "Content-Type: application/json" -d '{}'   # キー無し→401
```
```powershell
# Windows（PowerShell）
$body = '{"model":"mock-model","messages":[{"role":"user","content":"こんにちは"}]}'
Invoke-RestMethod -Method Post -Uri http://127.0.0.1:8790/v1/chat/completions -Headers @{Authorization="Bearer test-key"} -ContentType "application/json" -Body $body
```

## E. 試験を実行する
| 目的 | Ubuntu / WSL | Windows（PowerShell） |
|---|---|---|
| まとめて実行 | `bash run_tests.sh` | `powershell -ExecutionPolicy Bypass -File .\run_tests.ps1` |
| 契約・認証・失敗（17件） | `python3 -m unittest -v tests/test_api_contract.py` | `python -m unittest -v tests\test_api_contract.py` |
| 画面（5件） | `python3 tests/test_web_browser.py` | `python tests\test_web_browser.py` |
| 1件だけ | `python3 -m unittest tests.test_api_contract.TestFailures` | 同左 |

## F. 画面を開く
模倣サーバーを起動し、画面を配信する：
```bash
python3 -m http.server 8000     # api-testing-kit/web の中で実行する（web フォルダを配信）
```
ブラウザで `http://localhost:8000/index.html` を開く（接続先は http://127.0.0.1:8790 のまま）。
※ `file://` で直接開くと、通信が制限されることがある。

## G. VS Code で Python を使う
1. 拡張機能「Python」（ms-python.python）を入れる
2. `Ctrl + Shift + P` →「Python: Select Interpreter」→ `.venv` を選ぶ
3. 左の「テスト」（フラスコの形のアイコン）で、unittest のテストが一覧に出る
4. 失敗したテストを右クリック →「Debug Test」で、ブレークポイントを置いて止められる
5. WSL の場合：「Remote - WSL」拡張機能で、WSL の中のフォルダを開く（Windows 側のフォルダを開かない）

## H. よく使う Git の操作（記録用）
```bash
git status
git add api-testing-kit
git commit -m "API 模倣試験を追加（契約17・画面5）"
```

## I. つまずきと対処
| 症状 | 対処 |
|---|---|
| `Address already in use` | 前の模倣サーバーを `Ctrl + C` で止める。または PORT を変える |
| `ModuleNotFoundError: playwright` | 仮想環境を有効にしてから `pip install playwright` |
| 画面の試験が Chromium を見つけられない | `python -m playwright install chromium` を実行 |
| PowerShell で Activate.ps1 が実行できない | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| WSL で遅い | プロジェクトを WSL の中（~/）に置く |
