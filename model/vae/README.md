# Variational AutoEncoder (VAE)

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/vae/framework/VAE_framework.png/>
</p>
<p align="middle">
    <em>Exploratory VAE Framework.</em>
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

8. Array Constructions: After the label encoding process, the arrays were constructed from the dataframes by extracting the 100 sequence data of each notes and durations. There are four arrays produced in total which are treble notes, treble durations, bass notes and bass durations.

9. One Hot Encoding: Each of the arrays went through one hot encoding process where the categorical representation of data were converted to a binary matrix format.

10. Flatteing: Finally, each arrays were flattened to vocab size times sequence length of the data. Noted that since there are four arrays, there are 4 vocab size which represent unique value of treble notes, unique value of treble durations, unique value of bass notes and unique value of bass durations.

The final products of the preprocessing stage were the 4 processed array which consist of one hot sequence data which are treble notes, treble durations, bass notes and bass durations.

## Modelling
The VAE architecture used is a variant of VAE itself, which is a novel architcture (to the best of my knowledge) for VAE which named multi-VAE. Similar with the original VAE, it consist of two main components which are encoder and decoder. There are two encoder, two decorder and two latent distribution for two features used (notes and durations). 

1. Note Encorder: The note encoder takes an input of shape of input dimensionality for notes. Passes the input through three dense layers. The output of the third dense layer is split into two paths which are one path calculates the mean of the latent variable, z for note. Another path calculates the log variance of latent variable z for note.

2. Duration Encoder: The duration encorder takes an input of shape of input dimensionality for durations. Similar to the note encoder, it passes the input through three dense layers. The output of the third dense layer is split into two paths which are one path calculates the mean of the latent variable, z for duration. Another path calculates the log variance of latent variable, z for duration.

3. Combining Latent Variables: The outputs of the third dense layers from both the note and duration encoders are concatenated by using concatenate layer. The concatenated output is passed through another dense layer.

4. Sampling Layers: There are total two of sampling layer is used to sample from the calculated mean and log variance of latent distribution, z for note and duration. The sampled of latent variable for note and duration are concatenated with final layer of combined latent variable to create a finalize note and duration latent distribution.

5. Decoder: Two separate decoders are defined for notes and durations. Each decoder takes the concatenated latent variable (finalize note or duration latent distribution) as input. The decoders consist of a dense layer followed by a dense layer with the output dimensionality of the respective input (for notes or durations), using a sigmoid activation function.

6. Model Setup: The note and duration encoders, along with their respective decoders, are combined into one VAE model which named as multi-VAE. The overall VAE takes both the note and duration inputs and outputs reconstructed notes and durations, using the decoders. This architecture allows the VAE to learn a joint latent representation for notes and durations, enabling the generation of sequences with coherent note and duration components. There are two multi-VAE model were used to generate music for bass and treble clef data.

7. Model Loss: The loss of vae consist of addition two component which are reconstruction loss and Kullback-Liebler divergence term (KL term). The reconstruction loss is binary cross entropy while KL term is defined as follow:

$$ Loss_{KL} = - \frac{1}{2}*(1 + \log{\sigma} - \mu^2 - \sigma^2 ) $$

where $\mu$ and $\sigma$ is mean and standard deviation of latent distribution. The VAE loss is defined as 

$$ Loss_{Vae} = Loss_{Reconstruction} + Loss_{KL}$$

Since there are two sets in total of latent varaibles for notes and durations features, the total loss is defined as follows:

$$ Loss_{Total} =  Loss_{Vae Notes} + Loss_{Vae Durations}$$


## Music Generation

The outputs of the model training are arrays of treble notes, treble durations, bass notes and bass durations. Each of the outputs went through music generation processes to generate music. The processess is as follows:

1. Top K Sampling: The outputs (notes and durations) were underwent the top k sampling process where one from top ten notes and one from top five durations were randomly select.

2. Dataframe Construction: The dataframe was constructed based on the select notes and durations. Since there two clef, there are two total dataframes which are treble clef dataframe and bass clef dataframe.

3. Inverse Label Encoding: The dataframes underwent the inverse label encoding where the integer representation of data were converted to categorical representation of data.

4. Inverse Data Transformation: The dataframes went through the inverse data transformation where the categorical representation of data is transformed to original data representation.

5. Stream Construction: The processed generated dataframes were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream.

6. Stream Balancing: Both streams went through the stream balancing process where the both streams length were adjusted to make sure both length are similar (or almost similar).

7. Music Score Construction: The balanced streams were submitted to the music score. The music score was used to genete the music in the form of music audio and music sheet.
