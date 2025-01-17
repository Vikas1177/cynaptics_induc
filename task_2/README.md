# TASK - 2
I have created a Hangman game above your baseline code.
I have change the model architecture by introducing Bi-diretion LSTM

## Why Bi-directional LSTM
1.Bi-directional LSTMs process data in both forward and backward directions, allowing the model to capture context from both past and future states. 
2.Hangman involves words of varying lengths. Bi-directional LSTMs are well-suited for handling sequences of different lengths, making them ideal for this task.
3.By considering the entire sequence of letters in the word, a bi-directional LSTM can better infer the likely letters in the blanks. For example, if the word is "elephant" and the current state is "e _ e _ _ a _ t", the model can use the context from both ends to predict that the missing letters are likely "l", "p", and "h".

