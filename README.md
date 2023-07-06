# 用深度学习和域外数据进行自动音乐混合

传统的音乐混合涉及到以干净的、单独的轨道形式记录乐器，并使用音频效果和专家知识（例如，混合工程师）将它们混合成最终的混合物。近年来，音乐制作任务的自动化已经成为一个新兴的领域，基于规则的方法和机器学习方法已经被探索出来。尽管如此，缺乏干燥或干净的乐器录音限制了这类模型的性能，与专业的人工混音相比仍有距离。我们探索是否可以使用域外数据，如湿的或处理过的多轨音乐录音，并重新利用它来训练有监督的深度学习模型，以弥补目前自动混音质量的差距。为了实现这一目标，我们提出了一种新颖的数据预处理方法，使模型能够进行自动音乐混合。我们还重新设计了一种用于评估音乐混合系统的聆听测试方法。我们通过使用经验丰富的混音工程师作为参与者的这种主观测试来验证我们的结果。

## 论文

有关工作的技术细节，请参见：

"[Automatic music mixing with deep learning and out-of-domain data.](https://arxiv.org/abs/2208.11428)"
[Marco A. Martínez-Ramírez](https://m-marco.com/about/)， [Wei-Hsiang Liao](https://jp.linkedin.com/in/wei-hsiang-liao-66283154)， [Giorgio Fabbro](https://twitter.com/GioFabbro)， [Stefan Uhlich](https://scholar.google.de/citations?user=hja8ejYAAAAJ&hl=de)， [Chihiro Nagashima](https://jp.linkedin.com/in/chihiro-nagashima-9473271aa)，和 [Yuki Mitsufuji](https://www.yukimitsufuji.com/)。 <br />
23rd International Society for Music Information Retrieval Conference (ISMIR), 2022年12月.

```
@inproceedings{martinez2022FxNormAutomix,
   title={Automatic music mixing with deep learning and out-of-domain data},
   author={Mart\'{i}nez-Ram\'{i}rez, Marco A. and Liao, Wei-Hsiang and Fabbro, Giorgio and Uhlich, Stefan and Nagashima, Chihiro and Mitsufuji, Yuki},
   booktitle={23rd International Society for Music Information Retrieval Conference (ISMIR)},<br />
   month={December},
   year={2022}
}
```
主项目页面: https://marco-martinez-sony.github.io/FxNorm-automix/

ArXiv论文: https://arxiv.org/abs/2208.11428

## 安装

```
  python setup.py install
```
```
  pip install -r requirements.txt
```

## 数据预处理--效果归一化

这个脚本计算训练数据集的平均特征，然后对训练分区和验证分区进行归一化。

```
  bash scripts/data_normalization.sh
```   

## 训练模型

以下脚本训练FxNorm-Automix（Ours）和 Wave-U-Net（WUN）模型。检查`config.py`文件在`configs/ISMIR`的超参数和数据集设置。

### 预先训练FxNorm-automix

```
  bash scripts/pretrain_fxnorm_automix.sh
```

### FxNorm-automix


```
  bash scripts/train_fxnorm_automix.sh
```


### WAVE-U-Net


```
  bash scripts/train_wun.sh
```



## 评估模型

这个脚本在给定的测试数据集上评估一个训练有素的模型；计算出混合和指标

```
  bash scripts/evaluate.sh
```


## 推理 

该脚本在给定的多轨制上运行推理功能 

```
  bash scripts/inference.sh
```
                          
## 训练过的模型

训练过的模型可以在`training/results`找到，它们的`config.py`文件在`configs/ISMIR`找到。

可用的模型有 *ours_S_La*， *ours_S_Lb*， *ours_S_pretrained*，和 *wun_S_Lb*。

## 计算的特征

在MUSDB18上计算的平均特征可以在`training/features/features_MUSDB18.npy`找到。

                 

## 脉冲响应(IR)

由于版权问题，我们的模型在训练、评估和推理过程中使用的IR不能公开。

然而，用户可以提供他们的IRs来增加数据。理想情况下，IRs的混响时间（RT）应该在2到4秒之前。 然而，用户可以提供他们的IRs来增加数据。理想情况下，IRs的混响时间（RT）应该在2到4秒之前。对于 "pre-reverb "IRs（在真实的干数据上做推理时），RT应该小于1.5秒之前。(支持立体声和单声道)

数据加载器希望每个IR都在一个单独的文件夹中，并命名为 impulse_response.wav
e.g. /path/to/IR/impulse-response-001/impulse_response.wav 

## Requirements

* librosa>=0.8.1
* psutil
* `pymixconsole` (`pip install git+https://github.com/csteinmetz1/pymixconsole`)
* `pyloudnorm` (`pip install git+https://github.com/csteinmetz1/pyloudnorm`)
* `aubio` (`pip install git+https://github.com/aubio/aubio`)
* scipy>=1.6.3
* soundfile
* soxbindings
* sty
* tensorboard
* setuptools==59.5.0
* torch==1.9.0

Please see [requirements.txt](https://github.com/sony/FxNorm-automix/blob/main/requirements.txt)

