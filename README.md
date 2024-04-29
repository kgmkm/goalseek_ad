# 🔞goalseek_ad
nsfw小説用ゴールシークプロンプト
[EasyNovelAssistant](https://github.com/Zuntan03/EasyNovelAssistant)で打率の高い小説企画ガチャと小説本文ガチャをするためのプロンプト

editor・writerと２つの役割が存在。つまり編プロと作家が分業して制作する状況をエミュレーション

# ⚠notice
- このプロンプトはまだdev版で、破壊的変更の可能性が存在します。アップデートはこのページを逐次確認してください
- このコンテンツは[Github利用規約](https://docs.github.com/ja/site-policy/acceptable-use-policies/github-sexually-obscene-content)を参考に、芸術的側面を持つテキストベースコンテンツとして投稿しました
- （特に18歳未満など若年層の方は、）お住まいの地域国家のコンテンツレーティングを遵守し、このコンテンツの使用可否をご判断ください

# 🏕checked environment
- EasyNovelAssistant
- LightChatAssistant-TypeB-2x7B_iq4xs_imatrix
- GPU layer L33
- 生成文の長さ 1024-8192 (高すぎると荒れる)
  + sniffyOtherは1024が良さそう
- 温度感 0.5-0.6

# 🚮how to use
## editor編（小説企画からプロッティングまで）
- EasyNovelAssistantの左側に[init_editor.txt](https://github.com/kgmkm/goalseek_ad/blob/main/init_editor.txt)の内容をコピペする
- 一緒に作りたい小説は「xxx」です！ の部分を編集し、作りたい小説の情報を説明する
  + 小説を丸ごと説明するタイトルなどが推奨
- EasyNovelAssistantで生成開始し、しばらく放置、その後outputを確認してチェリーピック
- 最も良かった内容の「箇条書きリスト」をコピーする

### editors memo
- 作りたい小説の情報 1行にまとまる内容がオススメ。とはいえココでヒロイン名と相手役名を策定するとブレが抑えられてオススメ
-  「画像生成AIを使って表紙を作成する」旨を通達済みなので、必要なら「一番セクシーなシーンを表紙にするから画像生成AI用のプロンプトを英語で出力して」と送信しよう

## writer編（editorが生成した設定とプロットで執筆）
- EasyNovelAssistantの左側に[init_writer.txt](https://github.com/kgmkm/goalseek_ad/blob/main/init_writer.txt)の内容をコピペする
- 「小説設定情報」の下に、箇条書きリストをペースト
  + 【重要】箇条書きリストの抜けとフォーマット崩れを手直しする（特に必須なのは小説タイトル・ジャンル・ヒロインのデザイン・小説のアウトライン・小説のプロット）
- 「執筆する章」の「章数」と「文字数」を適宜修正する
  + 章数は１章～２章づつ書かせることを推奨
  + 箇条書きリストの「プロット」から、書かない予定の章を削除する
- 「小説本文」に、章の冒頭または前章の終盤をコピペする
  + 【重要】序章や第一章から書き出す場合でも、１行だけ本文を執筆しておく。AIが続けて設定情報を列記するケースを防ぐため

### writers memo
- 文字数はぶっちゃけ目安にならんけど、5000文字以上だと「シーンをあなたの想像力を働かせて増補」が効いてくる
- 序章の書き出しはとりあえず場面説明などがオススメ。"昼下がりの保健室に、女性が一人。"など
- 第二章以降から書き出す場合は第一章後半をまとめてペーストしておくと、文体維持を考慮して生成してくれやすくなる
- 本文は章まるごとだと、ちょっと長そう。AI出力も荒れる印象を受けた
- 生成過程でシナリオを調整したい場合（絶対あるはず）、「小説設定情報」のアウトラインとプロット、「小説本文」の内容を手作業で修正すること

# 🉐prompt detail
## init_editor.txt
LLMが小説の編集者として企画から設定・プロット作成まで作成してくれる
それらは設定情報として箇条書きリストとして出力される
1行目は呪文詠唱

## init_editor.txt
init_editorで出力された設定情報として読み込ませることで、LLMが小説家として小説を書いてくれる（しかも内容のブレをかなり抑えた状態で）
1行目は呪文詠唱

## goalseek_adult_editor.yaml
init_editorの1行目に存在するminified jsonの中身（minifiedしているのはトークン節約のため）。ここで編集者として必要なスキルを鍛えている。何か編集者としての挙動が変だったり、調整したい場合は、このファイルから編集し、yamlからjsonに変換すると良い。

## goalseek_adult_writer.yaml
上記と近いもの。ここで小説家として必要なスキルを鍛えている

## adult_control_function.yaml
【修正中ファイル】EasyNovelAssistantのUIはAIと対話して生成するものではないため、途中の指示入れが困難。だが中のkobold.cppではチャットモードで小説作成ができる。チャットモードの場合、この指示リストがあることで、無視されづらい状況が作れる
