# RNN Encoder-Decoder

## RNN

---

### 1-1. Summary
A RNN is a network for sequential data.
Unlike other neural networks, a RNN has a node called ***hidden state (h)***, which contains ***input vector (x)*** and ***previous hidden state (h_{t-1})***.
As ***previous hidden state*** is used as an input, RNN can contain ***sequential information of data***.

<p align="center">
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4Glvk%2FbtqEnhWV4fT%2F0pT6Vch1SqMlawCyAIg2P0%2Fimg.png" width="30%" height="30%" title="RNN"></img>
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhiMCH%2FbtqFcuVimHX%2Fxc0TTehp5mJGjRLpICnt11%2Fimg.png" width="30%" height="40%" title="RNN"></img>
</p>

But there's a significant issue of a RNN, called ***vanishing gradient***. The vanishing gradient indicates the lose of information in progress of delivering data,
and this is because of delivering mechanism of a RNN.

---

### 1-2. Numerical Approach
A recurrent neural network (RNN) is a neural network that consists of a ***hidden state (h)*** and an ***optional output (y)***,
which operates on a variable length sequence ***x=(x1, ..., xt)***. At each time step ***t***, ***current hidden state (h_{t})*** of the RNN is updated by,

![image](https://user-images.githubusercontent.com/74042372/135570951-6556b277-ada8-4c19-8165-7c43565ea9bf.png)

where ***f*** is a non-linear activation function, ***h_{t-1}*** is a previous hidden state, and ***x_{t}*** is a current time step's input.

A RNN can learn a ***probability distribution*** over a sequence by being trained to predict the next symbol in a sequence.
In that case, the output at each time step ***t*** is the ***conditional distribution***.
For example, a multinomial distribution (1-of-K conding) can be output using a softmax activation function,

![image](https://user-images.githubusercontent.com/74042372/135570641-df5316d5-941e-48ca-b095-99e971a183ca.png)
 
where ***w_{j}*** are the rows of a weight matrix ***W***.
By combining these probabilities, we can compute the probability of the sequence ***x*** using,

![image](https://user-images.githubusercontent.com/74042372/135571386-0416b047-e9ff-47a5-aeab-ab26538fba5d.png)

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
For example, in speech recognition problem, to transfer an ***input audio clip (x)*** into a ***ouput transcript (y)***, there are data processing steps such as feature extracting(MFCC), finding phonemes (ML), etc. But, if we use end-to-end deep learning model, we can just put audio clip (x) and get transcript (y) directly, without going through these steps.



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

[rnnedvideo1link]: https://machinelearningmastery.com/encoder-decoder-recurrent-neural-network-models-neural-machine-translation/

