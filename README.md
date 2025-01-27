## VC Client

[English](/README_en.md)

## What's New!

- v.1.5.1.15b

  - [RVC(Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI.git)の軽量化を行いました。精度や応答速度をわずかに落とすことでより低スペックな PC での稼働も可能になりました。

- v.1.5.1.15a

  - [RVC(Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI.git)に対応しました。

    hubert のモデルが必要になります。[このリポジトリ](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main)から`hubert_base.pt`をダウンロードして、バッチファイルがあるフォルダに格納してください。

# VC Client とは

[VC Client](https://github.com/w-okada/voice-changer)は[MMVC](https://github.com/isletennos/MMVC_Trainer), [so-vits-svc](https://github.com/svc-develop-team/so-vits-svc), [RVC(Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI)などの AI を使ったリアルタイムボイスチェンジャーのクライアントソフトウェアです。また、リアルタイムボイスチェンジャーで必要となるトレーニング用の音声の録音(MMVC 向け)アプリも提供しています。

[解説動画](https://www.nicovideo.jp/watch/sm41507891)

- MMVC のトレーニングについては[公式ノートブック](https://github.com/isletennos/MMVC_Trainer)をご利用ください。
- so-vits-svc のトレーニングについては[公式ノートブック](https://github.com/isletennos/MMVC_Trainer)をご利用ください。

# 特徴

1. 複数のプラットフォームで動作
   Windows, Mac(M1 等 Apple silicon), Linux, Google Colaboratory での動作をサポートしています。

2. 音声録音用アプリのインストールが不要
   音声録音を Github Pages にホストしてあるアプリケーション上で実行可能です。全てブラウザ上で動くため、特別なアプリケーションのインストールは不要です。また、完全にブラウザアプリケーションとして動くのでデータがサーバに送信されることもありません。

3. ボイチェンを別の PC 上で実行して負荷を分散
   本アプリケーションのリアルタイムボイスチェンジャーは、サーバ・クライアント構成で動きます。MMVC のサーバを別の PC 上で動かすことで、ゲーム実況など他の負荷の高い処理への影響を抑えながら動かすことができます。

![image](https://user-images.githubusercontent.com/48346627/206640768-53f6052d-0a96-403b-a06c-6714a0b7471d.png)

# 使用方法

詳細は[こちら](https://zenn.dev/wok/books/0004_vc-client-v_1_5_1_x)に纏まっています。

# (1) レコーダー（トレーニング用音声録音アプリ）

MMVC トレーニング用の音声を簡単に録音できるアプリです。
Github Pages 上で実行できるため、ブラウザのみあれば様々なプラットフォームからご利用可能です。
録音したデータは、ブラウザ上に保存されます。外部に漏れることはありません。

[録音アプリ on Github Pages](https://w-okada.github.io/voice-changer/)

[解説動画](https://youtu.be/s_GirFEGvaA)

# (2) プレイヤー（ボイスチェンジャーアプリ）

MMVC や so-vits-svc でボイチェンを行うためのアプリです。

大きく 3 つの方法でご利用できます。難易度順に次の通りです。

- Google Colaboratory での利用(MMVC のみ)
- 事前ビルド済みの Binary での利用
- Docker や Anaconda など環境構築を行った上での利用

本ソフトウェアや MMVC になじみの薄い方は上から徐々に慣れていくとよいと思います。

## (2-1) Google Colaboratory での利用(MMVC のみ)

Google が提供している機械学習プラットフォーム Colaboratory 上で実行できます。
MMVC のモデルをトレーニングが完了している場合、既に Colaboratory を利用していると思いますので、事前準備は必要ありません。ただし、ネットワーク環境や Colaboratory の状況によってボイスチェンジャのタイムラグが大きくなる傾向があります。

- [超簡単バージョン](https://github.com/w-okada/voice-changer/blob/master/VoiceChangerDemo_Simple.ipynb): 事前設定なしで Colab から実行できます。
- [普通バージョン](https://github.com/w-okada/voice-changer/blob/master/VoiceChangerDemo.ipynb): Google Drive と連携してモデルを読み込むことができます。

[解説動画](https://youtu.be/TogfMzXH1T0)

## (2-2) 事前ビルド済みの Binary での利用

実行形式のバイナリをダウンロードして実行することができます。
Windows 版と Mac 版を提供しています。

- Mac 版はダウンロードファイルを解凍したのちに、使用する VC に応じた`startHttp_xxx.command`をダブルクリックしてください。開発元を検証できない旨が示される場合は、再度コントロールキーを押してクリックして実行してください(or 右クリックから実行してください)。（詳細下記 \*1）

- Windows 版は、`ONNX(cpu,cuda),PyTorch(cpu)`版と `ONNX(cpu,cuda), PyTorch(cpu,cuda)`版と`ONNX(cpu,DirectML), PyTorch(cpu)`版を提供しています。環境に応じた zip ファイルをダウンロードしてください。ダウンロードした zip ファイルを解凍して、使用する VC に応じた VC に応じた`start_http_xxx.bat`を実行してください。

- 各種`startHttp_xxx.command`ファイル(mac)、`start_http_xxx.bat`ファイル(win)で起動できるボイスチェンジャは次の通りです。

| #   | バッチファイル(mac の場合は`.bat`を`.command`に読み替え) | 説明                                           |
| --- | -------------------------------------------------------- | ---------------------------------------------- |
| 1   | start_http_v13.bat                                       | MMVC v.1.3.x 系のモデルが使用できます。        |
| 2   | start_http_v15.bat                                       | MMVC v.1.5.x 系のモデルが使用できます。        |
| 3   | start_http_so-vits-svc_40.bat                            | so-vits-svc 4.0 系のモデルが使用できます。     |
| 4   | start_http_so-vits-svc_40v2.bat                          | so-vits-svc 4.0v2 系のモデルが使用できます。   |
| 5   | start_http_so-vits-svc_40v2_tsukuyomi.bat                | つくよみちゃんのモデルを使用します。(変更不可) |
| 6   | start_http_so-vits-svc_40v2_amitaro.bat                  | あみたろのモデルを使用します。(変更不可)       |
| 7   | start_http_RVC.bat                                       | RVC のモデルが使用できます。                   |

- リモートから接続する場合は、各種`.command`ファイル(mac)、`.bat`ファイル(win)の http が https に置き換わっているものを使用してください。

- Windows 環境で Nvidia の GPU をお持ちの方は多くの場合は `ONNX(cpu,cuda),PyTorch(cpu)`版で動きます。環境によって極まれに gpu が認識されない場合があります。その場合は `ONNX(cpu,cuda), PyTorch(cpu,cuda)`版の方をご利用ください。（サイズが大きく違います。）

- Windows 環境で Nvidia の GPU をお持ちでない方は多くの場合は `ONNX(cpu,DirectML), PyTorch(cpu) `版で動きます。

- Windows 環境で so-vits-svc 4.0/so-vits-svc 4.0v2 をお使いの場合は`ONNX(cpu,cuda), PyTorch(cpu,cuda)`版をご利用ください。

- so-vits-svc 4.0/so-vits-svc 4.0v2 やつくよみちゃんの動作には content vec のモデルが必要となります。こちらの[リポジトリ](https://github.com/auspicious3000/contentvec)から、ContentVec_legacy 500 のモデルをダウンロードして、実行する`startHttp_xxx.command`や`start_http_xxx.bat`と同じフォルダに配置してください。

- RVC(Retrieval-based-Voice-Conversion)の動作には hubert のモデルが必要になります。[このリポジトリ](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main)から`hubert_base.pt`をダウンロードして、バッチファイルがあるフォルダに格納してください。

| Version     | OS                                    | フレームワーク                        | link                                                                                       | サポート VC                                                         | サイズ |
| ----------- | ------------------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- | ------ |
| v.1.5.1.15b | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu)          | [通常](https://drive.google.com/uc?id=1nb5DxHQJqnYgzWFTBNxCDOx64__uQqyR&export=download)   | MMVC v.1.5.x, MMVC v.1.3.x, RVC                                     | 773MB  |
|             | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu,cuda)     | [通常](https://drive.google.com/uc?id=197U6ip9ypBSyxhIf3oGnkWfBP-M3Gc12&export=download)   | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 2794MB |
|             | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu)      | [通常](https://drive.google.com/uc?id=18Q9CDBnjgTHwOeklVLWAVMFZI-kk9j3l&export=download)   | MMVC v.1.5.x, MMVC v.1.3.x, RVC                                     | 488MB  |
|             | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu,cuda) | [通常](https://drive.google.com/uc?id=1rlGewdhvenv1Yn3WFOLcsWQeuo8ecIQ1&export=download)   | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 2665MB |
|             | <span style="color: red;">mac</span>  | ONNX(cpu), PyTorch(cpu)               | [normal](https://drive.google.com/uc?id=1saAe8vycI4zv0LRbvNmFLfYt0utGRWyZ&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 615MB  |

| Version     | OS                                    | フレームワーク                    | link                                                                                     | サポート VC                                                         | サイズ |
| ----------- | ------------------------------------- | --------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------- | ------ |
| v.1.5.1.15a | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu,cuda) | [通常](https://drive.google.com/uc?id=1lCo4P3D3QVvrl-0DRh305e34d_YmsI10&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 2641MB |

| Version    | OS                                    | フレームワーク                        | link                                                                                               | サポート VC                                                    | サイズ |
| ---------- | ------------------------------------- | ------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | ------ |
| v.1.5.1.14 | <span style="color: red;">mac</span>  | ONNX(cpu), PyTorch(cpu)               | [通常](https://drive.google.com/uc?id=1rI209apnDN9Gh47MZiGMxGPJ-PmCaixr&export=download)           | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2 | 581MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [つくよみちゃん](https://drive.google.com/uc?id=1ysTt0xOkWFSxyXfFm2GD7i5o22jce4B8&export=download) | -                                                              | 874MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [黄琴まひろ](https://drive.google.com/uc?id=1uZW-PSHttQuGXZf9vU7ZGufbYl-nIRs6&export=download)     | -                                                              | 872MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [あみたろ](https://drive.google.com/uc?id=1jc6YXcvt0_z1GezKSvqHQPYFmtZU2KaV&export=download)       | -                                                              | 872MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [黄琴海月](https://drive.google.com/uc?id=1ruaTdhrIJVdz__sDwZEeovzwxrk2ufLT&export=download)       | -                                                              | 873MB  |
|            | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu)          | [通常](https://drive.google.com/uc?id=1C6NPy2Dys6fBS-rWkiPSv0Ue46N44nT0&export=download)           | MMVC v.1.5.x, MMVC v.1.3.x                                     | 530MB  |
|            | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu,cuda)     | [通常](https://drive.google.com/uc?id=1X-vR-0ODhNeGBTUf9iINBFaBKeH3_jpJ&export=download)           | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2 | 2624MB |
|            | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu)      | [通常](https://drive.google.com/uc?id=14jwSVOS_3Yzm33qSVPdel7GeN3uCCCYT&export=download)           | MMVC v.1.5.x, MMVC v.1.3.x                                     | 417MB  |
|            | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu,cuda) | [通常](https://drive.google.com/uc?id=1hnYJoBNnW62QO3L9SLpFmAIgZWMs5bat&export=download)           | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2 | 2509MB |
|            | <span style="color: blue;">win</span> | -                                     | [つくよみちゃん](https://drive.google.com/uc?id=1QdeotmYP6nnoZt438kB8wvFbYF-C0bhq&export=download) | -                                                              | 823MB  |
|            | <span style="color: blue;">win</span> | -                                     | [黄琴まひろ](https://drive.google.com/uc?id=1IJJQj6CHcbyvTwZ5LF6GZSk7FLs5OK6o&export=download)     | -                                                              | 821MB  |
|            | <span style="color: blue;">win</span> | -                                     | [黄琴海月](https://drive.google.com/uc?id=1fiymPcoYzwE1yxyIfC_FTPiFfGEC2jA8&export=download)       | -                                                              | 823MB  |
|            | <span style="color: blue;">win</span> | -                                     | [あみたろ](https://drive.google.com/uc?id=1Vt4WBEOAz0EhIWs3ZRFIcg7ELtSHnYfe&export=download)       | -                                                              | 821MB  |

\*1 MMVC v.1.5.x は Experimental です。

\*2 つくよみちゃんはフリー素材キャラクター「つくよみちゃん」が無料公開している音声データを使用しています。（利用規約など、詳細は文末）

\*3 解凍や起動が遅い場合、ウィルス対策ソフトのチェックが走っている可能性があります。ファイルやフォルダを対象外にして実行してみてください。（自己責任です）

\*4 本ソフトウェアは開発元の署名しておりません。下記のように警告が出ますが、コントロールキーを押しながらアイコンをクリックすると実行できるようになります。これは Apple のセキュリティポリシーによるものです。実行は自己責任となります。

![image](https://user-images.githubusercontent.com/48346627/212567711-c4a8d599-e24c-4fa3-8145-a5df7211f023.png)

https://user-images.githubusercontent.com/48346627/212569645-e30b7f4e-079d-4504-8cf8-7816c5f40b00.mp4

## (2-3) Docker や Anaconda など環境構築を行った上での利用

本リポジトリをクローンして利用します。Windows では WSL2 の環境構築が必須になります。また、WSL2 上で Docker もしくは Anaconda などの仮想環境の構築が必要となります。Mac では Anaconda などの Python の仮想環境の構築が必要となります。事前準備が必要となりますが、多くの環境においてこの方法が一番高速で動きます。**<font color="red"> GPU が無くてもそこそこ新しい CPU であれば十分動く可能性があります </font>（下記のリアルタイム性の節を参照）**。

[WSL2 と Docker のインストールの解説動画](https://youtu.be/POo_Cg0eFMU)

[WSL2 と Anaconda のインストールの解説動画](https://youtu.be/fba9Zhsukqw)

## リアルタイム性

GPU を使用するとほとんどタイムラグなく変換可能です。

https://twitter.com/DannadoriYellow/status/1613483372579545088?s=20&t=7CLD79h1F3dfKiTb7M8RUQ

CPU でも最近のであればそれなりの速度で変換可能。

https://twitter.com/DannadoriYellow/status/1613553862773997569?s=20&t=7CLD79h1F3dfKiTb7M8RUQ

古い CPU( i7-4770)だと、1000msec くらいかかってしまう。

# Acknowledgments

- [立ちずんだもん素材](https://seiga.nicovideo.jp/seiga/im10792934)
- [いらすとや](https://www.irasutoya.com/)
- [つくよみちゃん](https://tyc.rei-yumesaki.net/)

```
  本ソフトウェアの音声合成には、フリー素材キャラクター「つくよみちゃん」が無料公開している音声データを使用しています。
  ■つくよみちゃんコーパス（CV.夢前黎）
  https://tyc.rei-yumesaki.net/material/corpus/
  © Rei Yumesaki
```

- [あみたろの声素材工房](https://amitaro.net/)
- [れぷりかどーる](https://kikyohiroto1227.wixsite.com/kikoto-utau)

# 利用規約

- リアルタイムボイスチェンジャーつくよみちゃんについては、つくよみちゃんコーパスの利用規約に準じ、次の目的で変換後の音声を使用することを禁止します。

```

■人を批判・攻撃すること。（「批判・攻撃」の定義は、つくよみちゃんキャラクターライセンスに準じます）

■特定の政治的立場・宗教・思想への賛同または反対を呼びかけること。

■刺激の強い表現をゾーニングなしで公開すること。

■他者に対して二次利用（素材としての利用）を許可する形で公開すること。
※鑑賞用の作品として配布・販売していただくことは問題ございません。
```

- リアルタイムボイスチェンジャーあみたろについては、あみたろの声素材工房様の次の利用規約に準じます。詳細は[こちら](https://amitaro.net/voice/faq/#index_id6)です。

```
あみたろの声素材やコーパス読み上げ音声を使って音声モデルを作ったり、ボイスチェンジャーや声質変換などを使用して、自分の声をあみたろの声に変換して使うのもOKです。

ただしその場合は絶対に、あみたろ（もしくは小春音アミ）の声に声質変換していることを明記し、あみたろ（および小春音アミ）が話しているわけではないことが誰でもわかるようにしてください。
また、あみたろの声で話す内容は声素材の利用規約の範囲内のみとし、センシティブな発言などはしないでください。
```

- リアルタイムボイスチェンジャー黄琴まひろについては、れぷりかどーるの利用規約に準じます。詳細は[こちら](https://kikyohiroto1227.wixsite.com/kikoto-utau/ter%EF%BD%8Ds-of-service)です。

# 免責事項

本ソフトウェアの使用または使用不能により生じたいかなる直接損害・間接損害・波及的損害・結果的損害 または特別損害についても、一切責任を負いません。
