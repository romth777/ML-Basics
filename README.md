# 本資料について
本資料ではAIを支える技術(=機械学習)に関する基本的な考え方の習得を目的とし、その簡単な応用を良く知られたタスクを使って体験する。
具体的には次の通りである。
* AI関連技術(=機械学習)の基本的な考え方
* 良く知られたタスクに対する機械学習の応用

まず、機械学習の基本的な考え方について説明し、それらがどのように応用できるか述べた後、実際のデータを使って簡単なモデルによりその効果を確認する。

## AI関連技術の具体的な定義
AI、即ち人工知能は[Wikipedia](https://ja.wikipedia.org/wiki/%E4%BA%BA%E5%B7%A5%E7%9F%A5%E8%83%BD)によると次のように定義されている。  
''人間の知的能力をコンピュータ上で実現する、様々な技術・ソフトウェア・コンピューターシステム。応用例は自然言語処理（機械翻訳・かな漢字変換・構文解析等）[3]、専門家の推論・判断を模倣するエキスパートシステム、画像データを解析して特定のパターンを検出・抽出したりする画像認識等がある。''  

筆者は"（人間の）推論・判断を模倣する"という部分がAIが他のシステムと違う本質的な表現であると考える。
例えば、人間に代わって画像から猫を抽出し、その猫が何という種類で誰が飼っているのか、年齢はいくつなのか、オスなのかメスなのかという情報を提示したりするようなシステムにおいては、人間が周囲を見渡した時にそこに猫がいるかどうか、もしいるのであれば見たことがある猫かそうでないか、見たことがあればそれに関する情報を提示したり、もし見たことが無ければ過去の近所の猫情報からもともといた猫が産んだ子猫かもしれないなどといった推論を行い、その上で、それらの情報を人間に提示するようなことができれば、それはAIシステムであると考える。あるいは、別の形態のシステムでは人間の会話に自然に入りこみ、問いかけに応じて適切な返事をするようなシステムであったり、はたまた、画像情報や各種センサーの情報を使って車を運転したりするようなシステムにおいて、システムが人間の運転（＝推論・判断）を模倣するようなシステムの事をAIシステムと呼ぶことが出来ると考える。即ち、これらの各タスクに対する人間の推論や判断がコンピュータシステムによって置き換えられたものが”AI”と呼ばれるものであると定義する。

このような定義の元、システムによる推論や判断を行う上での基礎的な技術の一つに機械学習が存在している。機械学習は、素朴に言えば与えられたデータの特徴をモデルの特性に従って捉えるものである。例えば先程の例を借りて周囲に猫がいるか検知するシステムを考える。画像情報が与えられた上で、その画像の中に猫がいるかを判断するために、与えられた画像のピクセル情報から猫の情報を学習によって獲得し知識として蓄える。そして、そこに基づいて別の新しいデータに猫がいるかを判定する。このように与えられたデータからその特性を見出して、見たことがないデータに対しての予備知識としてそれらを活用し、新しい入力データに対してシステムが何かしらの推論や判断を下して、その入力データがどのような性質のものなのかを、過去のデータから判断した上で出力を出すというのが機械学習の概念的な説明である。

## 機械学習の分類
機械学習分野の手法は大きく以下の3つに分けられる
* 教師あり学習
* 教師なし学習
* 強化学習

それぞれについて概要を説明する。

### 教師あり学習
教師あり学習とは、入力データと正解データが与えられたタスクである。例えば入力データが画像の場合には、その画像が何の画像なのかを示すデータや、どこに何が写っているのかラベル付けされたデータ等が正解データとして考えられる。ほかにもテーブルデータが入力の場合、例えば店舗の売り上げなどの正解データが与えられたりする。これらの正解データが正しく出力できるようにモデルを学習させる手法のことを教師あり学習と呼ぶ。教師あり学習における主なタスクは分類と回帰である。分類は例えば画像に写っているものの種類を当てるようなシステムを指す。例えば犬と猫の画像があったとき、入力された画像がどちらのものかを当てるようなタスクが考えられる。この場合の答えは一般的には離散的な値（例えば犬、猫等）を取る。もう一つのタスクに回帰というものがある。これは例えば店舗の売り上げ予測などに利用され、昨日の来客数、昨日の売り上げ、今朝の天気等が与えられたときに、今日の売り上げを予測するというものが考えられる。この時、予測する値は連続値を取るのが一般的である。もちろん応用例はこれだけに限らず、例えば画像データが与えられたときにその人が何歳ぐらいなのかを当てる回帰的なタスクや、年齢、年収、既婚/未婚等を含んだテーブルデータが与えられた時にその人の職業を分類するようなタスクもありえる。

### 教師なし学習
教師なし学習とは、入力データのみが与えられたタスクである。例えば入力データが画像の場合にそこに何が写っているか分類するタスクが考えられる。教師あり学習の場合はそれらの分類を学習するために正解データと一致しているかしていないかという情報に基づいて行っていた。教師なし学習の場合は、それらの学習を例えばその距離的な近さによってクラスタリングしてくようなモデルを使ってそれぞれがどの分類に当てはまるのかを探っていく。教師あり学習の場合はラベルデータを用意するコストがかかるが、教師なし学習の場合はそのようなコストは発生しない。

### 強化学習
強化学習は、これまでの学習法とは少し毛色が異なり、一般的にはagnetとenviromentが存在する。environmentは解くべきタスクであり、例えばゲームのようなものである。agentはこのゲームを解くプレイヤーであり、このagentがenvironmentにあれこれ相互作用することで、そのゲームに対する適切な操作を学習していく。例えば、一本道の橋を渡りきれば成功、落ちれば失敗というようなゲームを考えると、agentはまっすぐ進んで落ちずに渡り切れば良い成績を得る事が出来る。このまっすぐ進んで落ちずに渡り切るという動作を何度も失敗しながら体を張って覚えていく。具体的にはagentはenvironmentから現在の状態とスコア（報酬）を受け取り、それを元に次のアクションを決める。次のアクションを取るとゲームの次の状態と次のスコアが確定するので、それを元にまた次のアクションを決めるといった具合である。すなわち、どのような状態の時に、どのようなアクションを取ればよいスコアが得られるかを繰り返し試すことで、最適な動きをagentに学習させる枠組みを強化学習と呼ぶ。

### ちなみに深層学習
深層学習は上記の枠組みの全てで活用されている学習用モデルの事である。なので、機械学習と深層学習、強化学習等を並列に述べるのは少し違和感がある。

## 機械学習の応用タスク
現時点で思いつく範囲では以下のようなものが挙げられる。
* 画像認識
  - 画像処理
  - セグメンテーション
* 自然言語処理
  - 機械翻訳
  - 対話
  - 自動要約
* 音声処理
  - 音声自動生成
  - 音声認識
* テーブルデータ（時系列データ含む）
  - 来客予測モデル
  - 天気予報

# やってみよう
## タイタニック号生存予測
機械学習分野で良く知られたタスクの一つにタイタニック号の生存者予測というものがある。これは乗客の様々なプロパティ情報を元に、その乗客が生存したか、そうでなかったかを予測するバイナリークラシフィケーションタスクである。とにかくやってみるのがここでのやりたいことなので、手法に関する細かい説明は割愛するが、以下のファイルで実行してみましょう。


[colab](https://colab.research.google.com/github/romth777/ML-Basics/blob/master/src/titanic_survivals.ipynb)
[ソースはこちら](./src/titanic_survivals.ipynb)




## 参考資料
