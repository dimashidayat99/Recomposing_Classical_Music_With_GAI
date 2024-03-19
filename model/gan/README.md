# Generative Adversarial Network (GAN)

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gan/framework/GAN_framework.png/>
</p>
<p align="middle">
    <em>GAN Model Framework.</em>
</p>

## Preprocessing
As shown in the framework figure above, the processing of data for GAN modeling starts with the following processes:

1. Sampling: sampling process where only three midi files were used and only came from Chopin-composed music.

2. Key Transposing: All the midi files underwent the key transposing process where all the keys of the songs will be transposed to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for its clef property where parts with treble clef property belong to treble clef while parts with bass clef property belong to bass clef.

4. Music Element ExtractionThe music elements such as notes, chords, and durations were extracted for each clef. The notes and chords are grouped under the same feature while durations themselves become another feature.

5. Dataframes Construction: Both features were used to form a data frame. There are a total of two data frames which represent treble and bass clef.

6. Data Transformation: Both data frames were processed further for data transformation, where lists of chords were changed to chords labels and numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represented as categorical representative instead of numerical representative.

7. Label Encoding: After transformation, both data frames were encoded by using the label encoding technique where the categorical representation of data was changed to the integer representation of data.

8. Array Constructions: After the label encoding process, the arrays were constructed from the data frames by extracting the 100 sequence data of each clef. There are two arrays produced in total which are treble array and bass array.

9. One Hot Encoding: Each of the arrays went through one hot encoding process where the categorical representation of data was converted to a binary matrix format which produced three-dimensional arrays of treble array and bass array. 

The final products of the preprocessing stage were the two processed arrays which consisted of one hot sequence data of the treble array and bass array. The arrays' shape is in a dimensional array where the dimension represents the sample size, sequence length, and feature number (one hot feature or vocabulary size of note + duration). 

## Modelling 
The architecture of the GAN model consists of two components which are generator and discriminator. The generator component begins with the following architectures:

1. Input Layer: The generator takes an input tensor with the shape of input dimensionality for input data which is batch size, sequence length, and number of features.

2. Flatten Layer: The input is flattened using flatten layer to convert the input data into one-dimensional.

3. Dense Layers: Three dense (fully connected) layers were used to transform the input into a higher-level representation. The final dense layer output was split into two separate paths.

4. Dense Layer (First Path): This branch predicts the notes, with a Dense layer producing an output of the shape of sequence length times the vocabulary size of notes.

5. Reshape Layer (First Path): A Reshape layer was used to reshape the output into the shape of (sequence length, and vocabulary size of notes).

6. Dense Layer (Second Path): This branch predicts the durations, with a Dense layer producing an output of the shape of sequence length times the vocabulary size of durations.

7. Reshape Layer (Second Path): A Reshape layer was used to reshape the output into the shape of (sequence length, and vocabulary size of durations).

8. Softmax Activation Function (Both Paths): The softmax activation is applied to both branches to get a probability distribution over the output dimensions.
   
10. Loss Function: The loss function used in the generator component is sparse categorical cross-entropy.

The final output is the concatenation of the two branches, resulting in an output of tensor of shape (sequence length, vocabulary size of notes + vocabulary size of durations).

The discriminator component begins with the following architectures: 

1. Input Layer: The discriminator takes a tensor with the same shape as the output of the generator which is (batch size, sequence length, vocabolary size of notes + vocabolary size of durations).

2. Dense Layer: This layer processes the input data and extracts features relevant to discriminating between real and fake sequences.

3. Dropout Layer: Dropout is applied to regularize the model and prevent overfitting by randomly setting a fraction of input units to 0 during training.

4. Dense Layer: Another dense layer was added to further refine the extracted features.

5. Dropout Layer: Another dropout layer is added after the second dense layer for additional regularization.

6. Dense Layer: A third dense layer was added, continuing to extract discriminative features.

7. Dense Layer: The dense layer or output layer consisting of a single unit with a sigmoid activation function was added to the final architecture. The sigmoid was used to produce a probability score indicating whether the input sequence was real or fake.

8. Loss Function: The loss function used in the discriminator component is binary cross-entropy.

This GAN architecture is designed to generate sequences of notes and durations for music generation. The generator aims to produce realistic sequences, while the discriminator aims to distinguish between real sequences (from the dataset) and fake sequences (generated by the generator). Through adversarial training, the generator learns to produce sequences that are indistinguishable from real sequences, improving over time.

## Music Generation
### Processing
The notes and durations from each generated array of treble and bass are extracted forming note and duration arrays. Therefore, the outputs of the model training are arrays of treble notes, treble durations, bass notes, and bass durations. Each of the outputs went through music generation processes to generate music. The process is as follows:

1. Top K Sampling: The outputs underwent the top k sampling process where one from the top ten notes and one from the top five durations were randomly selected.

2. Dataframe Construction: The dataframe was constructed based on the selected notes and durations. Since there are two clef, there are two total data frames which are the treble clef data frame and bass clef data frame.

3. Inverse Label Encoding: The data frames underwent inverse label encoding where the integer representation of data was converted to the categorical representation of data.

4. Inverse Data Transformation: The data frames went through the inverse data transformation where the categorical representation of data is transformed to the original data representation.

5. Music Stream Construction: The processed generated data frames were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream.

6. Stream Balancing: Both streams went through the stream balancing process where both stream's lengths were adjusted to make sure both lengths are similar (or almost similar).

7. Music Score Construction: The balanced streams were submitted to the music score. The music score was used to generate the music in the form of music audio and music sheet.

### Music Generated
The generated music by GAN model can be found in the `music_generated` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gan/music_generated). The music sheet can be seen at the `music_generated\sheet` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gan/music_generated/sheet) and music audio can be found at the `music_generated\audio` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gan/music_generated/audio).

## Source code
The source code of the music generation using GAN model can be found in the `model\gan\source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/gan/source_code). There two files there, the first file named as "[GAN_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gan/source_code/GAN_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the begininng. While the second file which named as "[GAN_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gan/source_code/GAN_Music_Production.ipynb)", is the code for music production where different values of keys and tempos were changed to develop a variability of music generated.
