## VC Client

## What's New!

- v.1.5.1.15b

  - We lightened [RVC(Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI.git). By slightly reducing the accuracy and response speed, it is now possible to operate on a lower-spec PC..

- v.1.5.1.15a

  - Support [RVC(Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI.git)

    You need to have the hubert model to use it. Please download `hubert_base.pt` from [this repository](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main) and store it in the folder where the batch file is located.

# What is VC Client

[VC Client](https://github.com/w-okada/voice-changer) is a client software for real-time voice changers that uses AI such as [MMVC](https://github.com/isletennos/MMVC_Trainer) and [so-vits-svc](https://github.com/svc-develop-team/so-vits-svc), [RVC(Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI). It also provides an app for recording training audio for real-time voice changers, specifically for MMVC.

- Please use the [official notebook](https://github.com/isletennos/MMVC_Trainer) for MMVC training.
- Please use the [official notebook](https://github.com/isletennos/MMVC_Trainer) for so-vits-svc training.

# Features

1. Cross-platform compatibility
   Supports Windows, Mac (including Apple Silicon M1), Linux, and Google Colaboratory.

2. No need to install a separate audio recording app
   Audio recording can be done directly on the application hosted on Github Pages. Since it runs entirely on the browser, there is no need to install any special application. Additionally, since it works entirely as a browser application, no data is sent to the server.

3. Distribute the load by running Voice Changer on a different PC
   The real-time voice changer of this application works on a server-client configuration. By running the MMVC server on a separate PC, you can run it while minimizing the impact on other resource-intensive processes such as gaming commentary.

![image](https://user-images.githubusercontent.com/48346627/206640768-53f6052d-0a96-403b-a06c-6714a0b7471d.png)

# usage

Details are summarized [here](https://zenn.dev/wok/books/0004_vc-client-v_1_5_1_x).

# (1) Recorder (Voice Recording App for Training)

This is an app that allows you to easily record training voice for MMVC. It can be run on Github Pages, making it available from various platforms with just a browser. The recorded data is saved in the browser and will not leak externally.

[Recorder app on Github Pages](https://w-okada.github.io/voice-changer/)

[Explanation video](https://youtu.be/s_GirFEGvaA)

# (2) Player (Voice Changer App)

This is an app for performing voice changes with MMVC and so-vits-svc.

It can be used in three main ways, in order of difficulty:

- Using Google Colaboratory (MMVC only)
- Using a pre-built binary
- Setting up an environment with Docker or Anaconda and using it

For those who are not familiar with this software or MMVC, it is recommended to gradually get used to it from the top.

## (2-1) Use on Google Colaboratory (MMVC only)

You can run it on Google's machine learning platform, Colaboratory. If you have already used Colaboratory, you do not need to prepare anything as the training of MMVC model has been completed. However, the voice changer may have a large time lag depending on the network environment or the situation of Colaboratory.

- [Simple version](https://github.com/w-okada/voice-changer/blob/master/VoiceChangerDemo_Simple.ipynb): You can run it from Colab without any prior setup.
- [Normal version](https://github.com/w-okada/voice-changer/blob/master/VoiceChangerDemo.ipynb): You can load the model by cooperating with Google Drive.

[Explanation video](https://youtu.be/TogfMzXH1T0)

## (2-2) Usage with pre-built binaries

You can download and run executable binaries.
We offer Windows and Mac versions.

- For Mac version, after unzipping the downloaded file, double-click the `startHttp_xxx.command` file corresponding to your VC. If a message indicating that the developer cannot be verified is displayed, please press the control key and click to run it again (or right-click to run it). (Details below \* 1)

- For Windows version, we offer `ONNX(cpu, cuda), PyTorch(cpu)` version, `ONNX(cpu, cuda), PyTorch(cpu, cuda)` version, and `ONNX(cpu, DirectML), PyTorch(cpu)` version. Please download the zip file corresponding to your environment. After unzipping the downloaded zip file, please run the `start_http_xxx.bat` file corresponding to your VC.

- The following voice changers can be launched with each `startHttp_xxx.command` file (Mac) and `start_http_xxx.bat` file (Windows).

| #   | Batch file                                | Description                                     |
| --- | ----------------------------------------- | ----------------------------------------------- |
| 1   | start_http_v13.bat                        | MMVC v.1.3.x series models can be used.         |
| 2   | start_http_v15.bat                        | MMVC v.1.5.x series models can be used.         |
| 3   | start_http_so-vits-svc_40.bat             | so-vits-svc 4.0 series models can be used.      |
| 4   | start_http_so-vits-svc_40v2.bat           | so-vits-svc 4.0v2 series models can be used.    |
| 5   | start_http_so-vits-svc_40v2_tsukuyomi.bat | Use Tsukuyomi-chan's model. (Cannot be changed) |
| 6   | start_http_so-vits-svc_40v2_amitaro.bat   | Use Amitaro's model. (Cannot be changed)        |
| 7   | start_http_RVC.bat                        | RVC series models can be used.                  |

- If you are connecting remotely, please use the `.command` file (Mac) or `.bat` file (Windows) with https instead of http.

- If you have an Nvidia GPU on Windows, it will usually work with the `ONNX(cpu,cuda),PyTorch(cpu)` version. In rare cases, the GPU may not be recognized, in which case please use the `ONNX(cpu,cuda), PyTorch(cpu,cuda)` version (which is much larger in size).

- If you do not have an Nvidia GPU on Windows, it will usually work with the `ONNX(cpu,DirectML), PyTorch(cpu)` version.

- If you are using `so-vits-svc 4.0`/`so-vits-svc 4.0v2` on Windows, please use the `ONNX(cpu,cuda), PyTorch(cpu,cuda)` version.

- To use `so-vits-svc 4.0`/`so-vits-svc 4.0v2` or `tsukuyomi-chan`, you need the content vec model. Please download the ContentVec_legacy 500 model from [this repository](https://github.com/auspicious3000/contentvec), and place it in the same folder as `startHttp_xxx.command` or `start_http_xxx.bat` to run.

- You need to have the hubert model to use RVC(Retrieval-based-Voice-Conversion). Please download `hubert_base.pt` from [this repository](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main) and store it in the folder where the batch file is located.

| Version     | OS                                    | フレームワーク                        | link                                                                                       | サポート VC                                                         | サイズ |
| ----------- | ------------------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- | ------ |
| v.1.5.1.15b | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu)          | [normal](https://drive.google.com/uc?id=1nb5DxHQJqnYgzWFTBNxCDOx64__uQqyR&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, RVC                                     | 773MB  |
|             | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu,cuda)     | [normal](https://drive.google.com/uc?id=197U6ip9ypBSyxhIf3oGnkWfBP-M3Gc12&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 2794MB |
|             | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu)      | [normal](https://drive.google.com/uc?id=18Q9CDBnjgTHwOeklVLWAVMFZI-kk9j3l&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, RVC                                     | 488MB  |
|             | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu,cuda) | [normal](https://drive.google.com/uc?id=1rlGewdhvenv1Yn3WFOLcsWQeuo8ecIQ1&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 2665MB |
|             | <span style="color: red;">mac</span>  | ONNX(cpu), PyTorch(cpu)               | [normal](https://drive.google.com/uc?id=1saAe8vycI4zv0LRbvNmFLfYt0utGRWyZ&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 615MB  |

| Version     | OS                                    | Framework                         | link                                                                                       | VC Support                                                          | Size   |
| ----------- | ------------------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- | ------ |
| v.1.5.1.15a | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu,cuda) | [normal](https://drive.google.com/uc?id=1lCo4P3D3QVvrl-0DRh305e34d_YmsI10&export=download) | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2, RVC | 2641MB |

| Version    | OS                                    | Framework                             | link                                                                                               | VC Support                                                     | Size   |
| ---------- | ------------------------------------- | ------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | ------ |
| v.1.5.1.14 | <span style="color: red;">mac</span>  | ONNX(cpu), PyTorch(cpu)               | [normal](https://drive.google.com/uc?id=1rI209apnDN9Gh47MZiGMxGPJ-PmCaixr&export=download)         | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2 | 581MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [Tsukuyomi-chan](https://drive.google.com/uc?id=1ysTt0xOkWFSxyXfFm2GD7i5o22jce4B8&export=download) | -                                                              | 874MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [Kikoto Mahiro](https://drive.google.com/uc?id=1uZW-PSHttQuGXZf9vU7ZGufbYl-nIRs6&export=download)  | -                                                              | 872MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [Amitaro](https://drive.google.com/uc?id=1jc6YXcvt0_z1GezKSvqHQPYFmtZU2KaV&export=download)        | -                                                              | 872MB  |
|            | <span style="color: red;">mac</span>  | -                                     | [Kikoto Kurage](https://drive.google.com/uc?id=1ruaTdhrIJVdz__sDwZEeovzwxrk2ufLT&export=download)  | -                                                              | 873MB  |
|            | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu)          | [normal](https://drive.google.com/uc?id=1C6NPy2Dys6fBS-rWkiPSv0Ue46N44nT0&export=download)         | MMVC v.1.5.x, MMVC v.1.3.x                                     | 530MB  |
|            | <span style="color: blue;">win</span> | ONNX(cpu,cuda), PyTorch(cpu,cuda)     | [normal](https://drive.google.com/uc?id=1X-vR-0ODhNeGBTUf9iINBFaBKeH3_jpJ&export=download)         | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2 | 2624MB |
|            | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu)      | [normal](https://drive.google.com/uc?id=14jwSVOS_3Yzm33qSVPdel7GeN3uCCCYT&export=download)         | MMVC v.1.5.x, MMVC v.1.3.x                                     | 417MB  |
|            | <span style="color: blue;">win</span> | ONNX(cpu,DirectML), PyTorch(cpu,cuda) | [normal](https://drive.google.com/uc?id=1hnYJoBNnW62QO3L9SLpFmAIgZWMs5bat&export=download)         | MMVC v.1.5.x, MMVC v.1.3.x, so-vits-svc 4.0, so-vits-svc 4.0v2 | 2509MB |
|            | <span style="color: blue;">win</span> | -                                     | [Tsukuyomi-chan](https://drive.google.com/uc?id=1QdeotmYP6nnoZt438kB8wvFbYF-C0bhq&export=download) | -                                                              | 823MB  |
|            | <span style="color: blue;">win</span> | -                                     | [Kikoto Mahiro](https://drive.google.com/uc?id=1IJJQj6CHcbyvTwZ5LF6GZSk7FLs5OK6o&export=download)  | -                                                              | 821MB  |
|            | <span style="color: blue;">win</span> | -                                     | [Kikoto Kurage](https://drive.google.com/uc?id=1fiymPcoYzwE1yxyIfC_FTPiFfGEC2jA8&export=download)  | -                                                              | 823MB  |
|            | <span style="color: blue;">win</span> | -                                     | [Amitaro](https://drive.google.com/uc?id=1Vt4WBEOAz0EhIWs3ZRFIcg7ELtSHnYfe&export=download)        | -                                                              | 821MB  |

\*1 MMVC v.1.5.x is Experimental.

\*2 Tsukuyo Michan uses free character "Tsukuyo Michan" voice data that is publicly available for free. (Details such as terms of use are at the end of the document)

\*3 If unpacking or starting is slow, there is a possibility that virus checking is running on your antivirus software. Please try running it with the file or folder excluded from the target. (At your own risk)

\*4 This software is not signed by the developer. A warning message will appear, but you can run the software by clicking the icon while holding down the control key. This is due to Apple's security policy. Running the software is at your own risk.

![image](https://user-images.githubusercontent.com/48346627/212567711-c4a8d599-e24c-4fa3-8145-a5df7211f023.png)

https://user-images.githubusercontent.com/48346627/212569645-e30b7f4e-079d-4504-8cf8-7816c5f40b00.mp4

## (2-3) Usage after setting up the environment such as Docker or Anaconda

Clone this repository and use it. Setting up WSL2 is essential for Windows. Additionally, setting up virtual environments such as Docker or Anaconda on WSL2 is also required. On Mac, setting up Python virtual environments such as Anaconda is necessary. Although preparation is required, this method works the fastest in many environments. **<font color="red"> Even without a GPU, it may work well enough with a reasonably new CPU </font>(refer to the section on real-time performance below)**.

[Explanation video on installing WSL2 and Docker](https://youtu.be/POo_Cg0eFMU)

[Explanation video on installing WSL2 and Anaconda](https://youtu.be/fba9Zhsukqw)

## Real-time performance

Conversion is almost instantaneous when using GPU.

https://twitter.com/DannadoriYellow/status/1613483372579545088?s=20&t=7CLD79h1F3dfKiTb7M8RUQ

Even with CPU, recent ones can perform conversions at a reasonable speed.

https://twitter.com/DannadoriYellow/status/1613553862773997569?s=20&t=7CLD79h1F3dfKiTb7M8RUQ

With an old CPU (i7-4770), it takes about 1000 msec for conversion.

# Acknowledgments

- [Tachizunda-mon materials](https://seiga.nicovideo.jp/seiga/im10792934)
- [Irasutoya](https://www.irasutoya.com/)
- [Tsukuyomi-chan](https://tyc.rei-yumesaki.net)

> This software uses the voice data of the free material character "Tsukuyomi-chan," which is provided for free by CV. Yumesaki Rei.
>
> - Tsukuyomi-chan Corpus (CV. Yumesaki Rei)
>
> https://tyc.rei-yumesaki.net/material/corpus/
>
> Copyright. Rei Yumesaki

- [Amitaro's Onsozai kobo](https://amitaro.net/)
- [Replica doll](https://kikyohiroto1227.wixsite.com/kikoto-utau)

# Terms of Use

In accordance with the Tsukuyomi-chan Corpus Terms of Use for the Tsukuyomi-chan Real-time Voice Changer, the use of the converted voice for the following purposes is prohibited.

- Criticizing or attacking individuals (the definition of "criticizing or attacking" is based on the Tsukuyomi-chan character license).

- Advocating for or opposing specific political positions, religions, or ideologies.

- Publicly displaying strongly stimulating expressions without proper zoning.

- Publicly disclosing secondary use (use as materials) for others.
  (Distributing or selling as a work for viewing is not a problem.)

Regarding the Real-time Voice Changer Amitaro, we prohibit the following uses in accordance with the terms of use of the Amitaro's koe-sozai kobo.[detail](https://amitaro.net/voice/faq/#index_id6)

Regarding the Real-time Voice Changer Kikoto Mahiro, we prohibit the following uses in accordance with the terms of use of Replica doll.[detail](https://kikyohiroto1227.wixsite.com/kikoto-utau/ter%EF%BD%8Ds-of-service)

# Disclaimer

We are not liable for any direct, indirect, consequential, incidental, or special damages arising out of or in any way connected with the use or inability to use this software.
