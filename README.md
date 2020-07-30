# Conversational_Chatbot_using_LSTM

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
