# Fusion Model - RNN-VAE-GAN

<p align="middle">
<img src=https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/fusion/framework/FUS_framework.png/>
</p>
<p align="middle">
    <em>Fusion Model Framework.</em>
</p>

## Preprocessing
As shown in the framework figure above, the processing of data for Fusion Model modeling starts with the following processes:

1. Sampling: sampling process where only two midi files were used and only came from Chopin-composed music.

2. Key Transposing: All the midi files underwent the key transposing process where all the keys of the songs will be transposed to middle C.

3. Clef Splitting: The midi files were processed further by extracting their parts. Each part was looked for its clef property where parts with treble clef property belong to treble clef while parts with bass clef property belong to bass clef.

4. Music Element ExtractionThe music elements such as notes, chords, and durations were extracted for each clef. The notes and chords are grouped under the same feature while durations themselves become another feature.

5. Dataframes Construction: Both features were used to form a data frame. There are a total of two data frames which represent treble and bass clef.

6. Data Transformation: Both data frames were processed further for data transformation, where lists of chords were changed to chords labels and the numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represented as categorical representative instead of numerical representative.

7. Label Encoding: After transformation, both data frames were encoded by using the label encoding technique where the categorical representation of data was changed to an integer representation of data.

8. Array Constructions: After the label encoding process, the arrays were constructed from the data frames by extracting the 100 sequence data of notes and durations. There are four arrays produced in total which are treble notes, treble durations, bass notes, and bass durations.

9. One Hot Encoding: Each of the arrays went through one hot encoding process where the categorical representation of data was converted to a binary matrix format.

10. Flattening: Finally, each arrays were flattened to vocabulary size of each array times the sequence length of the data. Note that since there are four arrays, there are 4 vocabulary sizes that represent the unique value of treble notes, unique value of treble durations, unique value of bass notes, and unique value of bass durations.

The final products of the preprocessing stage were the 4 processed arrays which consist of one hot sequence data which are treble notes, treble durations, bass notes, and bass durations.

## Modelling 

### Generator Component
The fusion model used a combination of RNN, VAE, and GAN. Each of the architecture is implemented together forming a new model. The main architecture of RNN-VAE-GAN is a GAN model where it consists of two main components which are generator and discriminator. The generator component used the VAE architecture in its architecture and the RNN (GRU) architecture was used in the encoder part of VAE. The architecture of the generator component in fusion models is as follows:

Encoder Note and Duration:

1. Input Layers: The encoder starts with input layers where this layer receives the input data, which is the sequence of processed music elements. It does not perform any computations but passes the input to the next layer. There are two input layers used for each input which are notes and durations.

2. Reshape Layers: The reshape layer was added after the input layer, this layer reshapes the shape of inputs to (sequence length, vocabulary size of notes) and (sequence length, vocabulary size of durations) for notes and durations input respectively.

3. Concatenate Layer: The concatenate layer was added after reshape layer to concatenate the inputs for processing together.

4. GRU Layers: Three GRU layers were added after concatenate layer, each GRU layer processes the concatenated reshaped input sequence by learning to capture temporal dependencies in the input data and outputs a sequence of hidden states.

5. Dense Layer: The dense layer processes the final hidden state from the last GRU layer and produces the output.

6. LeakyReLU activation: After the dense layer, LeakyReLU activation is applied where it helps by allowing a small gradient for negative inputs, Leaky ReLU ensures that even neurons that have a negative input can still contribute to the learning process, helping the network to learn more effectively. The output from this activation was split into two separate paths.

7. Dense Layer + LeakyReLU (First Path): The first branch was connected to the dense layer with the addition of LeakyReLU activation functions. The output of this layer is connected to another dense layer together with LeakyReLU activations functions.

8.  Dense Layer + LeakyReLU (Second Path):  The first branch was connected to the dense layer with the addition of LeakyReLU activation functions. This is the path of duration output. The output of this layer is connected to another dense layer together with LeakyReLU activations functions.

9.  Dense Layer (First Path): The dense layer with Leaky ReLU of the previous layer was connected to another dense layer (this layer). The output of this dense layer is split into two paths where one path calculates the mean of the latent variable, z for note. Another path calculates the log variance of latent variable z for note. 

10. Dense Layer (Second Path): The dense layer with Leaky ReLU of the previous layer was connected to another dense layer (this layer). The output of this dense layer is split into two paths which are one path calculates the mean of the latent variable, z for duration. Another path calculates the log variance of the latent variable, z for the duration.

11. Concatenate Layers: The outputs of the final dense layers from both paths are concatenated by using a concatenate layer. The concatenated output is passed through another dense layer forming a combined latent distribution.

12. Sampling Layers: There are a total two of sampling layers used to sample from the calculated mean and log variance of the latent distribution, z for note and duration. The sampled latent variable for note and duration are concatenated with the final layer of the combined latent variable to create a finalized note and duration latent distribution.

Decoder Note and Duration:

1. Input Layers: The decoder starts with input layers where this layer receives the concatenated latent variable (finalized note or duration latent distribution). There are two input layers were used for each input which are note and duration latent distribution.

2. Dense Layers: Each of the inputs were connected linearly with three dense layers. Each dense layer processes the inputs, further processing the data and extracting higher-level features.

3. Reshape Layers: The reshape layers were applied after each third dense layer. This layer reshapes the output of the third dense layer into a shape of (sequence length, vocabulary size of notes) and (sequence length, vocabulary size of durations) for notes and durations input respectively. 

4. Softmax Activation Functions: The softmax activation functions are applied to the output of both reshape layers. It converts the output into a probability distribution over the vocabulary size for note and duration.

5. Flatten Layers: The flatten layer reshapes the output of both softmax layers into a one-dimensional vector.

