project_path: /web/_project.yaml
book_path: /web/fundamentals/_book.yaml
description: セマンティクスと支援技術の概要


{# wf_updated_on:2016-10-04 #}
{# wf_published_on:2016-10-04 #}

#  セマンティクスの概要 {: .page-title }

{% include "web/_shared/contributors/megginkearney.html" %}
{% include "web/_shared/contributors/dgash.html" %}
{% include "web/_shared/contributors/aliceboxhall.html" %}



ここまで、身体的な障がい、技術的な問題、または個人の好みなど理由のいかんを問わず、マウスやポインティング デバイスを使用できないユーザーがサイトにアクセスできるようにする方法について説明しました。そのために、キーボードだけで使用できるように対処しました。これにはいくつか注意や検討が必要ですが、最初からそのつもりで計画すれば、それほど大がかりな作業にはなりません。基本的な作業が完了したら、次は、完全にアクセス可能でより洗練されたサイトに至るまでの長い道のりを歩むことになります。


このレッスンでは、その作業を基に、その他のユーザー補助機能の要素についても検討します。たとえば、画面を見ることができない、[Victor Tsaran などのユーザー](/web/fundamentals/accessibility/#understanding-users-diversity)をサポートするウェブサイトを構築する方法を取り上げます。




まず、*支援技術*の背景について少し説明します。これは情報にアクセスできない障がいを持つ方をサポートする、スクリーン リーダーなどのツールを指す一般的な用語です。



次に、一般的なユーザー エクスペリエンスの概念を説明し、これらの概念をベースに、支援技術のユーザー エクスペリエンスについてさらに詳しく見ていきます。


最後に、HTML を効果的に使用し、支援技術が必要なユーザーのエクスペリエンスを改善する方法を説明します。この方法は、以前にフォーカスの問題に対処した方法と少し重なっているため、その点についても取り上げます。



##  支援技術

*支援技術*とは、障がいのためにタスクを完了するのが困難な方たちを支援するデバイス、ソフトウェア、ツールを包括的に表す用語です。広い意味では、歩行用の杖や読書用の虫メガネのようなローテクから、ロボット義手やスマートフォンの画像認識ソフトウェアなどのハイテクまで該当します。




![杖、虫眼鏡、ロボット義手など支援技術の例](imgs/assistive-tech1.png)


支援技術には、ブラウザのズームのように一般的なものから、カスタムデザインのゲーム コントローラなど特殊なものまで含まれます。点字ディスプレイのような独立した物理デバイスや、音声制御などソフトウェアに完全に組み込まれたものもあります。スクリーン リーダーのようにオペレーティング システムに組み込むものや、Chrome 拡張機能のようなアドオンもあります。


![ブラウザのズーム、点字ディスプレイ、音声制御など、その他の支援技術の例](imgs/assistive-tech2.png)


支援技術と一般的な技術の境界はあいまいですが、結局のところ、なんらかのタスクを行う人を支援するすべての技術があてはまります。また、技術は「支援」カテゴリの枠に収まらないこともあります。


たとえば、最も古い市販の音声言語合成製品の 1 つに、視覚障がい者向けの音声計算器がありました。現在、音声言語合成はルート案内からバーチャル アシスタントまで、いたるところで利用されています。反対に、元々汎用目的だった技術が、支援目的で使われることもよくあります。たとえば、低視力の方がスマートフォンのカメラのズーム機能を使用すると、現実の世界を見るのが楽になります。



ウェブ開発の世界では、幅広い技術について検討しなければなりません。スクリーン リーダー、点字ディスプレイ、画面の拡大、音声制御、スイッチ デバイス、さらにはページのデフォルトのインターフェースを適応させて特定のインターフェースを作成する支援技術を使用して、ウェブサイトを操作する場合があります。




これらの支援技術の多くは、アクセス可能なユーザー エクスペリエンスを実現するために、*プログラムで表現されたセマンティクス*に依存しています。このレッスンでは、主にこの内容について説明します。プログラムで表現されたセマンティクスについて説明する前に、*アフォーダンス*について少し説明します。


##  アフォーダンス

人工のツールやデバイスを使用するときは通常、その形式やデザインを見ると、その機能や使い方について理解できます。*アフォーダンス*とは、ユーザーにアクションを実行する機会を提供または説明するものを指します。アフォーダンスが適切にデザインされていれば、よりわかりやすく、直感的に使用できます。



古くからある例として、やかんやティーポットがあげられます。これまでティーポットを見たことがなくても、持つ場所は注ぎ口ではなく取っ手だと容易に認識できます。



![取っ手と注ぎ口のついたティーポット](imgs/teapot.png)

このアフォーダンスは、ウォーター ポット、ビールのピッチャー、コーヒーのマグカップなど、これまで目にしてきたその他多くのものと類似しているためです。ポットの注ぎ口を持つことも*できた*でしょうが、同様のアフォーダンスの経験から、ハンドルを持つほうが良いことがわかります。



グラフィック ユーザー インターフェースでは、アフォーダンスは実行できるアクションを表しますが、操作できる物理オブジェクトが存在しないため、あいまいになりがちです。そのため GUI のアフォーダンスでは特に、最小限のトレーニングで使い方が伝わるように、ボタン、チェックボックス、スクロールバーなどはあいまいさを排除して設計されています。




たとえば、一般的なフォーム要素の使い方（アフォーダンス）は、次のように言い換えることができます。


 - ラジオボタン: 「これらのオプションのうち 1 つを選択できます」
 - チェックボックス: 「このオプションで "はい" または "いいえ" を選択できます」
 - テキスト フィールド: 「この領域になにかを入力できます」
 - プルダウン: 「この要素を開いて、オプションを表示できます」

これらの要素は、*見ることさえできれば*結論を引き出すことができます。通常、要素が与える視覚的なヒントを見ることができないユーザーは、その意味を理解したり、アフォーダンスが表すものを直感的につかむことはできません。そこで、ユーザーのニーズに合った代替インターフェースを構築できる支援技術を使って、柔軟に情報にアクセスできるようにする必要があります。





このように非視覚的なアフォーダンスの提供方法を、*セマンティクス*と呼びます。

## スクリーン リーダー

一般的な支援技術の 1 つが*スクリーン リーダー*です。これは、生成された音声で画面上のテキストを読み上げることで、視覚障がいを持つ方がコンピューターを使用できるようにするプログラムです。ユーザーは、キーボードを使用して関連する領域にカーソルを移動し、読み上げる部分をコントロールできます。


視覚障がいを持つ [Victor
Tsaran](/web/fundamentals/accessibility/#understanding-users-diversity)
 に、OS X で VoiceOver という組み込みのスクリーン リーダーを使用して、どのようにウェブにアクセスしているのかを説明してもらいました。[こちらの動画](https://www.youtube.com/watch?v=QW_dUs9D1oQ)で、VoiceOver を使用している Victor をご覧ください。


次は、皆さんがスクリーン リーダーを試す番です。ここに、*ChromeVox
Lite* のページがあります。JavaScript で記述した、最小限の機能を持つスクリーン リーダーです。低視力の状態をシミュレートして、ユーザーがスクリーン リーダーを使用してタスクを完了できるように、画面はあえてぼやけています。当然ながら、この演習には Chrome ブラウザを使用する必要があります。


[ChromeVox Lite デモページ](http://udacity.github.io/ud891/lesson3-semantics-built-in/02-chromevox-lite/)

画面下部のコントロール パネルを使用して、スクリーン リーダーを制御できます。このスクリーン リーダーは、最小限の機能しかありませんが、`Previous` および `Next` ボタンを使用してコンテンツを移動し、`Click` ボタンを使用して要素をクリックできます。



ChromeVox Lite を有効にしてこのページを参照すると、スクリーン リーダーを使用したときの感覚がわかります。スクリーン リーダー（またはその他の支援技術）が実際に、プログラムで表現されたセマンティクスに基づいて、代替となる完全なユーザー エクスペリエンスを生み出している点について考えてみましょう。視覚的なインターフェースに代わって、スクリーン リーダーは音声インターフェースを提供します。


スクリーン リーダーが、各インターフェース要素に関する情報をどのようにユーザーに提供しているのかを意識してください。適切に設計されたリーダーは、遭遇した要素に関する次のような情報をすべて、あるいは少なくともその大半をユーザーに伝えることが期待されます。


 - 要素の*役割*またはタイプ。指定されている場合（必要）
 - 要素の*名前*。存在する場合（必要）
 - 要素の*値*。存在する場合（任意）
 - 要素の*状態*。有効 / 無効など（該当する場合）


ネイティブ要素にはユーザー補助機能のメタデータが組み込まれているため、スクリーン リーダーはこの代替 UI を作成できます。レンダリング エンジンがネイティブ コードを使用して視覚的なインターフェースを作成するのと同様に、スクリーン リーダーは DOM ノードのメタデータを使用して、次のようにアクセス可能なバージョンを作成できます。




![スクリーン リーダーが DOM を使用して、アクセス可能なノードを作成]
(imgs/nativecodetoacc.png)


{# wf_devsite_translation #}
