# pin-assets

Pinterest一括アップロード用の**画像だけ**を置く公開リポジトリ。

`affiliate` リポジトリの `pipeline/scripts/publish_pins.py` が、
`pipeline/out/pins/{week}/` の生成済みPNGをここへコピー → commit → push する。
Pinterestの一括CSVの `Media URL` 列は、ここのraw URLを指す。

```
https://raw.githubusercontent.com/kaseinohime/pin-assets/main/{week}/{pin_id}.png
```

## ディレクトリ

```
pin-assets/
├── README.md
├── .gitignore
└── 2026-W31/          ← publish_pins.py が週ごとに作る
    ├── A001.png
    └── B001.png
```

## ここに置いてはいけないもの

**公開リポジトリなので、画像以外は一切置かない。**

- 企画CSV（`plans/*.csv`）— キーワード戦略と案件の手の内が全部載っている
- 記事の下書き（`articles/`）— 文体定義とNGワードが含まれる
- `data/` 配下のデータ類
- `config.json` — ローカルパスが入っている
- 名義に関わるメモ（なぎ / まや / 姫乃の対応関係）

`.gitignore` で機械的に弾いているが、**ignoreは最後の砦であって設計ではない**。
そもそもこのリポジトリに近づけないこと。

## テスト行について

`publish_pins.py` は `qc.py` の `is_test_row()` で判定したテスト行（X999等）を
公開対象から自動で除外する。手で消す必要はない。

## セットアップ（初回のみ）

```bash
gh repo create kaseinohime/pin-assets --public --source=. --remote=origin --push
# gh が無い場合は GitHub 上で空リポジトリを作ってから
# git remote add origin git@github.com:kaseinohime/pin-assets.git
# git push -u origin main
```
