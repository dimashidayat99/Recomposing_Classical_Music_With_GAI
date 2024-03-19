# Generative Adversarial Network (GAN)

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gan/framework/GAN_framework.png/>
</p>
<p align="middle">
    <em>GAN Framework.</em>
</p>

## Preprocessing
As shown in the framework figure above, the processing od data for GAN modelling start with the following processes:

1. Sampling: sampling process where only three midi file were used and only come from Chopin composed music.

2. Key Transposing: All the midi files underwent the key tranposing process where all the key of the songs will be transpose to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for their clef property where parts with treble clef property belongs to treble clef while parts with bass clef property belongs to bass clef.

4. Music Element ExtractionThe music element such as notes, chords and durations were extracted for each clef. The notes and chords are grouped together under the same feature while durations itself become another feature.

5. Dataframes Construction: Both features were used forming a dataframe. There are total 2 dataframes which represent treble and bass clef.

6. Data Transformation: Both dataframes were processed further for data transformation, where list of chords were changed to chords label and numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represent as categorical representative instead of numerical representative.

7. Label Encoding: After transormation, both dataframes were encoded by using label encoding technique where the categorical representation of data was changed to integer representation of data.

8. Array Constructions: After the label encoding process, the arrays were constructed from the dataframes by extracting the 100 sequence data of each clef. There are two arrays produced in total which are treble array and bass array.

9. One Hot Encoding: Each of the arrays went through one hot encoding process where the categorical representation of data were converted to a binary matrix format which produce three dimentional array of treble array and bass array. 

The final products of the preprocessing stage were the 2 processed array which consist of one hot sequence data which are treble array and bass array. The arrays' shape is in three dimensional array where the dimension represent the samples size, sequence length and features number (one hot faetures or vocabolary size of notes + durations). 

## Modelling 
The architecture of GAN model consist of two component which are generator and discriminator. The generator component begin with the following architectures:

1. Input Layer: The generator takes an input tensor with shape of input dimensionality for input data which is batch size, sequence length and number of features.

2. Flatten Layer: The input is flattened using flatten layer to convert the input data into a one dimensional.

3. Dense Layers: Three dense (fully connected) layers were used to transform the input into a higher-level representation.The final dense layer output was split into two separate paths.

4. Dense Layer (First Path): This branch predicts the notes, with a Dense layer producing an output of shape of sequence length times vocabolary size of notes.

5. Reshape Layer (First Path): A Reshape layer was used to reshape the output into shape of (sequence length, vocabolary size of notes).

6. Dense Layer (Second Path): This branch predicts the durations, with a Dense layer producing an output of shape of sequence length times vocabolary size of durations.

7. Reshape Layer (Second Path): A Reshape layer was used to reshape the output into shape of (sequence length, vocabolary size of durations).

8. Softmax Activation Function (Both Path): The softmax activation is applied to both branches to get a probability distribution over the output dimensions.
   
10. Loss Function: The loss function used in the generator component is sparse categorical crossentropy.

The final output is the concatenation of the two branches, resulting in a output of tensor of shape (sequence length, vocabolary size of notes + vocabolary size of durations).

The discriminator component begin with the following architectures: 

1. Input Layer: The discriminator takes a tensor with the same shape as the output of the generator which are (batch size,sequence length, vocabolary size of notes + vocabolary size of durations).

2. Dense Layer: This layer processes the input data and extracts features relevant to discriminating between real and fake sequences.

3. Dropout Layer: Dropout is applied to regularize the model and prevent overfitting by randomly setting a fraction of input units to 0 during training.

4. Dense Layer: Another dense layer was added to further refines the extracted features.

5. Dropout Layer: Another dropout layer is added after the second dense layer for additional regularization.

6. Dense Layer: A third dense layer was added, continues to extract discriminative features.

7. Dense Layer: The dense layer or output layer consists of a single unit with a sigmoid activation function was added to the final architecture. The sigmoid was used to produces a probability score indicating whether the input sequence is real or fake.

8. Loss Function: The loss function used in the discriminator component is binary crossentropy.

This GAN architecture is designed to generate sequences of notes and durations for music generation. The generator aims to produce realistic sequences, while the discriminator aims to distinguish between real sequences (from the dataset) and fake sequences (generated by the generator). Through adversarial training, the generator learns to produce sequences that are indistinguishable from real sequences, improving over time.

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
The generated music by GAN model can be found in `music_generated` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gan/music_generated). The music sheet can be seen at `music_generated\sheet` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gan/music_generated/sheet) and music audio can be found at `music_generated\audio` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gan/music_generated/audio).

## Source code
The source code of the music generation using GAN model can be found in `model\gan\source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/gan/source_code). There two file there, the first file named as "[GAN_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gan/source_code/LSTM_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the begininng. While the second file which named as "[GAN_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gan/source_code/LSTM_Music_Production.ipynb)", is the code for music production where different value of key and tempo were changed to develop a variability of music generated.
