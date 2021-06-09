[Japanese/[English](https://github.com/Kazuhito00/Tensorflow2-ObjectDetectionAPI-Colab-Hands-On/blob/master/README_EN.md)] 

# TFLite-ModelMaker-EfficientDet-Colab-Hands-On
<img src="https://user-images.githubusercontent.com/37477845/121361039-e4ac9300-c96f-11eb-81f5-d8ee3c08bd16.png" width="60%"><br>

TensorFlow Lite Model Makerのハンズオン用資料です。<br>
VoTTでのアノテーションをローカルPCで実施し、学習～推論はColaboratory上で実施します。<br>アノテーションを実施せずにアノテーション済みデータセットを利用することも出来ます。<br><br>
以下の内容を含みます。<br>
* データセット ※アノテーション未実施
* データセット ※アノテーション済み
* Colaboratory用スクリプト(環境設定、モデル訓練、推論結果確認)

# Requirement
Tensorflow 2.5.0 or later

# Overview
1時間30分程度のボリュームの想定です。
1. VoTT：アノテーション(約30～60分)
1. Colaboratory：環境準備
1. Colaboratory：object_detector向けcsv作成
1. Colaboratory：モデル訓練(約5分)
1. Colaboratory：推論

# Preparations
事前準備として以下が必要です。
* このリポジトリのローカル環境へのクローン
* [VoTT](https://github.com/microsoft/VoTT)のインストール

# 1. VoTT：アノテーション
[VoTT](https://github.com/microsoft/VoTT)を使用してアノテーションを行い、CSV形式で出力します。

<details>
<summary>VoTTのプロジェクト設定</summary>
	
#### 「新規プロジェクト」を選択する
![2020-09-19 (3)](https://user-images.githubusercontent.com/37477845/94047557-38407600-fe0d-11ea-8d10-041a27546e85.png)
#### プロジェクト設定を行う
表示名：TFLite-ModelMaker-EfficientDet-Colab-Hands-On<br>
セキュリティトークン：Generate New Security Token<br>
ソース接続：「Add Connection」を押下<br>
![2021-06-09 (1)](https://user-images.githubusercontent.com/37477845/121363447-ec6d3700-c971-11eb-93fb-3d9dc666a4a0.png)
#### ソース接続の接続設定を行う
表示名：TFLite-ModelMaker-EfficientDet-Colab-Hands-On-TrainData
![2021-06-09 (2)](https://user-images.githubusercontent.com/37477845/121363605-1292d700-c972-11eb-9b4f-6a6a59815e53.png)
プロバイダー：ローカルファイルシステム
![2021-06-09 (3)](https://user-images.githubusercontent.com/37477845/121364024-62719e00-c972-11eb-8973-475206566d58.png)
フォルダーパス：クローンしたリポジトリの「01_dataset」ディレクトリを指定
![2021-06-09 (4)](https://user-images.githubusercontent.com/37477845/121364031-630a3480-c972-11eb-9fb9-0ab94f4e53b7.png)
#### ターゲット接続の接続設定を行う
ターゲット接続：Add Connection
![2021-06-09 (5)](https://user-images.githubusercontent.com/37477845/121364032-63a2cb00-c972-11eb-9694-aa31354b6177.png)
表示名：TFLite-ModelMaker-EfficientDet-Colab-Hands-On-Target<br>
プロバイダー：ローカルファイルシステム<br>
フォルダーパス：任意のディレクトリ<br>
![2021-06-09 (6)](https://user-images.githubusercontent.com/37477845/121364035-643b6180-c972-11eb-85d0-af841609a1df.png)
#### タグを追加し設定を保存する
タグ：「Fish」を追加<br>
「プロジェクトを保存」を押下
![94047577-3d9dc080-fe0d-11ea-9f4f-b5fe7727fc12](https://user-images.githubusercontent.com/37477845/94283906-98a9f180-ff8c-11ea-9e16-a546b26ba763.png)
</details>

<details>
<summary>VoTTを使用してアノテーションを実施</summary>
	
#### マウス左ドラッグで魚を選択する
![2020-09-19 (13)](https://user-images.githubusercontent.com/37477845/94047578-3e365700-fe0d-11ea-86b9-2d88ef24d0c0.png)
#### TAGSから「Fish」を選択する
南京錠のマークを選択しておくことでタグを使用するタグを固定することが可能
![2020-09-19 (14)](https://user-images.githubusercontent.com/37477845/94047588-41314780-fe0d-11ea-9574-0cb6c77f8be5.png)
<!-- #### 12
![2020-09-19 (15)](https://user-images.githubusercontent.com/37477845/94047598-442c3800-fe0d-11ea-9285-d72713520a65.png)-->
</details>

<details>
<summary>CSVエクスポート</summary>
	
#### エクスポート設定
プロバイダー：コンマ区切り値（CSV）<br>
アセットの状態：タグ付きアセットのみ<br>
「エクスポート設定を保存」を押下する
![2021-06-09 (8)](https://user-images.githubusercontent.com/37477845/121364839-1bd07380-c973-11eb-90ca-25e237abb6f5.png)
アノテーション画面からエクスポートマークを押下し、TFRecordをエクスポートする。
![2020-09-19 (14)](https://user-images.githubusercontent.com/37477845/94047588-41314780-fe0d-11ea-9574-0cb6c77f8be5.png)
</details>

# 2. Colaboratory：環境準備
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Kazuhito00/TFLite-ModelMaker-EfficientDet-Colab-Hands-On/blob/master/[Colaboratory]TFLite_ModelMaker_Hands_On.ipynb)<br>
以降の作業はGoogle Colaboratory上で実施します。<br>
[Open In Colab]リンクからノートブックを開き、以下の順に実行してください。
* パッケージインポート
* パッケージインストール

# 3.Colaboratory：object_detector向けcsv作成
「!mkdir dataset」実行後、VoTTからエクスポートした画像ファイルとCSVファイルを格納してください。<br>
格納後、以下を実行してください。<br>
アノテーション済みファイルを利用する方は以下の「if False:」を「if True:」に変更して実施してください。
```
if False:
    !git clone https://github.com/Kazuhito00/TFLite-ModelMaker-EfficientDet-Colab-Hands-On
    !cp -r "TFLite-ModelMaker-EfficientDet-Colab-Hands-On/02_dataset(Annotated)/*" "./dataset"
```
* データセットCSV読み込み(Read CSV)
* 学習データ/検証データ/テストデータ 分割
* object_detectorで読み込む形式に変換

# 4. Colaboratory：モデル訓練
以下の順に実行してください。
* Model MakerでCSVファイルを読み込む
* 物体検出のモデルアーキテクチャを選択
* 訓練
* モデル評価
* TensorFlow Lite形式でのモデルエクスポート(形式：完全整数量子化)
* TensorFlow Lite形式でのモデルエクスポート(形式：Float16量子化) 

# 5. Colaboratory：推論
以下の順に実行してください。
* 推論(形式：完全整数量子化)
* 推論(形式：Float16量子化) 

# Author
高橋かずひと(https://twitter.com/KzhtTkhs)
 
# License 
TFLite-ModelMaker-EfficientDet-Colab-Hands-On is under [MIT license](https://en.wikipedia.org/wiki/MIT_License).
