# Background of the Study

Music is a universal language that transcends cultural boundaries and speaks to the depths of human emotion and experience. Music has the power to stimulate memories, stir passions and bring people together in a profound way, from the rhythmic beats of tribal drums to the intricate melody of symphony orchestras. Classical music is one of the most enduring and beloved forms of music. Rooted in centuries of tradition and innovation, classical music encompasses a vast repertoire of compositions that have stood the test of time.  Classical music is one of the most enduring and beloved forms of music. Rooted in centuries of tradition and innovation, classical music encompasses a vast repertoire of compositions that have stood the test of time. Classical music, with its rich history and diverse repertoire, has long been a source of inspiration and admiration for musicians and audiences alike. For its complexity, beauty, and emotional depth, the compositions of great classical composers such as Bach, Beethoven, Mozart, and others are revered. For musicians and audiences alike, classical music has long been a source of inspiration and admiration, with its rich history and diverse repertoire. For its complexity, beauty, and emotional depth, the compositions of great classical composers such as Bach, Beethoven, Mozart, and others are revered. 

Eventhough the classical music is not really popular today, classical music does not remain static. It's continuing to evolve and be an inspiration for new generations of musicians and composers. The use of technology, particularly artificial intelligence (AI), is one way in which classical music has evolved. AI can change the way music is composed, performed and listened to, opening up new possibilities for creativity and expression. The growing interest in using AI in recent years has promoted the usage of AI in so many field including music generation. Generative AI, in particular, has shown promise in this regard. By analyzing vast amounts of musical data, generative AI algorithms can learn the patterns and structures that define a particular style or genre of music.  This allows them to compose new compositions which are stylistically similar to those of the composers they've been trained in. 

There are a number of possible benefits to the revival of classic music using generative AI. New instruments and techniques for the creation of music may be made available to composers, enabling them to explore new creative possibilities. By introducing classical music to new audiences in a fresh and engaging way, it can also help preserve and support classical music. The use of generative artificial intelligence for music composition also presents challenges and considerations which need to be addressed. Ensuring that the compositions created with artificial intelligence are original and creative rather than merely imitating existing works is one of the main challenges. In addition, questions are being raised about the role of a composer in AI's creative process and how to attribute and recognize music generated by artificial intelligence.

# Research Questions

The project will based on following research questions. These research questions are designed to provide a comprehensive exploration of the use of generative AI for recomposing classical music, covering technical, and artistic aspects of this emerging field.

1. How to create generaitve AI algorithms to produce music similar to classical music ?
2. What kind of generative AI algorithms can produces the most pleasant music and approaching the characteristics of classical music ?
3. How do AI-generated classical music compositions compare to established works in the classical repertoire in terms of technical execution and artistic expression, as evaluated by musicians and audiences?

# Research Objectives

The objective of this project is to investigate the use of generative AI for recomposing classical music. Specifically, the study aims to achieve the following objectives:

1. To developed generative AI algorithms to produces music similar to classical music.
2. To evaluate which generative AI algorithms that can produce the most pleasant music and approaching the characteristics of classical music.
3. To compared the AI-generated classical music compositions with the established work in the classical repertoire in terms of technical execution and artistic expression which evaluated by musicians and audiences.

# Methodology

