
- ソフトウェアのモデリング
    - 何をさせたいか(what)の「要求定義、要求モデリング」と、どう作るか(how)の「設計」の段階に分けられる

- 要求モデリングは「機能モデリング」と「データモデリング」に分けられる
    - 機能モデリング
        - コンピュータに任せる仕事を整理する

    - データモデリング
        - コンピュータに覚えさせる情報を整理する
        - 管理したい情報の性質を定義し、適切な名前をつけて概念を明確にする作業
        - 「概念モデリング」とも呼ばれる

- 概念モデリングを行うことの効果
    - システムの全体像を把握できる
        - アプリケーションの機能や規模や複雑さを把握できる
    - 対象とするビジネス活動そのものを理解できる
        - ビジネス上の出来事や登場人物がもれなく反映されるから

- UML(Unified Modeling Language)の中心となるもの
    - クラス図
    - オブジェクト図
    - ステートマシン図

- 概念モデリングの基本要素
    - クラス
    - 属性
    - 関連
    - 継承

- クラス
    - UMLでは「集合」を指す
    - 会員顧客クラスが集合で、個々の顧客が集合の要素(インスタンス)
    - 表現したい対象を集合として定義し、そこに適切な名前をつける

- 属性
    - 集合の要素が共通で持つ性質
    - 会員顧客は名称とメールアドレスを持つ

- 概念モデリングで表現するものは全て情報のため、クラス名には情報はつけない

---
![class01](./assets/image/class01.png)

---

- 実際には同じものでも、情報の重複を許容できる場合は別のインスタンスとして表現する

![class02](./assets/image/class02.png)

---

- 概念モデリングにおける継承は全体集合と部分集合の関係を表現するために使う

- サブクラス間で同じインスタンスは共有できない（部分集合の積集合には要素が存在しない)

![class03](./assets/image/class03.png)

---

![class04](./assets/image/class04.png)
![class05](./assets/image/class05.png)


---
- 協力会社や顧客企業は取引先として一元管理する

![class06](./assets/image/class06.png)

---
- 協力会社や顧客企業は取引先として一元管理する

- 部分集合の積集合に要素が存在する場合 = 1つの実体が複数の役割を持つことができる
    - 部分集合固有の性質を役割として実体から分離して表現できる

![class06](./assets/image/class06.png)

---
- 時間の経過により要素の属する部分集合が変わる場合は、変化する部分を役割として実体から切り出す

![class07](./assets/image/class07.png)


---
![class08](./assets/image/class08.png)
![class09](./assets/image/class09.png)
![class10](./assets/image/class10.png)

---
![class11](./assets/image/class11.png)

- 種類を表すか具体的なモノを表すのかを区別する場合
- モノから種類への関連の多重度が1 = 要素の帰属する部分集合が唯一

![class12](./assets/image/class12.png)

---

![class13](./assets/image/class13.png)
![class14](./assets/image/class14.png)

---

![class15](./assets/image/class15.png)

---
- 情報を管理する主体から見た命名をつける
    - 受注は、顧客から注文を受けたという事実をそのまま表現しているため適切な名前

- 1つの商品は複数の受注明細に対応する
- 1つの受注には商品ごとの受注明細が1つ以上存在する

![class16](./assets/image/class16.png)

- ビジネスの違いにより管理する対象が変わる
    - 居酒屋チェーンだとその場で代金精算をするため顧客の連絡先は不要

- 命名も異なる
    - 代金の精算時点で取引が完了するため「売上」

![class17](./assets/image/class17.png)

- 多重度(カーディナリティ)の背後にはビジネスルールが隠れている

- 1回の販売に対して、1人の顧客と1人の販売員と1台の中古車が決まる

![class18](./assets/image/class18.png)

- イベントが在庫を更新する

![class19](./assets/image/class19.png)

![class20](./assets/image/class20.png)

![class21](./assets/image/class21.png)

![class22](./assets/image/class22.png)

![class23](./assets/image/class23.png)

---

- 状態遷移図(ステートマシン)

```mermaid
stateDiagram

  [*] --> 未承認 
  未承認 --> 承認済
  未承認 --> 却下
  承認済 --> [*]
  却下 --> [*]
```

![class24](./assets/image/class24.png)


```mermaid
stateDiagram

  [*] --> 仮受注
  仮受注 --> 受注確定
  仮受注 --> キャンセル
  受注確定 --> 請求待ち
  請求待ち --> 入金済み
  入金済み --> [*]
  キャンセル --> [*]
```

![class25](./assets/image/class25.png)

- [分岐(ガード条件)](https://mermaid-js.github.io/mermaid/#/stateDiagram?id=choice)

```mermaid
stateDiagram-v2

  state if_state <<choice>>
  [*] --> if_state
  if_state --> 出荷準備完了: 在庫あり
  if_state --> 入荷待ち: 在庫なし
  入荷待ち --> 出荷準備完了: 
  出荷準備完了 --> 出荷済み: 出荷
  出荷済み --> 入金済み: 入金
  入金済み --> [*]
```

```mermaid
stateDiagram-v2

  [*] --> 仮登録
  仮登録 --> 本登録: 面談の結果,OK
  仮登録 --> 登録不可: 面談の結果,NG
  本登録 --> [*]
  登録不可 --> [*]
```

```mermaid
stateDiagram-v2

  [*] --> 販売中
  販売中 --> 売れ残り: 販売期間終了
  販売中 --> 予約済み: 予約
  予約済み --> 販売済み: 決済完了
  予約済み --> 販売中: キャンセル
  予約済み --> 売れ残り: 販売期間終了
  販売中 --> 販売済み: 決済完了
  売れ残り --> [*]
  販売済み --> [*]
```

---
- 2つのものを組み合わせた単位で別のものが存在するパターン

![class26](./assets/image/class26.png)
![class27](./assets/image/class27.png)


---
![class28](./assets/image/class28.png)
![class29](./assets/image/class29.png)

---

- 商品情報をモデルとして考える際は、商品の管理単位が「種類」か「個々のモノ」なのかを考える
    - 量産品は種類で扱う
    - 不動産、中古車などの高額商品や一点物を扱う場合は個々のモノで扱う

![class30](./assets/image/class30.png)

