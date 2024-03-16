# Autoregressive Model - LSTM

## LSTM Framework

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/lstm/framework/LSTM_framework.png/>
</p>
<p align="middle">
    <em>Exploratory LSTM Framework.</em>
</p>

## Preprocessing 

As shown in the framework figure above, the processing od data for VAE modelling start with the following processes:

1. Sampling: sampling process where only five midi file were used and only come from Chopin composed music.

2. Key Transposing: All the midi files underwent the key tranposing process where all the key of the songs will be transpose to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for their clef property where parts with treble clef property belongs to treble clef while parts with bass clef property belongs to bass clef.

4. Music Element ExtractionThe music element such as notes, chords and durations were extracted for each clef. The notes and chords are grouped together under the same feature while durations itself become another feature.

5. Dataframes Construction: Both features were used forming a dataframe. There are total 2 dataframes which represent treble and bass clef.

6. Data Transformation: Both dataframes were processed further for data transformation, where list of chords were changed to chords label and numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represent as categorical representative instead of numerical representative.

7. Label Encoding: After transormation, both dataframes were encoded by using label encoding technique where the categorical representation of data was changed to integer representation of data.

8. Datasets Construction: Finally, the sequence data tensor of each clef was produced by extracting 100 sequence data from the dataframe.

The final product of the preprocessing stage is two dataset tensor consist of 100 sequence of notes and durations.

## Modelling 

This project used typically one model for each clef. Therefore, there are total two identical models architecture were used for modelling stage. The architecture of LSTM model begins with the following architecture:

1. Input Layer: This layer receives the input data, which is the sequence of processed music elements. It does not perform any computations but passes the input to the next layer.

2. LSTM Layer: The input layer was connected to LSTM layer which is capable of learning long-term dependencies. In this layer, the LSTM units process the input sequences and learn to capture patterns in the data over time.

3. Dropout Layer: A dropout was applied to the architecture sequence. A dropout is a regularization technique used to prevent overfitting. It randomly sets a fraction of input units to zero during training, which helps to reduce the model's reliance on specific input features.

4. LSTM Layer: Another LSTM layer was added after the first dropout layer to further capture complex patterns in the data.

5. Dropout Layer: Another dropout layer was added after the second LSTM layer to regularize the model further.

6. LSTM Layer: The third LSTM layer was used continues to capture higher-level patterns in the data.

7. Dense Layer: Then dense layer was connected to the achitecture sequence. This dense layer is fully connected, meaning each neuron in this layer is connected to every neuron in the previous layer. It helps in learning complex patterns from the LSTM layers' outputs. The dense layer output was split into two separate paths.

8. Dense Layer (First Path): The first branch was connected to the dense layer with softmax activation function. The softmax activation function was used to transforms the raw outputs of the neural network into a vector of probabilities. This dense layer produces the output for the notes.

9. Dense Layer (Second Path): The second branch was also connected to another dense layer with softmax activation function where this layer for the second branch, which produces the output for the durations.

10. Model Loss: The loss function used in the LSTM model is sparse categorical crossentropy.

The final product of the models will be the generated notes and durations in the form of probability across all notes used and durations used in the dataset.

## Music Generation
The outputs of the model training are arrays of treble notes, treble durations, bass notes and bass durations. Each of the outputs went through music generation processes to generate music. The processess is as follows:

1. Top K Sampling: The outputs (notes and durations) were underwent the top k sampling process where one from top ten notes and one from top five durations were randomly select.

2. Dataframe Construction: The dataframe was constructed based on the select notes and durations. Since there two clef, there are two total dataframes which are treble clef dataframe and bass clef dataframe.

3. Inverse Label Encoding: The dataframes underwent the inverse label encoding where the integer representation of data were converted to categorical representation of data.

4. Inverse Data Transformation: The dataframes went through the inverse data transformation where the categorical representation of data is transformed to original data representation.

5. Music Stream Construction: The processed generated dataframes were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream.

6. Stream Balancing: Both streams went through the stream balancing process where the both streams length were adjusted to make sure both length are similar (or almost similar).

7. Music Score Construction: The balanced streams were submitted to the music score. The music score was used to genete the music in the form of music audio and music sheet.

## Source code
The source code of the music generation using LSTM model can be found in `model\lstm\source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/lstm/source_code). There two file there, the first file named as "[LSTM_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/lstm/source_code/LSTM_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the begininng. While the second file which named as "[LSTM_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/lstm/source_code/LSTM_Music_Production.ipynb)", is the code for music production where different value of key and tempo were changed to develop a variability of music generated.
