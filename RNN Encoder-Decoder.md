# RNN Encoder-Decoder

## RNN

---

### 1-1. Summary
A RNN is a network for sequential data.
Unlike other neural networks, the RNN has a node called ***hidden state*** (![image](https://user-images.githubusercontent.com/74042372/135587347-9fa7a6a5-2fee-4784-b09e-8b154b7cad3a.png)), which contains ***input vector*** (![image](https://user-images.githubusercontent.com/74042372/135587454-f1c41b31-cd4c-4996-ab56-4aeaeb7173b2.png)
) and ***previous hidden state*** (![image](https://user-images.githubusercontent.com/74042372/135587489-0af7e01e-957e-42b4-9086-339154c313a5.png)).
As ***previous hidden state*** is used as an input, the RNN can contain ***sequential information of data***.

<p align="center">
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4Glvk%2FbtqEnhWV4fT%2F0pT6Vch1SqMlawCyAIg2P0%2Fimg.png" width="30%" height="30%" title="RNN"></img>
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhiMCH%2FbtqFcuVimHX%2Fxc0TTehp5mJGjRLpICnt11%2Fimg.png" width="30%" height="40%" title="RNN"></img>
</p>

But there's a significant issue of the RNN, called ***vanishing gradient***. The vanishing gradient indicates the lose of information in progress of delivering data,
and this is because of delivering mechanism of the RNN.

---

### 1-2. Numerical Approach
The recurrent neural network (RNN) is a neural network that consists of a ***hidden state*** (![image](https://user-images.githubusercontent.com/74042372/135587347-9fa7a6a5-2fee-4784-b09e-8b154b7cad3a.png)) and an ***optional output*** (![image](https://user-images.githubusercontent.com/74042372/135587584-96f620b3-d6b7-4373-9c04-aebf45b957c3.png)
), which operates on a variable length sequence ![image](https://user-images.githubusercontent.com/74042372/135587704-335e9ce8-4d65-4cfc-b19e-191732be85b8.png). At each time step (![image](https://user-images.githubusercontent.com/74042372/135587747-20f0d359-baeb-4c18-867b-432a54349973.png)), ***current hidden state*** (![image](https://user-images.githubusercontent.com/74042372/135588245-74f3f724-93ef-498d-b714-c48fa40bd566.png)) of the RNN is updated by,

![image](https://user-images.githubusercontent.com/74042372/135588483-55de76ca-b37e-48cf-a942-114eab14ee4d.png),

where ![image](https://user-images.githubusercontent.com/74042372/135588686-2a034807-8f34-4bc7-b2cc-21f421a3fead.png) is a non-linear activation function,
![image](https://user-images.githubusercontent.com/74042372/135588577-b668e575-c8f4-49c2-923f-fad6705b1f48.png) is a previous hidden state,
and ![image](https://user-images.githubusercontent.com/74042372/135588738-11be4258-0b12-4fb4-87c1-048123f63c98.png) is a current time step's input.

The RNN can learn a ***probability distribution*** over a sequence by being trained to predict the next symbol in a sequence.
In that case, the output at each time step ***t*** is the ***conditional distribution***.
For example, a multinomial distribution (1-of-K conding) can be output using a softmax activation function,

![image](https://user-images.githubusercontent.com/74042372/135589612-f07bd23c-2771-45df-9275-68a041bd487c.png),
 
where ![image](https://user-images.githubusercontent.com/74042372/135590457-d3d87ec4-6061-4b17-aa66-bf9c50eac2c6.png) are the rows of a ***weight matrix*** (![image](https://user-images.githubusercontent.com/74042372/135590502-82e6b5d6-c8f4-4c95-b092-31c191957986.png)).
By combining these probabilities, we can compute the probability of the ***sequence*** (![image](https://user-images.githubusercontent.com/74042372/135590409-8a540924-e068-42f3-9f8a-d06c57d507cd.png)) using,

![image](https://user-images.githubusercontent.com/74042372/135571386-0416b047-e9ff-47a5-aeab-ab26538fba5d.png).

From this distribution, it is straightforward to sample a new sequence by iteratively sampling a symbol at eath time step.

---

## RNN Encoder-Decoder
### 2-1. Summary
RNN encoder-decoder is a neural network architecture that learns to ***encode*** a ***variable-length sequence*** into a ***fixed-length vector representation***,
and ***decode*** a given ***fixed-length vector representation*** into a ***variable-length sequence***.
We call this ***fixed-length vector representation*** as a ***context vector***.

<p align="center">
  <img src="https://machinelearningmastery.com/wp-content/uploads/2017/10/Depiction-of-Sutskever-Encoder-Decoder-Model-for-Text-Translation.png" width="60%" height="60%" title="RNN"></img>
<img src="https://lh3.googleusercontent.com/-e9nZHuOfYoI/X7o2lW8rkqI/AAAAAAAAOlI/83ixePcGfWQ3ZHoegDuhVJzLh7nYdt8QACLcBGAsYHQ/w586-h293/image.png" width="30%" height="30%" title="RNN"></img>
</p>

There are ***two key benefits*** using RNN encoder-decoder architecture, rather than using single RNN architecture.
  * By using a RNN encoder-decoder, we can train a single end-to-end model directly on source and target sentences
  * A RNN encoder-decoder can handle variable length input and output sequences of text

>An ***end-to-end model*** means, one neural network model which take over all kinds of other data processing steps.
For example, in speech recognition problem, to transfer an ***input audio clip*** (![image](https://user-images.githubusercontent.com/74042372/135589706-f27542c4-b7de-42cd-b28b-799ab800fa11.png)) into a ***ouput transcript*** (![image](https://user-images.githubusercontent.com/74042372/135589736-b2742ec2-c7fb-4093-9d61-54c2db28758e.png))
, there are data processing steps such as feature extracting(MFCC), finding phonemes (ML), etc. But, if we use end-to-end deep learning model, we can just put audio clip (![image](https://user-images.githubusercontent.com/74042372/135589706-f27542c4-b7de-42cd-b28b-799ab800fa11.png)) and get ***transcript*** (![image](https://user-images.githubusercontent.com/74042372/135589736-b2742ec2-c7fb-4093-9d61-54c2db28758e.png)) directly, without going through these steps.

### 2-2. Numerical Approach
A RNN encoder-decoder model is a general method to learn the conditional distribution over a ***variable-length sequence*** conditioned on yet ***another variable-length sequence*** ![image](https://user-images.githubusercontent.com/74042372/135579390-5499e71f-fc42-43d9-bbc1-ef86cb3b88ea.png), where input and output sequence ***lengths T and T' may differ***.

The ***encoder*** is an RNN that sequentially reads each symbol of an ***input sequence*** (![image](https://user-images.githubusercontent.com/74042372/135590170-6cee3090-6bee-4a36-aa25-de715284e8ab.png)).
As it reads eah symbol, the ***hidden state*** changes accrording to,

![image](https://user-images.githubusercontent.com/74042372/135588483-55de76ca-b37e-48cf-a942-114eab14ee4d.png).

After reading the end of the sequence (EOS), the ***hidden state becomes a summary of the whole input sequence***, which is the ***context vector*** (![image](https://user-images.githubusercontent.com/74042372/135590230-0e32c4ca-654c-4d46-9826-582892086f8b.png))
.

The ***decoder*** is another RNN which is trained to generate the output sequence, by predicting the next symbol ![image](https://user-images.githubusercontent.com/74042372/135587236-8e4d16ae-04e0-4f0a-9ab0-833a5d0f35b2.png) given the ***hidden state*** (![image](https://user-images.githubusercontent.com/74042372/135590825-d35462fd-0e42-481d-8242-b43688ca0a6f.png)). 

 
## Reference
1. RNN Reference:

  * [RNN reference blog][rnnblog1link]

[rnnblog1link]: https://22-22.tistory.com/25

2. RNN Encoder-Decoder Reference:

  * [NEURAL MACHINE TRANSLATION BY JOINTLY LEARNING TO ALIGN AND TRANSLATE (paper, May 2016)][paperlink]

[paperlink]: https://arxiv.org/pdf/1406.1078.pdf

  * [RNN Encoder-Decoder Reference Blog 1][rnnedblog1link]

[rnnedblog1link]: https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=ckdgus1433&logNo=221608376139

  * [RNN Encoder-Decoder Reference Blog 2][rnnedblog2link]

[rnnedblog2link]: https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=ckdgus1433&logNo=221608376139

  * [RNN Encoder-Decoder Reference Blog 3][rnnedblog3link]

[rnnedblog3link]: https://machinelearningmastery.com/encoder-decoder-recurrent-neural-network-models-neural-machine-translation/

  * [End-To-End Model Reference Video 1][rnnedvideo1link]

[rnnedvideo1link]: https://youtu.be/ImUoubi_t7s

