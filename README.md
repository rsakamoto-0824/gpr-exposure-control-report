# ガウス過程回帰を用いた枚葉露光量制御による線幅ばらつき改善

半導体リソグラフィー工程の積層膜干渉と、GPRを用いた枚葉露光量制御をまとめた日本語技術レポートです。
LuaLaTeX、BibLaTeXおよびBiberでコンパイルします。
表紙、概要（要旨）、本文を社内提出時に個別に扱えるよう、3つのTeXファイルに分けています。本文の数式と表は `main.tex` に集約し、LaTeX内部で生成する図はありません。
提案GPR制御は実験評価段階であり、量産適用実績はまだありません。本文の量産関連記述は、将来の適用に向けた実装案と評価課題です。

## ファイル構成

```text
report/
├── .gitignore        # PDF・コンパイル補助ファイルを除外
├── cover.tex         # 表紙（社内規定様式への転記・調整用）
├── abstract.tex      # 概要（要旨）
├── main.tex          # 目次から始まる本文・数式・表
├── references.bib    # 参考文献
├── latexmkrc         # LuaLaTeX / Biber設定
├── README.md
└── figures/
    └── README.md     # 後から追加する画像名の一覧
```

表紙・要旨・本文のPDFは各TeXファイルから生成し、Gitでは管理しません。`figures/` に追加する図版は、PNG、PDF、JPG、JPEGを含めて管理できます。

## Overleafへのアップロード方法

1. `report` ディレクトリ内のファイルとディレクトリをZIP形式にします。
2. Overleafで新規プロジェクトを作成します。
3. ZIPファイルをアップロードします。
4. 本文を作成するときは、`main.tex` をMain documentに設定します。
5. 表紙または概要を作成するときは、Main documentをそれぞれ `cover.tex` または `abstract.tex` に切り替えます。
6. CompilerをLuaLaTeXに設定します。
7. 本文の参考文献処理にBiberが使用されることを確認します。`biblatex` の `backend=biber` と `latexmkrc` は設定済みです。
8. Recompileを実行します。

## ローカルコンパイル方法

TeX Live等でLuaLaTeX、LatexmkおよびBiberが利用できる環境を用意します。`report` ディレクトリで次を実行します。

```bash
latexmk main.tex
latexmk cover.tex
latexmk abstract.tex
```

本文を個別に実行する場合は次の順序です。

```bash
lualatex main.tex
biber main
lualatex main.tex
lualatex main.tex
```

## 図の差し替え方法

1. `figures` ディレクトリに模式図または実データグラフを配置します。
2. `figures/README.md` に記載したファイル名と一致させます。
3. 図が存在しない場合は、PDF内にプレースホルダーが表示されます。
4. 指定名の図を配置して再コンパイルすると、本文を変更せずに実画像へ差し替わります。
5. 画像形式はPNG、PDF、JPGまたはJPEGを使用できます。拡張子を除いたファイル名を一致させてください。

## PDF完成前の未確定項目

以下を確定情報と実データで置き換えてください。

- `XX` および `\placeholder`
- RMSE、MAE、決定係数、最大絶対誤差、平均予測標準偏差
- OLSとGPRの比較結果
- 線幅標準偏差、線幅改善率
- イメージセンサー特性標準偏差、特性改善率
- 装置名、製品名、評価期間
- GPRのカーネル種類とハイパーパラメータ
- 模式図5点と実データグラフ10点
- `cover.tex` の部門名、作成者、作成日
- 社内規定の表紙・概要様式が指定されている場合は、`cover.tex` と `abstract.tex` の体裁

## 既知の警告

- `caption` パッケージが `ltjsarticle` を標準クラスとして識別しないため、`Unknown document class` 警告が表示されます。標準のキャプション設定が適用され、PDFの生成には影響しません。
- 模式図と実データグラフが未配置のため、現在のPDFには図ファイル未配置のプレースホルダーが表示されます。

## 注意事項

- 未確定値を仮の数値で埋めないでください。
- 参考文献を追加・変更する場合は、実在と書誌情報を確認してください。
- 実データや社内情報を外部へアップロードする前に、社内の情報管理ルールを確認してください。
