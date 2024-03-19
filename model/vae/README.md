# Variational AutoEncoder (VAE)

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/vae/framework/VAE_framework.png/>
</p>
<p align="middle">
    <em>VAE Model Framework.</em>
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

8. Array Constructions: After the label encoding process, the arrays were constructed from the data frames by extracting the 100 sequence data of each note and duration. There are four arrays produced in total which are treble notes, treble durations, bass notes, and bass durations.

9. One Hot Encoding: Each of the arrays went through one hot encoding process where the categorical representation of data was converted to a binary matrix format.

10. Flattening: Finally, each arrays were flattened to vocabulary size times the sequence length of the data. Note that since there are four arrays, there are 4 vocabulary sizes that represent the unique value of treble notes, unique value of treble durations, unique value of bass notes, and unique value of bass durations.

The final products of the preprocessing stage were the 4 processed arrays which consist of one hot sequence data which are treble notes, treble durations, bass notes, and bass durations.

## Modelling
The VAE architecture used is a variant of VAE itself, which is a novel architecture (to the best of my knowledge) for VAE which is named multi-VAE. Similar to the original VAE, it consists of two main components which are encoder and decoder. There are two encoders, two decoders, and two latent distributions for two features used (notes and durations). 

1. Note Encorder: The note encoder takes an input of the shape of input dimensionality for notes. Passes the input through three dense layers. The output of the third dense layer is split into two paths where one path calculates the mean of the latent variable, z for note. Another path calculates the log variance of latent variable z for note.

2. Duration Encoder: The duration encoder takes an input of the shape of input dimensionality for durations. Similar to the note encoder, it passes the input through three dense layers. The output of the third dense layer is split into two paths which are one path calculates the mean of the latent variable, z for duration. Another path calculates the log variance of the latent variable, z for the duration.

3. Combining Latent Variables: The outputs of the third dense layer from both the note and duration encoders are concatenated by using a concatenate layer. The concatenated output is passed through another dense layer.

4. Sampling Layers: There are a total two of sampling layers used to sample from the calculated mean and log variance of the latent distribution, z for note and duration. The sampled latent variable for note and duration are concatenated with the final layer of the combined latent variable to create a finalized note and duration latent distribution.

5. Decoder: Two separate decoders are defined for notes and durations. Each decoder takes the concatenated latent variable (finalized note or duration latent distribution) as input. The decoders consist of a dense layer followed by a dense layer with the output dimensionality of the respective input (for notes or durations), using a sigmoid activation function.

6. Model Setup: The note and duration encoders, along with their respective decoders, are combined into one VAE model which is named multi-VAE. The overall VAE takes both the note and duration inputs and outputs reconstructed notes and durations, using the decoders. This architecture allows the VAE to learn a joint latent representation for notes and durations, enabling the generation of sequences with coherent note and duration components. There are two multi-VAE models were used to generate music for bass and treble clef data.

7. Model Loss: The loss of VAE consists of the addition of two components which are reconstruction loss and Kullback-Liebler divergence term (KL term). The reconstruction loss is binary cross entropy while the KL term is defined as follows:

$$ Loss_{KL} = - \frac{1}{2}*(1 + \log{\sigma} - \mu^2 - \sigma^2 ) $$

where $\mu$ and $\sigma$ is mean and standard deviation of latent distribution. The VAE loss is defined as 

$$ Loss_{Vae} = Loss_{Reconstruction} + Loss_{KL}$$

Since there are two sets in total of latent varaibles for note and duration features, the total loss is defined as follows:

$$ Loss_{Total} =  Loss_{Vae Notes} + Loss_{Vae Durations}$$


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
The generated music by VAE model can be found in the `music_generated` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/vae/music_generated). The music sheet can be seen at the `music_generated\sheet` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/vae/music_generated/sheet) and music audio can be found at the `music_generated\audio` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/vae/music_generated/audio).

## Source code
The source code of the music generation using VAE model can be found in the `source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/vae/source_code). There two files there, the first file named as "[VAE_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/vae/source_code/VAE_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the data gathering until model saving. While the second file which named as "[VAE_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/vae/source_code/VAE_Music_Production.ipynb)", is the code for music production where different value of keys and tempos were changed to develop a variability of music generated.
