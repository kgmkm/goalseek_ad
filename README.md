# ㊙goalseek_ad
🔞小説用ゴールシークプロンプト
[EasyNovelAssistant](https://github.com/Zuntan03/EasyNovelAssistant)で打率の高い小説企画ガチャと小説本文ガチャをするためのプロンプト

editor・writerと２つの役割が存在。つまり編プロと作家が分業して制作する状況をエミュレーション

# ⚠notice
- このプロンプトはまだdev版で、破壊的変更の可能性が存在します。アップデートはこのページを逐次確認してください
- このコンテンツは[Github利用規約](https://docs.github.com/ja/site-policy/acceptable-use-policies/github-sexually-obscene-content)を参考に、芸術的側面を持つテキストベースコンテンツとして投稿しました
- （特に18歳未満など若年層の方は、）お住まいの地域国家のコンテンツレーティングを遵守し、このコンテンツの使用可否をご判断ください

# 🏕checked environment
- EasyNovelAssistant
- gguf models
  + Japanese-TextGen-MoE-TEST-2x7B-NSFW_iMat_IQ4_XS (汎用・おすすめ・5/14時点最推し)
  + Vecteus-v1 (汎用・おすすめ)
  + LightChatAssistant-TypeB-2x7B_iq4xs_imatrix (汎用)
  + sniffyOther-7B-Novel-writing (writer用)
  + Ninja-v1-NSFW_Q_8_0 (writer用)
  + japanese-starling-chatv-7b.Q4_K_M (imager用)
- GPU layer L33
- 生成文の長さ 2048が安定。 1024-4096 (高すぎると荒れる)
  + sniffyOtherは1024-2048が良さそう
- 温度感 0.5-0.6

# 🚮how to use
## editor編（小説企画からプロッティングまで）
- EasyNovelAssistantの左側に[init_editor.txt](https://github.com/kgmkm/goalseek_ad/blob/main/init_editor.txt)の内容をコピペする
- 一緒に作りたい小説は「xxx」です！ の部分を編集し、作りたい小説の情報を説明する
  + 小説を丸ごと説明するタイトルなどが推奨
- EasyNovelAssistantで生成開始し、しばらく放置、その後outputを確認してチェリーピック
- 最も良かった内容の「箇条書きリスト」をコピーする

### recommended config
- Japanese-TextGen-MoE-TEST-2x7B-NSFW_iMat_IQ4_XS 3072 0.6
- Vecteus-v1 L33 2048 0.6
- LightChatAssistant-TypeB-2x7B_iq4xs_imatrix L33 4096 0.6

### editors memo
- 作りたい小説の情報 1行にまとまる内容がオススメ。とはいえココでヒロイン名と相手役名を策定するとブレが抑えられてオススメ

## writer編（editorが生成した設定とプロットで執筆）
- EasyNovelAssistantの左側に[init_writer.txt](https://github.com/kgmkm/goalseek_ad/blob/main/init_writer.txt)の内容をコピペする
- 「小説設定情報」の下に、箇条書きリストをペースト
  + 【重要】箇条書きリストの抜けとフォーマット崩れを手直しする（特に必須なのは小説タイトル・ジャンル・ヒロインのデザイン・小説のアウトライン・小説のプロット）
- 「執筆する章」の「章数」と「文字数」を適宜修正する
  + 章数は１章～２章づつ書かせることを推奨
  + 箇条書きリストの「プロット」から、書かない予定の章を削除する
- 「小説本文」に、章の冒頭または前章の終盤をコピペする
  + 【重要】序章や第一章から書き出す場合でも、１行だけ本文を執筆しておく。AIが続けて設定情報を列記するケースを防ぐため
- EasyNovelAssistantで生成開始し、しばらく放置、その後outputを確認してチェリーピック
- 最も良かった内容の「小説本文」をコピーする
  + 手作業で小説本文を校正して、プロンプトに「小説本文」をペーストし、箇条書きリストの「プロット」を増補して、次章を書かせる
  + 終章まで繰り返す。お疲れ様！

### recommended config
- Japanese-TextGen-MoE-TEST-2x7B-NSFW_iMat_IQ4_XS 3072 0.6
- Vecteus-v1 L33 2048 0.6
- LightChatAssistant-TypeB-2x7B_iq4xs_imatrix L33 2048-4096 0.6

### writers memo
- 文字数はぶっちゃけ目安にならんけど、5000文字以上だと「シーンをあなたの想像力を働かせて増補」が効いてくる
- 序章の書き出しはとりあえず場面説明などがオススメ。"昼下がりの保健室に、女性が一人。"など
- 第二章以降から書き出す場合は第一章後半をまとめてペーストしておくと、文体維持を考慮して生成してくれやすくなる
- コピペする小説本文は章まるごとだと、ちょっと長そう。AI出力も荒れる印象があるため、長い場合は小説後半からペーストして次章を書かせる
- 生成過程でシナリオを調整したい場合（絶対あるはず）、「小説設定情報」のアウトラインとプロット、「小説本文」の内容を手作業で修正すること
- 三章・四章・終章執筆あたり、急に話がつまらなくなる印象を受けた際、jsonの部分を削ることで改善したことが何回もあった。試してみて！（プロンプトとは）

## imager編（editorが生成した設定で画像生成AI用プロンプトを作る）
- EasyNovelAssistantの左側に[init_imager.txt](https://github.com/kgmkm/goalseek_ad/blob/main/init_imager.txt)の内容をコピペする
- 行頭にキャラクター設定を箇条書きリストから抜き出して貼り付ける（例ではシャイニーピーチを参考にしつつ案を削除しよう
- EasyNovelAssistantで生成開始し、しばらく放置、その後outputを確認してチェリーピック
- 最も良さそうな内容のpromptをコピーしてpositive prompt欄に入れよう

### recommended config
- japanese-starling-chatv-7b.Q4_K_M 128 (stable diffusionらしいprompt構文を高いレベルで理解している)
- Vecteus-v1 L33 128 0.6

### imagers memo
- 正直俺が思いもつかなかったような画質向上プロンプトが混ざることがあり、驚くような画像が出ることがある。stable diffusionユーザは是非使ってほしい
- 時々プロンプト内にrealisticが交じるので、イラスト系出力したい人は気をつけること(とりわけpony系SDXL使ってると効きやすい)

# 🉐prompt detail
## init_editor.txt
LLMが小説の編集者として企画から設定・プロット作成まで作成してくれる
それらは設定情報として箇条書きリストとして出力される
1行目は呪文詠唱

## init_writer.txt
init_editorで出力された設定情報として読み込ませることで、LLMが小説家として小説を書いてくれる（しかも内容のブレをかなり抑えた状態で）
1行目は呪文詠唱

## goalseek_adult_editor.yaml
init_editorの1行目に存在するminified jsonの中身（minifiedしているのはトークン節約のため）。ここで編集者として必要なスキルを鍛えている。何か編集者としての挙動が変だったり、調整したい場合は、このファイルから編集し、yamlからjsonに変換すると良い。

## goalseek_adult_writer.yaml
上記と近いもの。ここで小説家として必要なスキルを鍛えている

## adult_control_function.yaml
【修正中ファイル】EasyNovelAssistantのUIはAIと対話して生成するものではないため、途中の指示入れが困難。だが中のkobold.cppではチャットモードで小説作成ができる。チャットモードの場合、この指示リストがあることで、無視されづらい状況が作れる

# 📕example of a novel
pixivにて"EasyNovelAssistantショーケース"で検索
