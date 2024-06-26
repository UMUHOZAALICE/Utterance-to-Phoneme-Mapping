# Utterance-to-Phoneme Mapping
# Overview
This project aims to address the challenge of speech recognition by predicting the phonemes in a recording to generate more natural predictions regardless of how the words have been articulated in the speech recordings. A sequence of feature vectors derived from a speech recording goes into a network, and it will output the sequence of phoneme labels for the recording with sequence-to-sequence conversion using a sequence-to-sequence model titled Recurrent Neural Network.

The input to the model is a sequence of feature vectors (shown by the orange boxes) from a speech recording. The network must analyze the input sequence and generate the output phoneme sequence that best matches the audio. Since the output is sporadic, not time-synchronous, a two-step process is decomposed. Firstly, the neural network generates outputs at every time step to eliminate the uncertainty of knowing when to generate the (sporadic) outputs. Secondly, a dynamic programming (DP) search-like operation on the complete set of outputs generated by the network is performed to generate the actual final output.

This project demonstrates the use of sequence models (e.g., Recurrent Neural Network, RNN) to solve sequence-to-sequence problems, specifically implementing automatic speech recognition.

# Dataset
AudioDataset were used to successful train abd evlaute the model with 36091157 Train dataset samples, 1928204 Validation dataset samples and 1934138  Test dataset samples. The training and validation data comprise (sequences of feature vectors derived from) speech recordings, and the sequence of phonemes representing the transcription for each utterance. The transcriptions are not timealigned to the speech feature vectors. The test data only comprise speech recordings. 

# Modeling
A Recurrent Neural Network (RNN) named a Pyramid Bidirectional Long Short-Term Memory (pBLSTM) was used to implement this automatic speech recognition. A pBLSTM is part of a model called "Listen, Attend and Spell (LAS)." The LAS model consists of two components: a listener and a speller. The listener is a pyramidal RNN encoder that accepts filter phonemes as inputs. The speller is an attention-based recurrent network decoder that emits characters as outputs. The listener, which is a pyramidal RNN, converts low-level speech signals into higher-level features, and this is done using a pBLSTM. In each successive stacked pBLSTM layer, the time resolution is reduced by a factor of 2; this allows the model to handle longer sequences and capture more complex patterns in the data.  The model was trained using training data and validated using validation data. Later, the model was tested using testing data where the trained model was used to derive the transcriptions for them.

# Outcomes
This project allowed me to understand how to deal with sequence-to-sequence problems using sequence models. I learned how to set up GRU/LSTM models on PyTorch, use CNNs for feature extraction, handle sequential data, pad/pack batches of variable length data, train the model using CTC Loss, optimize the model, and implement decoders such as greedy and beam decoders. I also explored various architectures and hyperparameters to find the optimal solution and learned how to stage data to efficiently search through the space of solutions. Finally, I learned how to use objects from the PyTorch framework to build a GRU/LSTM-based model and deal with issues of data loading, memory usage, and arithmetic precision to maximize the time efficiency of training and inference. In addition, I performed hyperparameter tuning to ensure the model's performance.

# Hyperparameter Tuning
To achieve the best score, different parameters were tuned. Around 200 epochs were used, with a batch size of 32 and a learning rate of 3e-3, among other settings as stated in the configs cell.

# Results
Valid distance locally: 5.244, 
Test distance on Kaggle (public score): 5.58, 
Test distance on Kaggle (private score): 5.80
