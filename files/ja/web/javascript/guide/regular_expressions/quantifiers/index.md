---
title: 数量詞
slug: Web/JavaScript/Guide/Regular_expressions/Quantifiers
l10n:
  sourceCommit: effd5de5e42bfe045c3bf44b2d7b14f4d6146785
---

{{jsSidebar("JavaScript Guide")}}

数量詞は、一致させる文字や式の数を示します。

{{EmbedInteractiveExample("pages/js/regexp-quantifiers.html", "taller")}}

## 種類

> **メモ:** 以下の表の中で、*アイテム*は単一の文字だけでなく、[文字クラス](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes)、[Unicode プロパティエスケープ](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes)、[グループと後方参照](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Backreferences)を示すこともあります。

<table class="standard-table">
  <thead>
    <tr>
      <th scope="col">文字</th>
      <th scope="col">意味</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code><em>x</em>*</code>
      </td>
      <td>
        <p>
          直前のアイテム "x" の 0 回以上の繰り返しに一致します。例えば
          <code>/bo*/</code> は "A ghost booooed" の "boooo" や "A bird warbled"
          の "b" に一致しますが、 "A goat grunted" には一致しません。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code><em>x</em>+</code>
      </td>
      <td>
        <p>
          直前のアイテム "x" の 1 回以上の繰り返しに一致します。<code>{1,}</code>
          と同等です。例えば <code>/a+/</code> は "candy" の "a" や
          "caaaaaaandy" のすべての "a" に一致します。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code><em>x</em>?</code>
      </td>
      <td>
        <p>
          直前のアイテム "x" の 0 回か 1 回の出現に一致します。例えば
          <code>/e?le?/</code> は "angel" の "el" や "angle" の "le"
          に一致します。
        </p>
        <p>
          <code>*</code>、<code>+</code>、<code>?</code>、<code>{}</code> といった数量詞の直後に使用した場合、既定とは逆に、その数量詞を非貪欲（出現回数が最小のものに一致）とします。既定は貪欲（出現回数が最大のものに一致）です。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code><em>x</em>{<em>n</em>}</code>
      </td>
      <td>
        <p>
          "n" には正の整数が入ります。直前のアイテム "x" がちょうど "n" 回出現するものに一致します。例えば <code>/a{2}/</code> は "candy" の "a" には一致しませんが、"caandy" のすべての "a"、"caaandy" の最初の 2 つの "a" に一致します。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code><em>x</em>{<em>n</em>,}</code>
      </td>
      <td>
        <p>
          "n" には正の整数が入ります。直前のアイテム "x" の少なくとも "n"
          回の出現に一致します。例えば、<code>/a{2,}/</code> は "candy" の "a"
          には一致しませんが、"caandy" や "caaaaaaandy" の "a"
          のすべてに一致します。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code><em>x</em>{<em>n</em>,<em>m</em>}</code>
      </td>
      <td>
        <p>
          "n" には 0 と正の整数が、 "m" には "n"
          より大きい正の整数が入ります。直前のアイテム "x" が少なくとも "n"
          回、多くても "m" 回出現するものに一致します。例えば
          <code>/a{1,3}/</code> は "cndy" では一致せず、"candy" の 'a'、"caandy"
          の 最初の 2 個の "a"、"caaaaaaandy" の最初の 3 個の "a"
          に一致します。"caaaaaaandy" では元の文字列に "a" が 4
          個以上ありますが、一致するのは "aaa" であることに注意してください。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>
          <code><em>x</em>*?</code><br /><code><em>x</em>+?</code><br /><code
            ><em>x</em>??</code
          ><br /><code><em>x</em>{n}?</code><br /><code><em>x</em>{n,}?</code
          ><br /><code><em>x</em>{n,m}?</code>
        </p>
      </td>
      <td>
        <p>
          既定では <code>*</code> や <code>+</code> といった数量詞は貪欲です。つまり、できる限り多くの文字列と一致しようとします。数量詞の後に <code>?</code> の文字を指定すると、数量詞が「非貪欲」になります。つまり、一致が見つかるとすぐに停止します。例えば、"some &#x3C;foo> &#x3C;bar> new &#x3C;/bar> &#x3C;/foo> thing" といった文字列が与えられた場合は、
        </p>
        <ul>
          <li>
            <code>/&#x3C;.*>/</code> は "&#x3C;foo> &#x3C;bar> new &#x3C;/bar> &#x3C;/foo>" に一致します。
          </li>
          <li><code>/&#x3C;.*?>/</code> は "&#x3C;foo>" に一致します。</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## 例

### 繰り返しパターン

```js
const wordEndingWithAs = /\w+a+\b/;
const delicateMessage = "This is Spartaaaaaaa";

console.table(delicateMessage.match(wordEndingWithAs)); // [ "Spartaaaaaaa" ]
```

### 文字数

```js
const singleLetterWord = /\b\w\b/g;
const notSoLongWord = /\b\w{2,6}\b/g;
const loooongWord = /\b\w{13,}\b/g;

const sentence = "Why do I have to learn multiplication table?";

console.table(sentence.match(singleLetterWord)); // ["I"]
console.table(sentence.match(notSoLongWord));    // [ "Why", "do", "have", "to", "learn", "table" ]
console.table(sentence.match(loooongWord));      // ["multiplication"]
```

### 省略可能な文字

```js
const britishText = "He asked his neighbour a favour.";
const americanText = "He asked his neighbor a favor.";

const regexpEnding = /\w+ou?r/g;
// \w+ 1 つ以上の文字
// o   "o" が続く
// u?  省略可能で "u" が続く
// r   "r" が続く

console.table(britishText.match(regexpEnding));
// ["neighbour", "favour"]

console.table(americanText.match(regexpEnding));
// ["neighbor", "favor"]
```

### 貪欲と非貪欲

```js
const text = "I must be getting somewhere near the center of the earth.";
const greedyRegexp = /[\w ]+/;
// [\w ]      ラテンアルファベットまたは空白
//      +     1 回以上

console.log(text.match(greedyRegexp)[0]);
// "I must be getting somewhere near the center of the earth"
// テキストのすべてに一致 (ピリオドを除く)

const nonGreedyRegexp = /[\w ]+?/; // クエスチョンマークに注目
console.log(text.match(nonGreedyRegexp));
// "I"
// 一致する箇所は取りうる最も短い 1 文字
```

## 関連情報

- [正規表現ガイド](/ja/docs/Web/JavaScript/Guide/Regular_Expressions)

  - [文字クラス](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes)
  - [アサーション](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions)
  - [Unicode プロパティエスケープ](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes)
  - [グループと後方参照](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Backreferences)

- [`RegExp()` コンストラクター](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- [ECMAScript 仕様書の数量詞](https://tc39.es/ecma262/multipage/text-processing.html#sec-quantifier)（英語）
