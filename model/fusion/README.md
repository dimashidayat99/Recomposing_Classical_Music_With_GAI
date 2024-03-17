# Fusion Model - RNN-VAE-GAN

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/fusion/framework/FUS_framework.png/>
</p>
<p align="middle">
    <em>Fusion Model Framework.</em>
</p>

## Preprocessing
As shown in the framework figure above, the processing od data for Fusion Model modelling start with the following processes:

1. Sampling: sampling process where only five midi file were used and only come from Chopin composed music.

2. Key Transposing: All the midi files underwent the key tranposing process where all the key of the songs will be transpose to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for their clef property where parts with treble clef property belongs to treble clef while parts with bass clef property belongs to bass clef.

4. Music Element ExtractionThe music element such as notes, chords and durations were extracted for each clef. The notes and chords are grouped together under the same feature while durations itself become another feature.

5. Dataframes Construction: Both features were used forming a dataframe. There are total 2 dataframes which represent treble and bass clef.

6. Data Transformation: Both dataframes were processed further for data transformation, where list of chords were changed to chords label and numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represent as categorical representative instead of numerical representative.

7. Label Encoding: After transormation, both dataframes were encoded by using label encoding technique where the categorical representation of data was changed to integer representation of data.

8. Array Constructions: After the label encoding process, the arrays were constructed from the dataframes by extracting the 100 sequence data of each notes and durations. There are four arrays produced in total which are treble notes, treble durations, bass notes and bass durations.

9. One Hot Encoding: Each of the arrays went through one hot encoding process where the categorical representation of data were converted to a binary matrix format.

10. Flattening: Finally, each arrays were flattened to vocab size times sequence length of the data. Noted that since there are four arrays, there are 4 vocab size which represent unique value of treble notes, unique value of treble durations, unique value of bass notes and unique value of bass durations.

The final products of the preprocessing stage were the 4 processed array which consist of one hot sequence data which are treble notes, treble durations, bass notes and bass durations.

## Modelling 
The fusion model used the combination of RNN, VAE and GAN. Each of the architecture is implemented together forming a new model. The main architecture of RNN-VAE-GAN is a GAN model where it consist two main component which are generator and discriminator. In this model, the variant of GAN was used namely MDGAN which stand for Multiple Discrimninator Generative Adversial Network. As its name, there are more than one discriminator in this model. The generator component used the VAE architecture in its architecture and the RNN (GRU) architecture was used in the encoder part of VAE. The architecture of generator component in fusion models is as follows:

Encoder Note and Duration:

1. Input Layers: The encoder start with input layers where this layer receives the input data, which is the sequence of processed music elements. It does not perform any computations but passes the input to the next layer. There are two input layers was used for each input which are notes and durations.

2. Reshape Layers: The reshape layer was added after the input layer, this layer reshape the shape of inputs reshaped to (sequence_length, vocabolary size of notes) and (sequence_length, vocabolary size of durations) for notes and durations input respectively.

3. Concatenate Layer: The concatenate layer was added after reshape layer to concatenates the inputs for processing together.

4. GRU Layers: Three GRU layers was added after concatenate layer, each of GRU layer processes the concatenated reshaped input sequence by learns to capture temporal dependencies in the input data and outputs a sequence of hidden states.

5. Dense Layer: The dense layer processes the final hidden state from the last GRU layer and produces the output.

6. LeakyReLU activation: After the dense layer, LeakyReLU activation is applied where it helps by allowing a small gradient for negative inputs, Leaky ReLU ensures that even neurons that have a negative input can still contribute to the learning process, helping the network to learn more effectively. The outputs from this activation was split into two separate paths.

7. Dense Layer + LeakyReLU (First Path): The first branch was connected to the dense layer with addition of LeakyReLU activation functions. The output of this layer is connected to another dense layer together with LeakyReLU activations functions.

8.  Dense Layer + LeakyReLU (Second Path):  The first branch was connected to the dense layer with addition of LeakyReLU activation functions. This is the path of durations output. The output of this layer is connected to another dense layer together with LeakyReLU activations functions.

9.  Dense Layer (First Path): The dense layer with Leaky ReLU of previous layer was connected to another dense layer (this layer). The output of the this dense layer is split into two paths which are one path calculates the mean of the latent variable, z for note. Another path calculates the log variance of latent variable z for note. 

10. Dense Layer (Second Path): The dense layer with Leaky ReLU of previous layer was connected to another dense layer (this layer). The output of the this dense layer is split into two paths which are one path calculates the mean of the latent variable, z for duration. Another path calculates the log variance of latent variable, z for duration.

11. Concatenate Layers: The outputs of the final dense layers from both paths are concatenated by using concatenate layer. The concatenated output is passed through another dense layer forming combined latent distribution.

12. Sampling Layers: There are total two of sampling layer is used to sample from the calculated mean and log variance of latent distribution, z for note and duration. The sampled of latent variable for note and duration are concatenated with final layer of combined latent variable to create a finalize note and duration latent distribution.


Decoder Note and Duration:

1. Input Layers: The decoder start with input layers where this layer receives the the concatenated latent variable (finalize note or duration latent distribution).There are two input layers was used for each input which are note and duration latent distribution.

2. Dense Layers: Each of inputs were connected linearly with three dense layer. Each dense layer processes the inputs, further processing the data and extracting higher-level features.

3. Reshape Layers: The reshape layers were applied for after each third dense layer. This layer reshapes the output of the third dense layer into a shape of (sequence_length, vocabolary size of notes) and (sequence_length, vocabolary size of durations) for notes and durations input respectively. 

4. Softmax Activation Functions: The softmax activation functions are applied to the output of the both reshape layer. It converts the output into a probability distribution over the vocabolary size for note and duration.

5. Flatten Layers: The flatten layer reshapes the output of both softmax layers into a one dimensional vector.

Generator Component Setup: The encoder and the decoder are combined into the one model GRU-VAE (VAE with GRU architecure). The overall generators takes both the note and duration inputs and outputs reconstructed notes and durations, using decorder. This architecture allows the generator component to learn a joint latent representation for notes and durations, enabling the generation of sequences with coherent note and duration components. 

Generator Loss: The loss of generator is similar with the VAE loss which consist of addition two component which are reconstruction loss and Kullback-Liebler divergence term (KL term). The reconstruction loss is binary cross entropy while KL term is defined as follow:

$$ Loss_{KL} = - \frac{1}{2}*(1 + \log{\sigma} - \mu^2 - \sigma^2 ) $$

where $\mu$ and $\sigma$ is mean and standard deviation of latent distribution. The VAE loss is defined as 

$$ Loss_{Vae} = Loss_{Reconstruction} + Loss_{KL}$$

Since there are two sets in total of latent varaibles for notes and durations features, the generator loss is defined as follows:

$$ Loss_{Generator} =  Loss_{Vae Notes} + Loss_{Vae Durations}$$

