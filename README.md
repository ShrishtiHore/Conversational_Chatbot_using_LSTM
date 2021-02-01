# Conversational_Chatbot_using_LSTM

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







































we will assemble a seq2seq LSTM model using Keras Functional API to create a working Chatbot which would answer questions asked to it.

Chatbots have become applications themselves. You can choose the field or stream and gather data regarding various questions. We can build a chatbot for an e-commerce webiste or a school website where parents could get information about the school.

Messaging platforms like Allo have implemented chatbot services to engage users. The famous Google Assistant, Siri, Cortana and Alexa may have been build using simialr models.

The dataset is from Chatterbot Kaggle English Dataset.

LSTM - encoder and decoder input questions are tokenized.

The model will have Embedding, LSTM and Dense layers. The basic configuration is as follows.

2 Input Layers : One for encoder_input_data and another for decoder_input_data.
Embedding layer : For converting token vectors to fix sized dense vectors.
LSTM layer : Provide access to Long-Short Term cells.

Working :

The encoder_input_data comes in the Embedding layer ( encoder_embedding ).
The output of the Embedding layer goes to the LSTM cell which produces 2 state vectors ( h and c which are encoder_states )
These states are set in the LSTM cell of the decoder.
The decoder_input_data comes in through the Embedding layer.
The Embeddings goes in LSTM cell ( which had the states ) to produce seqeunces.

We train the model for a number of 150 epochs with RMSprop optimizer and categorical_crossentropy loss function.

model training accuracy = 0.96 ie; 96%

Converted our seq2seq model to a TensorFlow Lite model so that it can be used on edge devices.
