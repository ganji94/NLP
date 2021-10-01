# RNN Encoder-Decoder
RNN Reference:

  * [RNN reference blog][rnnblog1link]

[rnnblog1link]: https://22-22.tistory.com/25

RNN Encoder-Decoder Reference:

  * [NEURAL MACHINE TRANSLATION BY JOINTLY LEARNING TO ALIGN AND TRANSLATE (paper, May 2016)][paperlink]

[paperlink]: https://arxiv.org/pdf/1406.1078.pdf

  * [RNN Encoder-Decoder Reference blog][rnnedblog1link]

[rnnedblog1link]: https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=ckdgus1433&logNo=221608376139

## RNN
RNN is a network for sequential data.
Unlike other neural networks, RNN has a node called ***hidden state***, which contains ***input vector*** and ***result of previous hidden state***.
As ***result of previous hidden state*** is used as an input of next hidden state, RNN can contain ***sequential information of data***.

<p align="center">
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4Glvk%2FbtqEnhWV4fT%2F0pT6Vch1SqMlawCyAIg2P0%2Fimg.png" width="40%" height="30%" title="RNN"></img>
</p>

But there's significant issue of RNN, called ***Vanishing Gradient***. Vanishing Gradient indicates the lose of information in progress of delivering data,
and this is because of delivering mechanism of RNN. To solve this problem, LSTM (Long Short Term Memory) is made, which changed delivering mechanism inside hidden state.
<p align="center">
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhiMCH%2FbtqFcuVimHX%2Fxc0TTehp5mJGjRLpICnt11%2Fimg.png" width="40%" height="30%" title="RNN"></img>
</p>
<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?h_%7Bt%7D%20%3D%20tanh%28h_%7Bt-1%7DW_%7Bh%7D&plus;x_%7Bt%7DW_%7Bx%7D&plus;b%29" width="20%" height="20%"></img>
</p>

## RNN Encoder-Decoder
