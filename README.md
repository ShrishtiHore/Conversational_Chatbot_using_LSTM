# Conversational Chatbot using LSTM

This project is to create conversational chatbot using Sequence to sequence LSTM models. Sequence to sequence learning is about training models to convert from one domain to sequences another domain.

**Code and Resources Used**

**Language:** Python 3.8

**Dataset:** [Chatterbot Kaggle English Dataset](https://www.kaggle.com/kausr25/chatterbotenglish)

**Pakages Used:** numpy, tensorflow, pickle, keras

**Model Used:** Seq2Seq LSTM model 

**API built:** Keras Functional API

----

#### Step 1: Data Extraction and Preprocessing 
- The dataset hails from [chatterbot/english on Kaggle](https://www.kaggle.com/kausr25/chatterbotenglish).com by [kausr25](https://www.kaggle.com/kausr25). - It contains pairs of questions and answers based on a number of subjects like food, history, AI etc

- Parse each .yml file:
1. Concatenate two or more sentences if the answer has two or more of them.
2. Remove unwanted data types which are produced while parsing the data.
3. Append <START> and <END> to all the answers.
4. Create a Tokenizer and load the whole vocabulary ( questions + answers ) into it.

- Three arrays required by the model are encoder_input_data, decoder_input_data and decoder_output_data
- Encoder_input-data: Tokenize the questions and Pad them to maximum length.
- Decoder_input-data: Tokenize the answers and Pad them to maximum length.
- Decoder_output-data: Tokenize the answers and Remove the first element from all the tokenized_answers. This is the <START> element which we added earlier.

#### Step 2: Defining the Encoder-Decoder Model
- The model will have Embedding, LSTM and Dense layers. The basic configuration is as follows:
1. 2 Input Layers : One for encoder_input_data and another for decoder_input_data.
2. Embedding layer : For converting token vectors to fix sized dense vectors. ( Note : Don't forget the  ask_zero=True argument here )
3. LSTM layer : Provide access to Long-Short Term cells.

#### Working :

- The encoder_input_data comes in the Embedding layer ( encoder_embedding ).
- The output of the Embedding layer goes to the LSTM cell which produces 2 state vectors ( h and c which are encoder_states )
- These states are set in the LSTM cell of the decoder.
- The decoder_input_data comes in through the Embedding layer.
- The Embeddings goes in LSTM cell ( which had the states ) to produce seqeunces.
![working](https://github.com/ShrishtiHore/Conversational_Chatbot_using_LSTM/blob/master/Visualizations/ende.PNG)

#### Long Short Term Memory (LSTM):
- Long Short-Term Memory (LSTM) networks are a type of recurrent neural network capable of learning order dependence in sequence prediction problems.
- This is a behavior required in complex problem domains like machine translation, speech recognition, and more.
- The success of LSTMs is in their claim to be one of the first implements to overcome the technical problems and deliver on the promise of recurrent neural networks.
![Illustrations](https://github.com/ShrishtiHore/Conversational_Chatbot_using_LSTM/blob/master/Visualizations/ill.PNG)
- LSTM network is comprised of different memory blocks called cells
(the rectangles that we see in the image).  
- There are two states that are being transferred to the next cell; the cell state and the hidden state. 
- The memory blocks are responsible for remembering things and manipulations to this memory is done through three major mechanisms, called gates.
- The key to LSTMs is the cell state, the horizontal line running through the top of the diagram.
- The cell state is kind of like a conveyor belt. It runs straight down the entire chain, with only some minor linear interactions. It’s very easy for information to just flow along it unchanged.
- The LSTM does have the ability to remove or add information to the cell state, carefully regulated by structures called gates.
- Gates are a way to optionally let information through. They are composed out of a sigmoid neural net layer and a pointwise multiplication operation.
- The sigmoid layer outputs numbers between zero and one, describing how much of each component should be let through. A value of zero means “let nothing through,” while a value of one means “let everything through!”
- LSTMs is Explained in much more detail in this Blogpost [Colah's Blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)

#### Step 4: Training the Model
- We train the model for a number of 150 epochs with RMSprop optimizer and categorical_crossentropy loss function.
- Model training accuracy = 0.96 ie; 96%

#### Step 5: Defining Inference Models
- **Encoder inference model :** Takes the question as input and outputs LSTM states ( h and c ).

- **Decoder inference model :** Takes in 2 inputs, one are the LSTM states ( Output of encoder model ), second are the answer input seqeunces ( ones not having the <start> tag ). It will output the answers for the question which we fed to the encoder model and its state values.
  
#### Step 6: Talking with our Chatbot
- First, we define a method str_to_tokens which converts str questions to Integer tokens with padding.
1. First, we take a question as input and predict the state values using enc_model.
2. We set the state values in the decoder's LSTM.
3. Then, we generate a sequence which contains the <start> element.
4. We input this sequence in the dec_model.
5. We replace the <start> element with the element which was predicted by the dec_model and update the state values.
6. We carry out the above steps iteratively till we hit the <end> tag or the maximum answer length.
  
#### Results

![otuput](https://github.com/ShrishtiHore/Conversational_Chatbot_using_LSTM/blob/master/chatbot_output.PNG)

#### References
1. https://colah.github.io/posts/2015-08-Understanding-LSTMs/
2. https://medium.com/predict/creating-a-chatbot-from-scratch-using-keras-and-tensorflow-59e8fc76be79
3. https://machinelearningmastery.com/gentle-introduction-long-short-term-memory-networks-experts/
4. https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21
5. https://www.analyticsvidhya.com/blog/2017/12/fundamentals-of-deep-learning-introduction-to-lstm/
