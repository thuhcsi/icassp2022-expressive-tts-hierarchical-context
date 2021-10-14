---
layout: default
---
# Abstract

Previous works on expressive speech synthesis mainly focus on current sentence. The context in adjacent sentences is neglected, resulting in inﬂexible speaking style for the same text, which lacks speech variations. In this paper, we propose a hierarchical framework to model speaking style from context. A hierarchical context encoder is proposed to explore a wider range of contextual information considering structural relationship in context, including interphrase and inter-sentence relations. Moreover, to encourage this encoder to learn style representation better, we introduce a novel training strategy with knowledge distillation, which provides the target for encoder training. Both objective and subjective evaluations on a Mandarin lecture dataset demonstrate that the proposed method can signiﬁcantly improve the naturalness and expressiveness of the synthesized speech.

# Subjective Evaluation 
To demonstrate that our proposed model can significantly improve the naturalness and expressiveness of the synthesized speech, some samples are provided for comparison. **GT** means ground truth. **FastSpeech 2** means  original FastSpeech 2 with several changes consistent to the proposed model, and **XLNET-FastSpeech 2** means FastSpeech 2 with a plain context encoder without the use of inter-sentence relations, which are described in detail in the paper. In addition, a well-trained HIFI-GAN is used as the vocoder to generate waveform.

| Target Chinese Text | GT | FastSpeech 2 | XLNET-FastSpeech2 | Proposed |
| :---- | :---- | :---- | :---- | :---- |
| 那学着学着学着，是不是有一种望洋兴叹的感觉？ | <audio controls><source src="./wavs/gt/0.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/0.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/0.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/0.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 而恰恰是因为学的深，反而有可能过不了。 | <audio controls><source src="./wavs/gt/1.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/1.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/1.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/1.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 当然我也必须强调的是，每年都会有一道两道题很难。 | <audio controls><source src="./wavs/gt/2.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/2.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/2.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/2.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 我们所需要掌握的是保险诈骗的理论，而根本不需要去看法条。 | <audio controls><source src="./wavs/gt/3.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/3.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/3.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/3.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 这两种观点在今后我们所有的刑法问题中大家都会看到它们的分析。 | <audio controls><source src="./wavs/gt/4.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/4.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/4.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/4.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 从实质上来看，冒充军警人员抢劫都要判十年以上，那真警察抢劫是不更应该处十年以上了，是不这意思。 | <audio controls><source src="./wavs/gt/5.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/5.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/5.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/5.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 理解我的意思没有，但是这个案件毕竟是多年前的案件。 | <audio controls><source src="./wavs/gt/6.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/6.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/6.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/6.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 在二审期间那么就应该撤销案件啊宣判无罪。 | <audio controls><source src="./wavs/gt/8.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/8.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/8.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/8.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 但是我希望大家采取阶层论也要尊重四要件。 | <audio controls><source src="./wavs/gt/10.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/fs2/10.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/xlnet-fs2/10.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/proposed/10.wav" type="audio/wav">Your browser does not support the audio element.</audio> |


* * *


# Ablation Study 
### Investigation on speaker embeddings with different granularity 
To investigate the impact of local speaker embeddings with different granularity, we adjust the kernel size of average pooling layer in the downsample encoder. The number after CDFSE- represents the **overall downsampling times** in the temporal resolution compared with the reference mel-spectrogram. It can be observed that, with smaller downsampling times, more fine-grained local speaker embeddings can be extracted from reference audio, which can improve speaker similarity but result in deterioration of intelligibility.

| SpeakerID | Reference Audio | Target Chinese Text | CDFSE-1 | CDFSE-4 | CDFSE-16 | CDFSE-64 |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| SSB0112 | <audio controls><source src="./wavs/reference/SSB01120001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 一三三三七零八零七八七。 | <audio controls><source src="./wavs/cdfse-1/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0393 | <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 如新兴区域的望京奥运村地区。 | <audio controls><source src="./wavs/cdfse-1/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0710 | <audio controls><source src="./wavs/reference/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 甜心特工国语版。 | <audio controls><source src="./wavs/cdfse-1/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1020 | <audio controls><source src="./wavs/reference/SSB10200001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 将依据发行人的信息披露文件进行独立的投资判断。 | <audio controls><source src="./wavs/cdfse-1/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1630 | <audio controls><source src="./wavs/reference/SSB16300375.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 广州的电影有什么。 | <audio controls><source src="./wavs/cdfse-1/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> |


### Investigation on preprocessing operations
We have tried to remove the preprocessing operations (slice, shuffle & concatenate) mentioned in the paper 2.3 during training, and find it will result in synthesized speech with strange prosody and poor intelligibility for zero-shot inference.