Generator Component Setup: The encoder and the decoder are combined into one model GRU-VAE (VAE with GRU architecture). The overall generator takes both the note and duration inputs and outputs reconstructed notes and durations, using the decoder. This architecture allows the generator component to learn a joint latent representation for notes and durations, enabling the generation of sequences with coherent note and duration components. 

Loss Function: The loss of the generator component is similar to the VAE loss which consists of the addition of two components which are reconstruction loss and Kullback-Liebler divergence term (KL term). The reconstruction loss is binary cross entropy while the KL term is defined as follows:

$$ Loss_{KL} = - \frac{1}{2}*(1 + \log{\sigma} - \mu^2 - \sigma^2 ) $$

where $\mu$ and $\sigma$ is mean and standard deviation of latent distribution. The VAE loss is defined as 

$$ Loss_{Vae} = Loss_{Reconstruction} + Loss_{KL}$$

Since there are two sets in total of latent varaibles for notes and durations features, the generator loss is defined as follows:

$$ Loss_{Generator} =  Loss_{Vae Notes} + Loss_{Vae Durations}$$

### Discriminators Component

In this model, the variant of GAN was used namely MDGAN which stands for Multiple Discriminator Generative Adversarial Network. As its name, there is more than one discriminator in the MDGAN model. In this fusion model, there are two discriminators were utilized. One discriminator will discriminate the note feature while the other discriminator will discriminate the duration feature. Each of 

1. Input Layer (Dense): The first layer is a dense layer, It takes the input data and applies a linear transformation to map it to a higher-dimensional space.

2. Batch Normalization: Batch normalization normalizes the activations of the previous layer, which can help with training by reducing internal covariate shifts and improving gradient flow.

3. Leaky ReLU Activation: The Leaky ReLU activation function introduces a small slope for negative inputs, helping to avoid "dying ReLU" units and allowing the network to learn even when the input is negative.

4. Dropout Layer: Dropout which helps prevent overfitting by reducing co-adaptation of neurons.

5. Dense layer: Another dense layer follows the first dropout layer. It further processes the data and extracts more complex features.

6. Batch Normalization: Another batch normalization layer normalizes the activations of the previous layer, similar to the first batch normalization layer.

7. Leaky ReLU Activation: Another Leaky ReLU activation function is applied after the second batch normalization layer to introduce non-linearity.

8. Dropout Layer: Another dropout layer was added after the second Leaky ReLU activation function to further prevent overfitting.

9. Output Layer (Dense): The output layer is a dense layer with a single unit and a sigmoid activation function. It produces a binary output indicating the probability that the input data is real (1) or fake (0).

10. Loss Function: The loss function used in the discriminator component is binary cross-entropy.

In the fusion model, the generator utilizing the GRU component will be used for sequence modeling. GRUs are a type of RNN that can capture long-range dependencies in sequences, making them suitable for tasks where the context of previous elements is important. While the VAE component would handle the latent space modeling. It would encode input data into a latent space representation, which can then be decoded back into the original data. VAEs are useful for learning meaningful representations of data and generating new samples that resemble the training data. With this architecture, the generator aims to produce realistic sequences of notes and durations, while the two discriminators are responsible for evaluating the realism of the generated notes and durations; they are trained to classify samples as either real (from the dataset) or fake (generated by the generator). During training, the generator aims to produce samples that are indistinguishable from real data to fool both discriminators, while both discriminators aim to become better at distinguishing between real and fake samples. This adversarial process drives the improvement of both the generator and the discriminators until the generator can generate high-quality, realistic samples that are difficult for both discriminators to differentiate from real data.

## Music Generation

### Processing
The outputs of the model training are arrays of treble notes, treble durations, bass notes, and bass durations. Each of the outputs went through music generation processes to generate music. The process is as follows:

1. Top K Sampling: The outputs (notes and durations) underwent the top k sampling process where one from the top ten notes and one from the top five durations were randomly selected.

2. Dataframe Construction: The dataframe was constructed based on the selected notes and durations. Since there are two clef, there are two total data frames which are the treble clef data frame and bass clef data frame.

3. Inverse Label Encoding: The data frames underwent inverse label encoding where the integer representation of data was converted to the categorical representation of data.

4. Inverse Data Transformation: The data frames went through the inverse data transformation where the categorical representation of data is transformed to the original data representation.

5. Music Stream Construction: The processed generated data frames were submitted to the music stream, where the generated treble data was submitted to the treble clef stream while the generated bass data was submitted to the bass clef stream.

6. Stream Balancing: Both streams went through the stream balancing process where both stream's lengths were adjusted to make sure both lengths are similar (or almost similar).

7. Music Score Construction: The balanced streams were submitted to the music score. The music score was used to generate the music in the form of music audio and music sheet.

### Music Generated
The generated music by RNN-VAE-GAN model can be found in the `music_generated` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/fusion/music_generated). The music sheet can be seen at the `music_generated\sheet` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/fusion/music_generated/sheet) and the music audio can be found at the `music_generated\audio` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/main/model/fusion/music_generated/audio).

## Source code
The source code of the music generation using RNN-VAE-GAN model can be found in the `model\fusion\source_code` [directory](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/tree/8e442b232784161b4b851ba214667b9fc2bc72de/model/fusion/source_code). There two files there, the first file named as "[RNN_VAE_GAN_Music_Generation_with_Generative_AI](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/fusion/source_code/RNN_VAE_GAN_Music_Generation_with_Generative_AI.ipynb)" is the code for modelling from the begininng process of data gathering until model saving. While the second file which named as "[RNN_VAE_GAN_Music_Production](https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/model/fusion/source_code/RNN_VAE_GAN_Music_Production.ipynb)", is the code for music production where different values of keys and tempos were changed to develop a variability of music generated.






