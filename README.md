# Background of the Study

Music is a universal language that transcends cultural boundaries and speaks to the depths of human emotion and experience. Classical music is one of the most enduring and beloved forms of music. Rooted in centuries of tradition and innovation, classical music encompasses a vast repertoire of compositions that have stood the test of time.  Classical music, with its rich history and diverse repertoire, has long been a source of inspiration and admiration for musicians and audiences alike. For its complexity, beauty, and emotional depth, the compositions of great classical composers such as Bach, Beethoven, Mozart, and others are revered.

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
The dataset used in this project was obtained from [kaggle](https://www.kaggle.com/datasets/soumikrakshit/classical-music-midi). Where the dataset consists of classical piano midi files containing compositions of 19 famous composers scraped from [piano-midi website](http://www.piano-midi.de). From all famous composer, this porject utilizing classical music from only one composer which known as Chopin. The reason why only one composer was used due to the resource limitation, cost and time efficiency.

## EDA

![]()

The process of Exploratory Data Analysis (EDA) is shown in figure above where it begins with gathering the classical music midi data. The data the was undergone sampling process where only chopin music will be choosen. There are two type of EDA, the first type of EDA is directly toward the exploration of the music itself without data preprocessing where the music sheet and audio was produced to get better understanding on the music on how music sounds like and how the musics notes and durations looks like.

![]()

![]()

The process continue with the data preprocessing where each of the Chopin composed music was undergone clef spliiting where the treble and bass clef was separated. Each of the clef was undergone the music element extraction where the notes, chords and durations were extracted for the dataframe construction. There are two total dataframe was created which are treble dataframe and bass dataframe, each represent treble clef and bass clef respectively. Each dataframe consist of two features where the first features consisting the notes and chords while the second features consisting durations. The chords and notes were extracted based on their pitch freuency while the durations were extracted based on the durations type. Each of the dataframe were underwent the second type of EDA which is more toward data analytics. The EDA includes the univariate analysis, mutlivariate analysis and outliers analysis. 

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

# Multivariate Analysis
## Bass Clef
![]()

The 8th note, 16th note and quarter note have almost similar shape of distribution which is almost symmetric. Majority of the notes are in the range of 30 $s^{-1}$ to 400 $s^{-1}$. The range of 8th note distribution is around 20 $s^{-1}$ to 1300 $s^{-1}$ while te range of 16th note distribution is around 20 $s^{-1}$ to 1400 $s^{-1}$. Half note has similar distribution of majority of the notes but postively skewed with the mode around 100 $s^{-1}$. The whole note has a mode around 80 $s^{-1}$ with majority of the notes is in the range of 20 $s^{-1}$ to 200 $s^{-1}$. The complex note has the range of distribution of 0 $s^{-1}$ to 1400 $s^{-1}$ with majority of the notes is in the range of 0 $s^{-1}$ to 400 $s^{-1}$. Both breve note and 32nd note has almost the same shape of distribution with almost same modes around 100 $s^{-1}$. Also, both have the same range of distribtion which from 0 $s^{-1}$ to around 360 $s^{-1}$.

## Treble Clef
![]()

The half note, quarter note, 8th note and 16th note have almost similar shape of distribution which is slight positively skewed with almost similar range where most notes are in the range of 200 $s^{-1}$ to 1000 $s^{-1}$ with the distribution range of 200 $s^{-1}$ to 2900 $s^{-1}$. The whole note has a mode around 450 $s^{-1}$ with distribution range of 150 $s^{-1}$ to 1000 $s^{-1}$. The complex note has the longest range of distribution of 0 $s^{-1}$ to 3000 $s^{-1}$. The breve note distribution is the only negatively skewed in the treble clef dsitribution, the breve note distribution has mode around 500 $s^{-1}$ with the range of 200 $s^{-1}$ to 800 $s^{-1}$. The 32nd note distribution has mode around 500 $s^{-1}$ with the range of 0 $s^{-1}$ to 1750 $s^{-1}$ with the majority of the notes lies in the range of 200 $s^{-1}$ to 800 $s^{-1}$. 

# Outliers Analysis
## Bass Clef
![]()

From the plot, the median of the bass clef distribution is at 200 $s^{-1}$ with the interquartile range of 150 $s^{-1}$ to 250 $s^{-1}$. The bass clef distribution has maximum of around 500 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 500 $s^{-1}$ are identfied as outliers.

## Treble Clef
![]()

From the plot, the median of the treble clef distribution is at 500 $s^{-1}$ with the interquartile range of 400 $s^{-1}$ to 750 $s^{-1}$. The bass clef distribution has maximum of around 1300 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 1300 $s^{-1}$ are identfied as outliers.

The outliers analsis shows there are many outliers in the data. However, the technique used to deal with outliers is simply keep the outliers in the data. Dealing with outliers by removing will affect the sequences of the notes which make the music have high degree of disorderness in the notes sequences which may cause worst output of AI-generate music.


## Modelling

There are so many generative models available which can be used in this project. However, among all the generaitve models, only 4 models will be used which are autoregressive model or known as Recurrent Neural Network (RNN) by using Long Short-Term Memory (LSTM) architecture, Variational AutoEncoder (VAE), Generative Adversarial Network (GAN) and large language model of Generative Pretrained Transformer (GPT). Another model used in this project is a fusion model which a combination of three different generative model architecture. The fusion model utilizing the RNN of Gate Recurrent Unit (GRU) architecure combine with VAE architecture together with GAN architecture. Each of the model require different representation of the data, therefore, different preprocesing was applied to the data for each model. 

### Autoregressive Model - LSTM

![]()

LSTM is a type of neural network designed to handle sequence data by maintaining long-term dependencies. It does this by using a memory cell that can store information, along with gates that control the flow of information into and out of the cell. This allows LSTM networks to learn patterns in sequences and make predictions based on them, making them useful for main tasks in this project which is classical music recomposition. The detail explanation of LSTM framework as well as source code can be found in `` [directory]().

### AutoEncoder Model - VAE

![]()

VAE is a type of neural network used for generative modeling. It learns to encode input data into a lower-dimensional latent space and then decode it back to the original input. VAEs are trained to maximize the likelihood of the observed data while also maximizing the mutual information between the latent variables and the data. This allows them to generate new data samples that resemble the training data, making them useful for main tasks in this project which is classical music recomposition.  The detail explanation of VAE framework as well as source code can be found in `` [directory]().

### Generative Adversarial Network - GAN

![]()


GAN is a type of neural network used for generative modeling. It consists of two networks: a generator and a discriminator. The generator creates new data samples, while the discriminator tries to distinguish between real and generated samples. They are trained together in a adversarial manner, where the generator tries to fool the discriminator and the discriminator tries to become better at distinguishing real from fake. This competition leads to the generator learning to create increasingly realistic samples, making GANs useful for main tasks in this project which is classical music recomposition. The detail explanation of GAN framework as well as source code can be found in `` [directory]().

### Fusion Model - RNN-VAE-GAN

![]()

A fusion generative model that combines GRU, VAE and GAN elements would be a complex architecture aimed at capturing the strengths of each component. The GRU component will be used for sequence modeling. GRUs are a type of RNN that can capture long-range dependencies in sequences, making them suitable for tasks where the context of previous elements is important. While the VAE component would handle the latent space modeling. It would encode input data into a latent space representation, which can then be decoded back into the original data. VAEs are useful for learning meaningful representations of data and generating new samples that resemble the training data. Finally, the GAN component would add a competitive training mechanism to improve the realism of the generated samples. The generator part of the GAN would likely be integrated with the VAE decoder, generating samples from the learned latent space. The discriminator would then provide feedback to both the generator and the VAE on the realism of the generated samples.

In this fusion model, the GRU would help capture the sequential dependencies in the data, the VAE would learn a meaningful latent space representation, and the GAN would improve the quality of the generated samples. By combining these components, the model could potentially achieve better performance than using any one component alone. The detail explanation of fusion model framework as well as source code can be found in `` [directory]().

### Large Language Model - GPT

![]()

GPT is a type of deep learning model based on the transformer architecture. It is designed for natural language processing tasks such as text generation, translation, and question answering. However, since text generation is a sequence data and the music also is a sequence data. The GPT should be able to model music data, in a way that captures the structure and patterns of music. GPT is "pre-trained" on a large corpus of musical data, which allows it to learn the nuances of music elements and context. This pre-training is followed by fine-tuning on specific tasks to further improve performance. The detail explanation of GPT framework as well as source code can be found in `` [directory]().

# Result & Evaluation
# Conclusion

   


