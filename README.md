# Character-Level-Language-Model
I have constructed a character-level LSTM with PyTorch. The network will train character by character on some text, then generate new text character by character. As an example, I will train on Anna Karenina. This model will be able to generate new text based on the text from the book.
<p> The network is based on Andrej Karpathy's <a href="karpathy.github.io/2015/05/21/rnn-effectiveness/">post on RNNs</a> and <a href="https://github.com/karpathy/char-rnn"> implementation in Torch.</a> </p>
<p> This code implements multi-layer Recurrent Neural Network (RNN, LSTM, and GRU) for training/sampling from character-level language models. In other words the model takes one text file as input and trains a Recurrent Neural Network that learns to predict the next character in a sequence. The RNN can then be used to generate text character by character that will look like the original training data. </p>
<p> As a working example, suppose we only had a vocabulary of four possible letters “helo”, and wanted to train an RNN on the training sequence “hello”. This training sequence is in fact a source of 4 separate training examples: 1. The probability of “e” should be likely given the context of “h”, 2. “l” should be likely in the context of “he”, 3. “l” should also be likely given the context of “hel”, and finally 4. “o” should be likely given the context of “hell”. </p>

<p> Concretely, we will encode each character into a vector using top_k encoding (i.e. all zero except for a single one at the index of the character in the vocabulary), and feed them into the RNN one at a time with the step function. We will then observe a sequence of 4-dimensional output vectors (one dimension per character), which we interpret as the confidence the RNN currently assigns to each character coming next in the sequence. Here’s a diagram: </p>
