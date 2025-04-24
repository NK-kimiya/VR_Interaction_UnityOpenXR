## 開発したもの 

目的：仮想空間(メタバース)上で音声通話をしながらコミュニケーションができるアプリで、「病気や障がいなどがきっかけで感じる孤独感を軽減したい」という目的でミニマムで開発を進めました。

[紹介記事](https://kimikou-blog.jp/prototypes/vr%e3%82%a2%e3%83%97%e3%83%aa/)

## 利用ツール：Unity、Django、Express、React

 [VR_Interaction_UnityOpenXR(Unity)](https://github.com/NK-kimiya/VR_Interaction_UnityOpenXR)　

 [VR_Interaction_API(Django)](https://github.com/NK-kimiya/VR_Interaction_API)　

 [VR_Interaction_signallingserver(Express)](https://github.com/NK-kimiya/VR_Interaction_signallingserver)　

 [VR_Interaction_WebRTC(React)](https://github.com/NK-kimiya/VR_Interaction_WebRTC)　

 ※下記の方法での実行を試しました。　
 
 Django、Express、Reactはホスティングサービス(RenderやHerokuなど)でホスティングを行い、Unityはビルドし、MetaQuest2に実行ファイルを送信　

---

## 入力設定ファイルの場所

使用ファイル：Assets/ActionAssets/InputActionForVR.inputactions　

## 🧭入力設定ファイルの設定 

・設定ファイルと作成したアクションマップとアクション、コントローラーの設定内容　



### 🎮 アクションマップ：CubeController

| アクション       | アクションタイプ | バインディング（入力） ：コントローラー                   | 解説 |
|------------------|------------------|---------------------------------------------|------|
| LiftUp           | Button           | `trigger [RightHand XR Controller]`         | トリガーを押すと「持ち上げ」操作 |
| ChangeColor      | Button           | `gripPressed [RightHand XR Controller]`     | グリップを押すと色が変わる |
| Move             | Button           | `gripPressed [RightHand XR Controller]`     | グリップを押すと移動（移動用にも使用） |

---

### 🧑‍💻 アクションマップ：Head（視点トラッキング）

| アクション       | アクションタイプ | バインディング（入力）： コントローラー                    | 解説 |
|------------------|------------------|---------------------------------------------|------|
| Position         | Pose             | `centerEyePosition [XR HMD]`               | HMD（ヘッドマウントディスプレイ）の位置 |
| Rotation         | Pose             | `centerEyeRotation [Open XR HMD]`          | HMDの回転角度（視点の方向） |

---

### ✋ アクションマップ：RightHand（位置・姿勢）

| アクション       | アクションタイプ | バインディング（入力）： コントローラー               | 解説 |
|------------------|------------------|---------------------------------------------|------|
| Position         | Pose             | `pointerPosition [RightHand XR Controller]` | 右手コントローラーの位置 |
| Rotation         | Pose             | `pointerRotation [RightHand XR Controller]` | 右手コントローラーの回転 |

---

### 🧤 アクションマップ：RightHandInteractions（操作）

| アクション        | アクションタイプ | バインディング（入力）：                    | 解説 |
|-------------------|------------------|------------------------------------------------|------|
| Select            | Button           | `gripPressed [RightHand XR Controller]`        | 掴む／選択（グリップ押下） |
| Activate          | Button           | `triggerPressed [RightHand XR Controller]`     | アクティブ化／実行（トリガー） |
| UIPress           | Button           | `triggerPressed [RightHand XR Controller]`     | UIを押す（トリガー） |
| RotateAnchor      | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで回転操作 |
| TranslateAnchor   | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで移動操作 |

---

### 🕹️ アクションマップ：RightHandLocomotion（移動）

| アクション        | アクションタイプ | バインディング（入力）：                        | 解説 |
|-------------------|------------------|------------------------------------------------|------|
| Move              | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで前後左右の移動 |
| Turn              | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで回転（左右） |

---

## 🧷 XR Controllerコンポーネントの設定

### プレハブ保存場所：Assets/Resources/XR Origin 21111

'''
XR Origin

 →Camera Offset

　　→Main Camera（HMDに連動）

　　→RightHand Controller（操作割り当て済）

　→LeftHand Controller（現在は未使用）
'''

### XR Controllerコンポーネントの変数の割り当て　

| XR Controller変数       | 割り当てるアクション名 |
|------------------------|------------------------|
| Position Action         | `RightHand/Position`   |
| Rotation Action         | `RightHand/Rotation`   |
| Select Action           | `RightHandInteractions/Select` |
| Activate Action         | `RightHandInteractions/Activate` |
| UI Press Action         | `RightHandInteractions/UIPress` |
| Rotate Anchor Action    | `RightHandInteractions/RotateAnchor` |
| Translate Anchor Action | `RightHandInteractions/TranslateAnchor` |


---

### 主なスクリプトと役割　

| スクリプト名      | 役割 |
|------------------------|------------------------|
| DataManager.cs        |  データの保存・読み込みなどを管理するクラス  |
| GmeManager.cs        | シーン遷移やステート管理   |
| PhotonManager.cs           | Photon Unity Networkinのネットワーク接続やルーム管理 |
| PlayerController.cs        | プレイヤーの移動・回転・アクションなど、中心的なプレイヤー制御スクリプト |
| Room.cs         | ネットワークの部屋（ルーム）を管理。参加・退出・部屋一覧表示などの処理 |
| SpawnManager.cs    | オブジェクトの生成管理。プレイヤーやアイテムなどのスポーン処理を一括で制御 |
| UIManager.cs | VR用UI表示・切り替え・操作管理を行うスクリプト |

## 🧪 動作検証手順（Meta Quest 2 用）

このプロジェクトは Meta Quest 2 を使用して、OpenXRベースのVR入力動作を検証できます。  
以下の手順でセットアップを行ってください。

## ⚠️ 前提条件：Django プロジェクトのデプロイについて

本Unityプロジェクトは、外部サーバーと通信してアバター情報などを取得するため、  
**別途 Django によるバックエンドAPIのデプロイが必要**です。　

[Django](https://github.com/NK-kimiya/VR_Interaction_API/tree/master)

---

### ✅ 1-1. Meta Quest 2 を開発者モードにする

VRビルドを行うには、Meta Quest 2 を「開発者モード」に設定する必要があります。

#### 🔗 開発者モードの有効化方法（公式ガイド）：
👉 [Meta公式ガイド：開発者モードの有効化](https://developer.oculus.com/documentation/unity/unity-enable-device/)

---

### ✅ 1-2. Photon Unity Networking (PUN) の導入

本プロジェクトでは、マルチプレイヤー通信に **Photon Unity Networking (PUN)** を使用しています。  
Unity内でPhotonを使用するには、以下の手順でセットアップを行ってください。

#### 📦 導入手順

1. Unity Asset Store または [Photon公式ダウンロードページ](https://www.photonengine.com/en-US/PhotonUnityNetworking) から **Photon Unity Networking (PUN 2)** をインポートします。
2. `PhotonServerSettings` に自分の **App ID** を設定（Photon公式サイトで無料アカウント登録して取得可能）
3. プロジェクト内の `PhotonManager.cs` などのスクリプトがネットワーク処理に対応します

#### 🔗 Photon公式ページ：
👉 [Photon Unity Networking (PUN) 公式サイト](https://www.photonengine.com/en-US/PhotonUnityNetworking)

---

### ✅ 2. Unityでプロジェクトを開く

1. このリポジトリをクローンする
2. Unity Hub で `VR_Interaction_UnityOpenXR` プロジェクトを開く
3. `Assets/Scenes/Title Scene.unity` を開く

---

### ✅ 3. スクリプト `PhotonManager.cs` の変更について

以下のスクリプトでは、Unityから外部APIへアクセスし、アバター番号を取得しています。  
使用しているURLは仮のものであり、**実際にDjangoプロジェクトをホスティングしているURLに変更してください。**
変更する箇所　→　
```cshar
"https://django-login-yggs.onrender.com"
```

---

#### 🔁 対象コード（`PhotonManager.cs`）

```csharp
string apiUrl = "https://django-login-yggs.onrender.com/api/get-avatar-number/";
```



### ✅ 4. Meta Quest 2 をUSBでPCに接続

- デバイス上で USB デバッグの許可を求められたら「許可」を選択
- UnityがMeta Quest 2を認識した状態にする

---

### ✅ 5. ビルドとデプロイ

1. Unity 上部メニューから  
   `File > Build Settings` を選択  
2. Platform を `Android` に設定し `Switch Platform`
3. `Scenes In Build` に `Title Scene`と`GameScene Scene` が含まれていることを確認
4. Meta Quest 2 が USB 接続されていることを確認したら `Build and Run` をクリック

---

### ✅ 6. ヘッドセットを装着して動作確認

- トリガーやスティック操作が、アクションに応じて反映されるかをチェック
- 掴む・色を変える・移動するなどの処理が正常に機能するかを確認

---

## 💡 補足コントローラー入力やHMDの動作がUnityのInput Systemと連携し、正しく反映されるように設定

### ✅ UnityでOpenXRを有効にする理由と設定方法

UnityのXR開発では、対象のVRデバイス（Meta Quest 2など）に対応した「XR規格（ランタイム）」を指定する必要があります。  
本プロジェクトでは、**OpenXR** を使用します。

---

### ✅ 設定手順（Unity内で行う）

1. Unity メニューから `Edit > Project Settings` を開く  
2. 左側のメニューで `XR Plug-in Management` を選択  
3. 上部タブで `Android` を選択（Meta Quest 2 はAndroidベース）  
4. 一覧の中から `OpenXR` にチェックを入れる ✅

---

### ✅ さらに推奨設定：Meta Questサポートを明示する

OpenXR の中でも、Meta Quest に最適化された機能群を使うために：

1. `Project Settings > XR Plug-in Management > OpenXR` を開く  
2. `Feature Groups` セクションで `Meta Quest Support` にチェックを入れる ✅

> これにより、Meta Quest 2 固有の入力や最適化が有効になります。

---

### 連携プロジェクト

📁[VR_Interaction_WebRTC(React)](https://github.com/NK-kimiya/VR_Interaction_WebRTC)　

-WebRTCを使用して、Web上で音声通話、ビデオ通話を行う　

-アカウントの作成とログインのリクエスト　

📁[VR_Interaction_API(Django)](https://github.com/NK-kimiya/VR_Interaction_API)　

-Reactでカウントの作成、ログイン処理のAPI　

-VRでユーザーIDを通したログイン処理のAPI　

📁 [VR_Interaction_signallingserver(Express)](https://github.com/NK-kimiya/VR_Interaction_signallingserver)　　

-ReactプロジェクトでWebRTCを実装する際のシグナリングサーバー




