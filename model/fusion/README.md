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


