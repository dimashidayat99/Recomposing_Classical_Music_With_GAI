# Autoregressive Model - LSTM

## LSTM Framework

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/lstm/framework/LSTM_framework.png/>
</p>
<p align="middle">
    <em>LSTM Model Framework.</em>
</p>

## Preprocessing 

As shown in the framework figure above, the processing of data for VAE modeling starts with the following processes:

1. Sampling: sampling process where only five midi files were used and only came from Chopin-composed music.

2. Key Transposing: All the midi files underwent the key transposing process where all the keys of the songs will be transposed to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for its clef property where parts with treble clef property belong to treble clef while parts with bass clef property belong to bass clef.

4. Music Element ExtractionThe music elements such as notes, chords, and durations were extracted for each clef. The notes and chords are grouped under the same feature while durations themselves become another feature.

5. Dataframes Construction: Both features were used to form a data frame. There are a total of two data frames which represent treble and bass clef.

6. Data Transformation: Both data frames were processed further for data transformation, where lists of chords were changed to chords labels and the numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represented as categorical representative instead of numerical representative.

7. Label Encoding: After transformation, both data frames were encoded by using the label encoding technique where the categorical representation of data was changed to integer representation of data.

8. Datasets Construction: Finally, the sequence data tensor of each clef was produced by extracting 100 sequence data from the data frame.

The final product of the preprocessing stage is two dataset tensors consisting of 100 sequences of notes and durations.

## Modelling 

This project used typically one model for each clef. Therefore, are total of two identical model architectures were used for the modeling stage. The architecture of the LSTM model begins with the following architecture:

1. Input Layer: This layer receives the input data, which is the sequence of processed music elements. It does not perform any computations but passes the input to the next layer.

2. LSTM Layer: The input layer was connected to the LSTM layer which is capable of learning long-term dependencies. In this layer, the LSTM units process the input sequences and learn to capture patterns in the data over time.

3. Dropout Layer: A dropout was applied to the architecture sequence. A dropout is a regularization technique used to prevent overfitting. It randomly sets a fraction of input units to zero during training, which helps to reduce the model's reliance on specific input features.

4. LSTM Layer: Another LSTM layer was added after the first dropout layer to further capture complex patterns in the data.

5. Dropout Layer: Another dropout layer was added after the second LSTM layer to regularize the model further.

6. LSTM Layer: The third LSTM layer was used to capture higher-level patterns in the data.

7. Dense Layer: The dense layer was connected to the architecture sequence. This dense layer is fully connected, meaning each neuron in this layer is connected to every neuron in the previous layer. It helps in learning complex patterns from the LSTM layers' outputs. The dense layer output was split into two separate paths.

8. Dense Layer (First Path): The first branch was connected to the dense layer with a softmax activation function. The softmax activation function was used to transform the raw outputs of the neural network into a vector of probabilities. This dense layer produces the output for the notes.

9. Dense Layer (Second Path): The second branch was also connected to another dense layer with a softmax activation function where this layer for the second branch, which produces the output for the duration.

10. Model Loss: The loss function used in the LSTM model is sparse categorical cross-entropy.

The final product of the models will be the generated notes and durations in the form of probability across all notes and durations used in the dataset.

## Music Generation
The outputs of the model training are arrays of treble notes, treble durations, bass notes, and bass durations. Each of the outputs went through music generation processes to generate music. The process is as follows:

1. Top K Sampling: The outputs (notes and durations) underwent the top k sampling process where one from the top ten notes and one from the top five durations were randomly selected.

2. Dataframe Construction: The dataframe was constructed based on the selected notes and durations. Since there are two clef, there are two total data frames which are the treble clef data frame and bass clef data frame.

3. Inverse Label Encoding: The data frames underwent inverse label encoding where the integer representation of data was converted to the categorical representation of data.

4. Inverse Data Transformation: The data frames went through the inverse data transformation where the categorical representation of data is transformed to the original data representation.

5. Music Stream Construction: The processed generated data frames were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream.

6. Stream Balancing: Both streams went through the stream balancing process where both stream's lengths were adjusted to make sure both lengths are similar (or almost similar).

7. Music Score Construction: The balanced streams were submitted to the music score. The music score was used to generate the music in the form of music audio and music sheet.

## Music Generated
The generated music by VAE model can be found in the `music_generated` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/lstm/music_generated). The music sheet can be seen at the `music_generated\sheet` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/lstm/music_generated/sheet) and music audio can be found at the `music_generated\audio` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/lstm/music_generated/audio).

## Source code
The source code of the music generation using LSTM model can be found in the `model\lstm\source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/lstm/source_code). There two file there, the first file named as "[LSTM_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/lstm/source_code/LSTM_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the data gathering until model saving. While the second file which named as "[LSTM_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/lstm/source_code/LSTM_Music_Production.ipynb)", is the code for music production where different value of key and tempo were changed to develop a variability of music generated.