## Dataset
The dataset used in this project was obtained from [kaggle](https://www.kaggle.com/datasets/soumikrakshit/classical-music-midi). Where the dataset consists of classical piano midi files containing compositions of 19 famous composers scraped from [piano-midi website](http://www.piano-midi.de). From all famous composer, this porject utilizing classical music from only one composer which known as Chopin. The reason why only one composer was used due to the simplicity, memory consumptions and model training time.

## EDA

![]()

The process of Exploratory Data Analysis (EDA) is shown in figure above where it begins with gathering the classical music midi data. The data the was undergone sampling process where only chopin music will be choosen. There are two type of EDA, the first type of EDA is directly toward the exploration of the music itself without data preprocessing where the music sheet and audio was produced to get better understanding on the music on how music sounds like and how the musics notes and durations looks like.

![]()

![]()

The process continue with the data preprocessing where each of the Chopin composed music was undergone clef spliiting where the treble and bass clef was separated. Each of the clef was undergone the music element extraction where the notes, chords and durations were extracted for the dataframe construction which consisting of two features where the first features consisting the notes and chords while the second features consisting durations. The chords and notes were extracted based on their pitch freuency while the durations were extracted based on the durations type. Two dataframe was constructed for each treble and bass clef. Each of the dataframe was undergone the EDA for second type which is more toward data analytics. The EDA was done for univariate, mutlivariate and outliers. Noted that the first column was named music element which consist of notes and chords while second column was named durations.

# Univariate Analysis
## Bass Clef
### Pitch Frequency Distribution
![]()

The distribution of pitch frequency is positively skewed with the modes around 160 $s^-{1}$. Majority of the chords and notes used is in the frequencies of 50 $s^{-1}$ to 300 $s^{-1}$. While chords and notes with frequencies around 500 $s^{-1}$ and above can be seen as minority chords and notes used in the Chopin composed music. 

### Duration Distribution
![]()

Majority of the durations used was 8th notes with around 17500 counts followed by 16th note with around 14000 counts. The quarter notes is in the third position with around 7500 count. Other than the mentioned durations which are whole note, half note, complex note, breve note and 32nd note are the minority durations in the Chopin compoased music.

## Treble Clef
### Pitch Frequency Distribution
![]()

The distribution of pitch frequency is positively skewed with the modes around 350 $s^-{1}$. Majority of the chords and notes used is in the frequencies of 200 $s^{-1}$ to 1300 $s^{-1}$. While chords and notes with frequencies around 1500 $s^{-1}$ and above can be seen as minority chords and notes used in the Chopin composed music.

### Duration Distribution
![]()

Majority of the durations used was 16th notes followed by 8th note. The quarter notes is in the third position with around 6500 counts. Other than the mentioned durations which are whole note, half note, complex note, breve note and 32nd note are the minority durations in the Chopin compoased music.

## Both Clef
### Pitch Frequency Distribution
![]()

The distribution of pitch frequency is positively skewed with the modes around 250 $s^{-1}$. Majority of the chords and notes used is in the frequencies of 50 $s^{-1}$ to 750 $s^{-1}$. While chords and notes with frequencies around 1000 $s^{-1}$ and above can be seen as minority chords and notes in the Chopin composed music.

### Duration Distribution
![]()

Majority of the durations used was 8th notes with 35000 count followed by 16th note with around 32500 counts. The quarter notes is in the third position with 15000 counts. Other than the mentioned durations which are whole note, half note, complex note, breve note and 32nd note are the minority durations in the Chopin compoased music.

# Multivariate Analysis
## Bass Clef
![]()

The 8th note, 16th note and quarter note have almost similar shape of distribution which is almost symmetric. Majority of the notes are in the range of 30 $s^{-1}$ to 400 $s^{-1}$. The range of 8th note distribution is around 20 $s^{-1}$ to 1300 $s^{-1}$ while te range of 16th note distribution is around 20 $s^{-1}$ to 1400 $s^{-1}$. Half note has similar distribution of majority of the notes but postively skewed with the mode around 100 $s^{-1}$. The whole note has a mode around 80 $s^{-1}$ with majority of the notes is in the range of 20 $s^{-1}$ to 200 $s^{-1}$. The complex note has the range of distribution of 0 $s^{-1}$ to 1400 $s^{-1}$ with majority of the notes is in the range of 0 $s^{-1}$ to 400 $s^{-1}$. Both breve note and 32nd note has almost the same shape of distribution with almost same modes around 100 $s^{-1}$. Also, both have the same range of distribtion which from 0 $s^{-1}$ to around 360 $s^{-1}$.

## Treble Clef
![]()

The half note, quarter note, 8th note and 16th note have almost similar shape of distribution which is slight positively skewed with almost similar range where most notes are in the range of 200 $s^{-1}$ to 1000 $s^{-1}$ with the distribution range of 200 $s^{-1}$ to 2900 $s^{-1}$. The whole note has a mode around 450 $s^{-1}$ with distribution range of 150 $s^{-1}$ to 1000 $s^{-1}$. The complex note has the longest range of distribution of 0 $s^{-1}$ to 3000 $s^{-1}$. The breve note distribution is the only negatively skewed in the treble clef dsitribution, the breve note distribution has mode around 500 $s^{-1}$ with the range of 200 $s^{-1}$ to 800 $s^{-1}$. The 32nd note distribution has mode around 500 $s^{-1}$ with the range of 0 $s^{-1}$ to 1750 $s^{-1}$ with the majority of the notes lies in the range of 200 $s^{-1}$ to 800 $s^{-1}$. 

## Both Clef
![]()

The 8th note and 16th note have almost similar shape of distribution which is positively skewed with similar range where most notes are in the range of 30 $s^{-1}$ to 2800 $s^{-1}$ and mode of 200 $s^{-1}$ with majority of the notes lies in the range of 100 $s^{-1}$ to 1000 $s^{-1}$. Half note has similar distribution range but the distribution is symmetric. The quarter note distribution has notable mode around 250 with the range of 0 $s^{-1}$ to 1200 $s^{-1}$ with majority of the notes lies in the range of 100 $s^{-1}$ to 500 $s^{-1}$. The whole note distribution is positively skewed with the mode around 150 $s^{-1}$ with distribution range of 0 $s^{-1}$ to 1100 $s^{-1}$ with the majority of notes lies in the range of 50 $s^{-1}$ to 500 $s^{-1}$. The complex note has the longest range of distribution of 0 $s^{-1}$ to 3000 $s^{-1}$. Both breve note and 32nd note, both are positively skewed but different shape and range. The range of distribtion of 32nd note is a bit longer compared to the range of distribtion of breve note while both have almost the same mode around 200 $s^{-1}$.

# Outliers Analysis
## Bass Clef
![]()

From the plot, the median of the bass clef distribution is at 200 $s^{-1}$ with the interquartile range of 150 $s^{-1}$ to 250 $s^{-1}$. The bass clef distribution has maximum of around 500 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 500 $s^{-1}$ are identfied as outliers.

## Treble Clef
![]()

From the plot, the median of the treble clef distribution is at 500 $s^{-1}$ with the interquartile range of 400 $s^{-1}$ to 750 $s^{-1}$. The bass clef distribution has maximum of around 1300 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 1300 $s^{-1}$ are identfied as outliers.

## Both Clef
![]()

From the plot, the median of the both clef distribution is at 300 $s^{-1}$ with the interquartile range of around 150 $s^{-1}$ to 500 $s^{-1}$. The both clef distribution has maximum of around 1000 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 1000 $s^{-1}$ are identfied as outliers.

The outliers analsis shows there are many outliers in the data. However, the technique used to deal with outliers is simply keep the outliers in the data. Dealing with outliers by removing will affect the sequences of the notes which make the music have high degree of disorderness in the notes sequences which may cause worst output of AI-generate music.


## Modelling

There are so many generative models available which can be used in this project. However, among all the generaitve models, only 4 models will be used which are autoregressive model or known as Recurrent Neural Network (RNN) by using LSTM architecture, Variational AutoEncoder (VAE), Generative Adversarial Network (GAN) and large language model of Generative Pretrained Transformer (GPT). Another model used in this project is a fusion model which a combination of three different generative model architecture where RNN of Gate Recurrent Unit (GRU) architecure was combine with VAE architecture together with GAN architecture. Each of the model require different representation of the data, therefore, different preprocesing was applied to the data for each model. 

### Autoregressive Model - Recurrent Neural Network (LSTM)
![]()

#### Preprocessing - LSTM
As shown in the framework figure above, the LSTM modelling start with sampling process where only five midi file was used and only come from Chopin composed music. The midi files was processed further by extracting their parts. Each part was looked for their clef property where parts with treble clef property belongs to treble clef while parts with bass clef property belongs to bass clef. The music element such as notes, chords and durations will be extracted for each clef. The notes and chords are grouped together under the same feature while durations itself become another feature. Both features was combine forming a dataframe. There are total 2 dataframe which represent treble and bass clef. Both dataframe were processed further for data transformation, where list of chords were changed to chords label and numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represent as categorical representative instead of numerical representative. After transormation, both dataframe were encoded by using label encoding technique. Finally, the sequence data of each clef was produced by extracting 100 sequence data from the dataframe. The final product of the preprocessing stage is two data consist of 100 sequence of notes and durations

#### Modelling - LSTM
This project used typically one model for each clef. Therefore, there are total two identical model architecture were used for modelling stage. The architecture of LSTM model is based on 3 layers of LSTM architecture with a dropout layer between two LSTM layer. After the final layer of LSTM, the architecture utilized a dense layer.  Since there are two features in the input data, the output data will have two features too (notes and durations). Therefore, the final layers (output layers) is consist of two dense layer with softmax activation function which each represent notes (can be chords) and durations. The loss function used in the LSTM model is sparse categorical crossentropy. The final product of the models will be the generated notes and durations in the form of probability across all notes used and durations used in the dataset.

#### Music Generation - LSTM
The outputs (notes and durations) were go through top k sampling process where one from top 10 notes and one from top 5 durations will be randomly select. The dataframe was constructed based on the select notes and durations. Since there two clef, there are two total dataframe which are treble clef dataframe and bass clef dataframe. The dataframes will undergo the inverse label encoding and inverse transformation. The processed generated dataframes will be combine together into music score and stream forming a music.

### Variational AutoEncoder (VAE)

![]()

#### Preprocessing - VAE
As shown in the framework figure above, the VAE processing has some degree of similarity with LSTM. Sampling, clef splitting, music element extraction, dataframe construction, transformation and label encoding process was similar to LSTM. The difference start after the label encoding process, where the dataframe will be processed by extracing the 100 sequence data of each notes and durations and forming arrays. There four arrays produced in total which are treble notes, treble durations, bass notes and bass durations. Each of the arrays will go through one hot encoding. Finally, each notes will be flattened to vocab size times sequence length of the data. Noted that since there are four arrays, there are 4 vocab size which represent unique value of treble notes, unique value of treble durations, unique value of bass notes and unique value of bass durations. The final product of the preprocessing stage is the 4 processed array which consist of one hot sequence data which are treble notes, treble durations, bass notes and bass durations.

#### Modelling - VAE
Similar with LSTM this project used identical architectue in the modelling stage. The VAE architecture used is a variant of VAE itself, which is a novel architcture (to the best of my knowledge) for VAE which named multi-VAE. Similar with the original VAE, it consist of two main components which are encoder and decoder. The encoder in multi-VAE receive two input which from notes and durations. Each input layer is connected to three dense layer, the final dense layer is have two different connection. The first connection is the final dense layer in the encoder will be connected to another two dense layer forming latent variables of z means and z log variance. Later the z means and z log variance will be connected to sampling layer to sampled the latent representation of z. On the other hand, the two final dense layer for each input (notes and durations) will be combined together using concecatenate layers and connected to the dense layers. This dense layer will be combined with the sampled latent representation of z for notes and durations using concatenate layer forming the final product of latent representation. Both final latent representation of z for notes and durations will be used as input to the dercorder. The input layers of decorder is connected to the two dense layers with activation function of sigmoid in the final dense layer in the decorder. The loss of vae consist of addition two component which are reconstruction loss and Kullback-Liebler divergence term (KL term). The reconstruction loss is binary cross entropy while KL term is defined as follow:

$$ Loss_{KL} = - \frac{1}{2}*(1 + \log{\sigma} - \mu^2 - \sigma^2 ) $$

where $\mu$ and $\sigma$ is mean and standard deviation of latent distribution. The total loss is defined as 

$$ Loss_{Total} = Loss_{Reconstruction} + Loss{KL}$$

#### Music Generation - VAE
The outputs (notes and durations) were go through top k sampling process where one from top 10 notes and one from top 5 durations will be randomly select. The dataframe was constructed based on the select notes and durations. Since there two clef, there are two total dataframe which are treble clef dataframe and bass clef dataframe. The dataframes will undergo the inverse label encoding and inverse transformation. The processed generated dataframes will be combine together into music score and stream forming a music.

### Generative Adversarial Network (GAN)
![]()
#### Preprocessing - GAN
As shown in the framework figure above, the GAN modelling start with sampling process where only three midi file was used and only come from Chopin composed music. The reduction of midi file is due to the memory consumption during preprocessing. The midi files was processed further by extracting their parts. Each part was looked for their clef property where parts with treble clef property belongs to treble clef while parts with bass clef property belongs to bass clef. The music element such as notes, chords and durations will be extracted for each clef. The notes and chords are grouped together under the same feature while durations itself become another feature. Both features was combine forming a dataframe. There are total 2 dataframe which represent treble and bass clef. Both dataframe were processed further for data transformation, where list of chords were changed to chords label and numerical representation of duration data was transformed to categorical data. Noted that, in music, the duration is mostly represent as categorical representative instead of numerical representative. After transformation, both dataframe were encoded by using label encoding technique. The two arrays were constructed which consist of 100 sequence data from the processed dataframe. Finally,  both the arrays will undergo the one hot encoding process to produce three dimentional array of treble array and bass array. 

#### Modelling - LSTM
This project used typically one model for each clef. Therefore, there are total two identical model architecture were used for modelling stage. The architecture of GAN model consist of two component which are generator and discriminator. The generator component begin with input layer as the first layer. The input layer is connected to flatten layer to flatteing the three dimensional input data into two dimensional input data. The flatten layer is then linearly connected with three dense layer. The final dense layer from this sequence is connected to two dense layer. This connection is represent the two feature in the input which are notes and durations. Each of the dense layer is connected to the reshape layer with the softmax activation function. The reshape layer is necessary because to change the shape follow the input data while the softmax activation function is required to distribute the probability distribution across the vocab size. Finally, the concatenate layer was used at the end of the generator component to combine the both probability distribution for notes and durations. This is necessary since the input data also consist of the one hot encoding of both notes and durations. The input and the output data are needed to be similar to discriminator to compared both data. 

The discriminator component also begin with input layer which is connected to two alternating dense and dropout. Next, the sequence is continue with the dropout layer is connected linearly with the two dense layer. The final layer which is dense layer used sigmoid activation function to do the binary classification which discriminate the generated data from generator is fake or real. The concept of GAN start with the generator to generate new data from stochastic noise, while discriminator distinguish the generated data whether it is from real (from the trainingset) or not (from the generator). In the model, the both networks are trained separately but simultaneously where the generator network has no access to real example and only learn from the discriminator judgement. While discriminator use the real example to make the judgement. Both generator and discriminator compete with each other which is based on a game theory scenario called "the minmax game".

#### Music Generation - GAN
After the GAN training, the notes and durations from the generated is extracted. The outputs (notes and durations) will go through top k sampling process where one from top ten notes and one from top five durations will be randomly select. The dataframe was constructed based on the selected notes and durations. Since there two clef, there are two total dataframe which are treble clef dataframe and bass clef dataframe. The dataframes will undergo the inverse label encoding and inverse transformation. The processed generated dataframes will be combine together into music score and stream forming a music.

### Fusion Model - RNN (GRU) + VAE + GAN
### Large Language Model - Generative Pretrained Transformer (GPT)
# Evaluation
# Conclusion

   


