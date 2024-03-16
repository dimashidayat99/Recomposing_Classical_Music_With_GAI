# Large Language Model - Generative Pretrained Transformer (GPT)
<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gpt/framework/GPT_framework.png/>
</p>
<p align="middle">
    <em>Exploratory GPT Framework.</em>
</p>

## Preprocessing

As shown in the framework figure above, the processing of data for GPT modelling start with the following processes:

1. Sampling: sampling process where only five midi file were used and only come from Chopin composed music.

2. Key Transposing: All the midi files underwent the key tranposing process where all the key of the songs will be transpose to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for their clef property where parts with treble clef property belongs to treble clef while parts with bass clef property belongs to bass clef.

4. Music Element ExtractionThe music element such as notes, chords and durations were extracted for each clef. The notes and chords are grouped together under the same feature while durations itself become another feature.

5. Dataframes Construction: Both features were used forming a dataframe. There are total 2 dataframes which represent treble and bass clef.

6. Data Transformation: Both dataframes were processed further for data transformation, where list of chords were changed to chords label and numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represent as categorical representative instead of numerical representative.

7. Feature Construction: After transormation, both features of notes and durations were combined together forming a new feature. This new feature (combined feature) is the only feature use for model training.

8. Label Encoding: The both dataframe later were encoded by using label encoding technique  where the categorical representation of data was changed to integer representation of data.

9. Training Data Construction: Finally, the sequence data of each clef was produced by extracting 100 sequence data from the dataframe.

The final product of the preprocessing stage is two data consist of 100 sequence of combined feature.

## Modelling 
This project used typically one model for each clef. Since there are two clef in total, therefore, there are total two identical model architecture were used for modelling stage.The architecture of GPT model start with the following architecture:

1. Input Layer: This layer receives the input data, which is the sequence of processed music elements. It does not perform any computations but passes the input to the next layer.
2. Embbeding Layers: The input layer was connected to embedding layers, the embedding layer which is a trainable vector embedding space is used to represent the discrete data as continous data in the form of vectors or embeddings and occupies a unique location in that space.
3. Positional Encoding: Then, the positional encoding was added to the embedding vector to process the information of the data order.
4. Transformer Block: Then, three transformer block was linearly connected with the previous layer. Each transformer block has similar architecture, where it contain multi head self attention connected linearly with dropout layer, layer normalization, feed forward network, another dropout layer and another layer normalization.
  * Multi Head Self Attention: The first component in the transformer block was multi head self attention which it allows the model to focus on different parts of the input sequence simultaneously by computing attention scores between different positions of the input. The outputs from different attention heads are concatenated and linearly transformed to retain information from different representation subspaces.
  * Dropout Layer: The second layer, the dropout is a regularization technique that helps prevent overfitting by randomly setting a fraction of input units to zero during training. This encourages the network to learn more robust features and reduces reliance on specific neurons.
  * Layer Normalization: Layer normalization normalizes the inputs of each layer to have a mean of zero and a standard deviation of one. This helps stabilize the training process and speeds up convergence.
  * Feed Foward Network: The feed foward network component consists of one or more fully connected layers with an activation function applied to the output of each layer. The feedforward network helps the model capture complex dependencies in the data.
  * Dropout Layer: Another dropout layer was applied after the feedforward network to further regularize the model and prevent overfitting.
  * Layer Normalization: Another layer normalization step aws applied after the second dropout layer to normalize the outputs of the feedforward network.

5. Dense Layer: The last layer of the GPT model is a dense layer with the neuron size of vocab size of combine features which give the output.

The final product of the models will be the generated a combination of notes and durations together (combined feature) in the form of probability across all combination of notes and durations used in the dataset.

## Music Generation 
The outputs of the models training are combination of notes and durations for both treble and bass clef data. Each of the outputs went through music generation processes to generate music. The processess is as follows:


 This output went through the top k sampling process where one from top ten of probability of combined feature was randomly select. The dataframe was constructed based on the selected value. Since there two clef, there are two total dataframe which are treble clef dataframe and bass clef dataframe. The dataframes underwent the inverse label encoding where the numerical representation of data will be transform to categorical data. The dataframe which contained only one feature which is the combine feature was splitted into two features for notes and durations. Each notes and durations were extracted from combined features to construct a new dataframe. The dataframe went through the inverse transformation to transform categorical representation of data to the initial data representation. The processed generated dataframes were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream. Both streams went through the stream balancing process where the both streams length were adjusted to make sure both length are similar (or almost similar). The balanced streams were submitted to the music score. The music score was used to generate the music in the form of music audio and music sheet.

 

1. Top K Sampling: The outputs (combination of notes and durations) were underwent the top k sampling process where one from top ten of them were randomly select.

2. Dataframe Construction: The dataframe was constructed based on selected combined notes and duratons. Since there two clef, there are two total dataframes which are treble clef dataframe and bass clef dataframe.

3. Inverse Label Encoding: The dataframes underwent the inverse label encoding where the integer representation of data were converted to categorical representation of data.

4. Feature Splitting: The dataframe which contained only one feature which is the combine feature was splitted into two features for notes and durations.

5. Dataframe Construction: The dataframes were constructed based on the splitted feature, where the notes and durations features was used to create a new dataframe.

6. Inverse Data Transformation: The dataframes went through the inverse data transformation where the categorical representation of data is transformed to original data representation.

7. Music Stream Construction: The processed generated dataframes were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream.

8. Stream Balancing: Both streams went through the stream balancing process where the both streams length were adjusted to make sure both length are similar (or almost similar).

9. Music Score Construction: The balanced streams were submitted to the music score. The music score was used to genete the music in the form of music audio and music sheet.

## Source code
The source code of the music generation using GPT model can be found in `model\gpt\source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/gpt/source_code). There two file there, the first file named as "[GPT_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gpt/source_code/GPT_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the begininng. While the second file which named as "[GPT_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/gpt/source_code/GPT_Music_Production.ipynb)", is the code for music production where different value of key and tempo were changed to develop a variability of music generated.


