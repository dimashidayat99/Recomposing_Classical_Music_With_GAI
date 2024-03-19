# Large Language Model - Generative Pretrained Transformer (GPT)
<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gpt/framework/GPT_framework.png/>
</p>
<p align="middle">
    <em>GPT Model Framework.</em>
</p>

## Preprocessing

As shown in the framework figure above, the processing of data for GPT modeling starts with the following processes:

1. Sampling: sampling process where only five midi files were used and only came from Chopin-composed music.

2. Key Transposing: All the midi files underwent the key transposing process where all the keys of the songs will be transposed to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for its clef property where parts with treble clef property belong to treble clef while parts with bass clef property belong to bass clef.

4. Music Element ExtractionThe music elements such as notes, chords, and durations were extracted for each clef. The notes and chords are grouped under the same feature while durations themselves become another feature.

5. Dataframes Construction: Both features were used to form a data frame. There are a total of two data frames which represent treble and bass clef.

6. Data Transformation: Both data frames were processed further for data transformation, where lists of chords were changed to chords labels and the numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represented as categorical representative instead of numerical representative.

7. Feature Construction: After transformation, both features of notes and durations were combined forming a new feature. This new feature (combined feature) is the only feature used for model training.

8. Label Encoding: Both data frames later were encoded by using the label encoding technique where the categorical representation of data was changed to an integer representation of data.

9. Training Data Construction: Finally, the sequence data of each clef was produced by extracting 100 sequence data from the data frame.

The final product of the preprocessing stage is two data (treble and bass data) consisting of 100 sequences of combined feature.

## Modelling 
This project used typically one model for each clef. Since there are two clefs in total, therefore, there are a total of two identical model architectures were used for the modeling stage. The architecture of the GPT model starts with the following architecture:

1. Input Layer: This layer receives the input data, which is the sequence of processed music elements. It does not perform any computations but passes the input to the next layer.

2. Embedding Layers: The input layer was connected to embedding layers, the embedding layer which is a trainable vector embedding space is used to represent the discrete data as continuous data in the form of vectors or embeddings and occupies a unique location in that space.

3. Positional Encoding: Then, the positional encoding was added to the embedding vector to process the information of the data order.

4. Transformer Block: Then, three transformer blocks were linearly connected with the previous layer. Each transformer block has a similar architecture, where it contains multi-head self-attention connected linearly with a dropout layer, layer normalization, feed-forward network, another dropout layer, and another layer normalization.

    * Multi-head Self-Attention: The first component in the transformer block was multi-head self-attention which allows the model to focus on different parts of the input sequence simultaneously by computing attention scores between different positions of the input. The outputs from different attention heads are concatenated and linearly transformed to retain information from different representation subspaces.

    * Dropout Layer: The second layer, the dropout is a regularization technique that helps prevent overfitting by randomly setting a fraction of input units to zero during training. This encourages the network to learn more robust features and reduces reliance on specific neurons.

    * Layer Normalization: Layer normalization normalizes the inputs of each layer to have a mean of zero and a standard deviation of one. This helps stabilize the training process and speeds up convergence.

    * Feed Foward Network: The feed forward network component consists of one or more fully connected layers with an activation function applied to the output of each layer. The feedforward network helps the model capture complex dependencies in the data.
  
    * Dropout Layer: Another dropout layer was applied after the feedforward network to further regularize the model and prevent overfitting.
  
    * Layer Normalization: Another layer normalization step was applied after the second dropout layer to normalize the outputs of the feedforward network.

5. Dense Layer: The last layer of the GPT model is a dense layer with the neuron size of vocab size of combined feature which give the output.

The final product of the models will be the generated combination of notes and durations together (combined feature) in the form of probability across all combinations of notes and durations used in the dataset.

## Music Generation 
### Processing
The outputs of the model's training are a combination of note and duration (combined feature) for both treble and bass clef data. Each of the outputs went through music generation processes to generate music. The process is as follows:

1. Top K Sampling: The outputs (combination of notes and durations) underwent the top k sampling process where one from the top ten of them was randomly selected.

2. Dataframe Construction: The data frame was constructed based on a selected combination of notes and durations. Since there are two clef, there are two total data frames which are the treble clef dataframe and the bass clef dataframe.

3. Inverse Label Encoding: The data frames underwent inverse label encoding where the integer representation of data was converted to the categorical representation of data.

4. Feature Splitting: The data frame which contained only one feature which is the combined feature was split into two features for notes and durations.

5. Dataframe Construction: The data frames were constructed based on the split feature, where the notes and duration features were used to create a new data frame.

6. Inverse Data Transformation: The data frames went through the inverse data transformation where the categorical representation of data is transformed to the original data representation.

7. Music Stream Construction: The processed generated data frames were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream.

8. Stream Balancing: Both streams went through the stream balancing process where both stream's lengths were adjusted to make sure both lengths are similar (or almost similar).

9. Music Score Construction: The balanced streams were submitted to the music score. The music score was used to generate the music in the form of music audio and music sheet.

### Music Generated
The generated music by GPT model can be found in `music_generated` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gpt/music_generated). The music sheet can be seen at `music_generated\sheet` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gpt/music_generated/sheet) and music audio can be found at `music_generated\audio` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/gpt/music_generated/audio).

## Source code
The source code of the music generation using GPT model can be found in `model\gpt\source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/gpt/source_code). There two file there, the first file named as "[GPT_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gpt/source_code/GPT_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the begininng. While the second file which named as "[GPT_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gpt/source_code/GPT_Music_Production.ipynb)", is the code for music production where different value of key and tempo were changed to develop a variability of music generated.