| Reference Audio | Target Chinese Text | w preprocessing | w/o preprocessing |
| :---- | :---- | :---- | :---- |
| <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 看来我现在是个真正的作家了。 | <audio controls><source src="./wavs/cdfse-16/SSB03930007.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-woshuffle/SSB03930007.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| <audio controls><source src="./wavs/reference/SSB06060001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 智能硬件需要软件平台交互数据。 | <audio controls><source src="./wavs/cdfse-16/SSB06060003.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-woshuffle/SSB06060003.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| <audio controls><source src="./wavs/reference/SSB10200001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 私募债券的投资风险由投资者自行承担。 | <audio controls><source src="./wavs/cdfse-16/SSB10200104.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-woshuffle/SSB10200104.wav" type="audio/wav">Your browser does not support the audio element.</audio> |


* * *


# Case Study
We have plotted some alignment samples from reference attention module. It can be observed that the reference attention module successfully learns the right content alignment between reference audio and text, providing the interpretability of our proposed method.

**Sample 1**

Reference Audio: <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio>

Content: 仅在与之利益密切相关的特定事项上享有表决权。（jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 .）


| Target Chinese Text（Phoneme Sequence） | CDFSE | Reference Alignment |
| :---- | :---- | :---- |
| 你好。（ni2 hao3 .） | <audio controls><source src="./wavs/casestudy/L0.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L0.jpg" width="100%"> |
| 仅在表决权，仅在表决权。（jin3 zai4 biao3 jue2 quan2 , jin3 zai4 biao3 jue2 quan2 .） | <audio controls><source src="./wavs/casestudy/L1.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L1.jpg" width="100%"> |
| 仅在与之利益密切相关的特定事项上享有表决权。（jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 .） | <audio controls><source src="./wavs/casestudy/L2.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L2.jpg" width="100%"> |
| 仅在与之利益密切相关的特定事项上享有表决权，仅在与之利益密切相关的特定事项上享有表决权。（jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 , jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 .） | <audio controls><source src="./wavs/casestudy/L3.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L3.jpg" width="100%"> |
| 为了观察不同长度的对齐现象，我们今天就来合成一句非常长的句子试试看。（wei4 le2 guan1 cha2 bu4 tong2 chang2 du4 de5 dui4 qi2 xian4 xiang4 , wo3 men1 jin1 tian1 jiu4 lai2 he2 cheng2 yi2 ju4 fei1 chang2 chang2 de5 ju4 zi5 shi4 shi4 kan4 .） | <audio controls><source src="./wavs/casestudy/L4.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L4.jpg" width="100%"> |


**Sample 2**

Reference Audio: <audio controls><source src="./wavs/reference/SSB19350001.wav" type="audio/wav">Your browser does not support the audio element.</audio>

Content: 六十三万四千一百七十八。（liu4 shi2 san1 wan4 si4 qian1 yi1 bai3 qi1 shi2 ba1 .）

| Target Chinese Text（Phoneme Sequence） | CDFSE | Reference Alignment |
| :---- | :---- | :---- |
| 你好。（ni2 hao3 .） | <audio controls><source src="./wavs/casestudy/L5.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L5.jpg" width="80%"> |
| 六十三万。（liu4 shi2 san1 wan4 .） | <audio controls><source src="./wavs/casestudy/L6.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L6.jpg" width="80%"> |
| 六十三万四千一百七十八。（liu4 shi2 san1 wan4 si4 qian1 yi1 bai3 qi1 shi2 ba1 .） | <audio controls><source src="./wavs/casestudy/L7.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L7.jpg" width="80%"> |
| 八十七百一千四万三十六。（ba1 shi2 qi1 bai3 yi1 qian1 si4 wan4 san1 shi2 liu4 .） | <audio controls><source src="./wavs/casestudy/L8.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L8.jpg" width="80%"> |
| 为了观察不同长度的对齐现象，我们今天就来合成一句非常长的句子试试看。（wei4 le2 guan1 cha2 bu4 tong2 chang2 du4 de5 dui4 qi2 xian4 xiang4 , wo3 men1 jin1 tian1 jiu4 lai2 he2 cheng2 yi2 ju4 fei1 chang2 chang2 de5 ju4 zi5 shi4 shi4 kan4 .） | <audio controls><source src="./wavs/casestudy/L9.wav" type="audio/wav">Your browser does not support the audio element.</audio> |<img src="./wavs/casestudy/refalign_L9.jpg" width="80%">|





