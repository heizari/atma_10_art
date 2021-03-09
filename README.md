# atma_10
<!-- toc -->
* [各テーブルの詳細](#各テーブルの詳細)
*
<!-- tocstop -->


## 各テーブルの詳細
<!-- toc -->
- [art_object](#art_object)
- [color](#color)
- [material](#material)
- [historical_person](#historical_person)
- [object_collection](#object_collection)
- [production_place](#production_place)
- [technique](#technique)
- [maker](#maker)
- [principal_maker](#principal_maker)
- [principal_maker_occupation](#principal_maker_occupation)
 

<!-- tocstop -->
### art_object (train / test.csv の table)
作品情報が記録されたテーブルです。今回のコンペティションで予測対象となる likes は train.csv のみ存在しています。

object_id: 作品ID.
art_series_id: シリーズものの作品ID
title: 作品のタイトル
description: 説明文
long_title: 長いめのタイトル
principal_maker: 主な製作者
principal_or_first_maker: 第一製作者或いは主な製作者
sub_title: 作品の大きさなどの情報
copyright_holder: 権利保持者
more_title: タイトル2
acquisition_method: 収集方法 (作品を収集することを acquisition とよびます)
acquisition_date: 収集された日
acquisition_credit_line: 収集に際して資金提供などを行った場合の情報
dating_presenting_date: 製作期間 (dating は作品を作った日のことを表す prefix です)
dating_sorting_date: 並び替え表示の際に用いられる代表年
dating_period: 制作のされた世紀
dating_year_early: 製作期間の始まり・年
dating_year_late: 製作期間のおわり・年
like: 作品につけられたいいねの数。0以上の整数。この値が予測対象です。
color / palette
作品の写真に移った色の情報です。color はアムステルダム美術館が利用している色情報、palette は nyk510 が作成したアルゴリズムによって抽出された色情報です。

### color
object_id
percentage: 全体にしめる割合 (%)
hex: 色
palette
object_id
ratio: 全体での割合
color_r: 色を rgb 表示したときの R (red) の値.以下 G/B も同様です
color_g: G
color_b: B

### material
作品の材料が紐付いたテーブルです。ひとつの作品に対して複数対応する可能性があります。

object_id
name: 材料名

### historical_person
作品に描かれたり、写ったりしている人物のテーブルです。たとえばレンブラント・ファン・レインの「夜警」では実際に存在した市長 https://en.wikipedia.org/wiki/Frans_Banninck_Cocq などが描かれており、それらの情報が保存されています。

object_id
name: 人物の名前
### object_collection
作品がどのような形式であるか。

object_id
name: 形式名
### production_place
作品が描かれた場所です。複数にまたがる場合や、不明な場合があります。
不明な場合, name の prefix として "?" が付与されます。

ex: "? Netherlands" - オランダであると言われているが、不明確

object_id
name: 場所の名前
### technique
どのような技法で描かれたかが保存されたテーブルです。

object_id
name: 技法の名前
### maker
作家情報が保存されたテーブルです。name が行に対してユニークであり、他のテーブルと紐付ける場合 name を key 列として利用してください。

name: 名前
date_of_birth: 誕生日 (or 年)
place_of_birth: 生まれた場所
date_of_death: 死亡日 (or 年)
place_of_death: 死亡した場所
nationality: 国籍
### principal_maker
作品に携わった作家に関するテーブル。作家ごとに作品にどのように関与したかが保存されています。ひとつの作品に対して複数の作家が関わっている場合があるため art_object に対しては複数紐づく可能性があることに注意してください。

id: principal_maker table のレコードに固有のID
object_id: 携わった作品. train/test の object_id とひも付きます.
qualification: どのような携わり方をしたか (ex. mentioned on object)
roles: 役割
productionPlaces: 制作場所
maker_name: 作家の名前. maker の name とひも付きます.
### principal_maker_occupation
作家が作品に対してどのような作業を行ったかを表しているテーブルです。複数の仮定に関与する場合があるため principal_maker とは 1-m でひも付きます。

id: principal_maker の id 列とひも付きます
name: 作家の行った作業名