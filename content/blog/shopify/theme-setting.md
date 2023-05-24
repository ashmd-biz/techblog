---
title: Shopifyのテーマのカスタマイズ設定で配列的なデータの扱い方
date: "2023-05-22"
description: "shopifyのテーマのカスタマイズの項目に複数データ形式の設定方法"
---

shopifyのthemeのカスタマイズで、単純な文字列とか数字とか日付とはちゃんと設定項目として用意されているんですが
可変形式の配列的なデータの持ち方がわからなかったのでChatGPTで質問してみました。

質問内容

```
shopifyでフロントに任意の<input type="select">を配置して、shopfiyのテーマのカスタマイズからoptionの内容をいじりたいんですが、どうやればいいですか？schemaで可変の配列的なのを扱うtypeがありますか？
```

この回答としては、方法はないとのこと。。。


でもって、しょうが無いのでtextareaを改行区切りで代用できるか聞いてみました。
```
パラグラフで改行を分割する形で実装できますか？
```

そしたら

Shopifyのテーマ設定には直接的な配列型のデータを扱う機能がないため、テキストエリアを利用してパラグラフを区切るというクリエイティブな方法を試すことができます。
```
{
  "name": "My settings",
  "settings": [
    {
      "type": "textarea",
      "id": "my_select_options",
      "label": "Enter options, separated by new lines",
      "default": "Option 1\nOption 2\nOption 3"
    }
  ]
}
```
使い方は以下
```
{% assign options = settings.my_select_options | newline_to_br | split: '<br />' %}
<select>
{% for option in options %}
  <option>{{ option }}</option>
{% endfor %}
</select>
```

でできるとのこと。回答はいいとして、クリエイティブな方法でできますよ！！とちょっと褒められた感があって嬉しい。
人間と分かってなくても、ほぼ人間的な挙動をするものから褒められるとやっぱ嬉しいらしい。

よく考えたら、ChatGPT3.5だとできないとは言わず、適当な回答を出すことが多いんですが、やはりGPT4はちゃんと否定してくれるのでやはりかなり賢いですね。