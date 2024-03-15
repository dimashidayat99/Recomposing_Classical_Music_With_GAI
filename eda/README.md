# EDA Framework
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/framework/eda_framework.png"  width="300" />
</p>
<p align="middle">
    <em>Exploratory Data Analysis Workflow.</em>
</p>

The process of Exploratory Data Analysis (EDA) is shown in figure above where it begins with gathering the classical music midi data. The data the was undergone sampling process where only chopin music will be choosen. There are two type of EDA, the first type of EDA is directly toward the exploration of the music itself without data preprocessing where the music sheet and audio was produced to get better understanding on the music on how music sounds like and how the musics notes and durations looks like.

# Music Composition
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/music_sheet_audio/eda_sheet_music.png"  width="800" />
</p>
<p align="middle">
    <em>One of Chopin Composed Music, Music Sheet.</em>
</p>


<div align="center">

<video src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/assets/69446089/e531ea2b-ec2f-4fc1-b451-e12e0e71d873" width=400 />
</div>
<p align="middle">
    <em>One of Chopin Composed Music, Music Audio</em>
</p>

The process continue with the data preprocessing where each of the Chopin composed music was undergone clef spliiting where the treble and bass clef was separated. Each of the clef was undergone the music element extraction where the notes, chords and durations were extracted for the dataframe construction. There are two total dataframe was created which are treble dataframe and bass dataframe, each represent treble clef and bass clef respectively. Each dataframe consist of two features where the first features consisting the notes and chords while the second features consisting durations. The chords and notes were extracted based on their pitch freuency while the durations were extracted based on the durations type. Each of the dataframe were underwent the second type of EDA which is more toward data analytics. The EDA includes the univariate analysis, mutlivariate analysis and outliers analysis. 

# Univariate Analysis
## Bass Clef
### Pitch Frequency Distribution

<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/univariate_analysis/pitch_frequency_distribution_bass.png"  width="800" />
</p>
<p align="middle">
    <em>Pitch Frequency Distribution for Bass Clef Data.</em>
</p>

The distribution of pitch frequency is positively skewed with the modes around 160 $s^-{1}$. Majority of the chords and notes used is in the frequencies of 50 $s^{-1}$ to 300 $s^{-1}$. While chords and notes with frequencies around 500 $s^{-1}$ and above can be seen as minority chords and notes used in the Chopin composed music. 

### Duration Distribution

<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/univariate_analysis/durations_distribution_bass.png"  width="800" />
</p>
<p align="middle">
    <em>Duration Distribution for Bass Clef Data.</em>
</p>

Majority of the durations used was 8th notes with around 17500 counts followed by 16th note with around 14000 counts. The quarter notes is in the third position with around 7500 count. Other than the mentioned durations which are whole note, half note, complex note, breve note and 32nd note are the minority durations in the Chopin compoased music.

## Treble Clef
### Pitch Frequency Distribution

<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/univariate_analysis/pitch_frequency_distribution_treble.png"  width="800" />
</p>
<p align="middle">
    <em>Pitch Frequency Distribution for Treble Clef Data.</em>
</p>

The distribution of pitch frequency is positively skewed with the modes around 350 $s^-{1}$. Majority of the chords and notes used is in the frequencies of 200 $s^{-1}$ to 1300 $s^{-1}$. While chords and notes with frequencies around 1500 $s^{-1}$ and above can be seen as minority chords and notes used in the Chopin composed music.

### Duration Distribution

<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/univariate_analysis/durations_distribution_treble.png"  width="800" />
</p>
<p align="middle">
    <em>Duration Distribution for Treble Clef Data.</em>
</p>

Majority of the durations used was 16th notes followed by 8th note. The quarter notes is in the third position with around 6500 counts. Other than the mentioned durations which are whole note, half note, complex note, breve note and 32nd note are the minority durations in the Chopin compoased music.

## Both Clef
### Pitch Frequency Distribution
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/univariate_analysis/durations_distribution_both.png"  width="800" />
</p>
<p align="middle">
    <em>Pitch Frequency Distribution for Both Clef Data.</em>
</p>

The distribution of pitch frequency is positively skewed with the modes around 250 $s^{-1}$. Majority of the chords and notes used is in the frequencies of 50 $s^{-1}$ to 750 $s^{-1}$. While chords and notes with frequencies around 1000 $s^{-1}$ and above can be seen as minority chords and notes in the Chopin composed music.

### Duration Distribution
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/univariate_analysis/durations_distribution_both.png"  width="800" />
</p>
<p align="middle">
    <em>Duration Distribution for Both Clef Data.</em>
</p>

Majority of the durations used was 8th notes with 35000 count followed by 16th note with around 32500 counts. The quarter notes is in the third position with 15000 counts. Other than the mentioned durations which are whole note, half note, complex note, breve note and 32nd note are the minority durations in the Chopin compoased music.

# Multivariate Analysis
## Bass Clef

<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/multivariate_analysis/durations_vs_pitch_frequency_bass.png"  width="800" />
</p>
<p align="middle">
    <em>Violnin Plot of Duration against Pitch Frequency for Bass Clef Data.</em>
</p>


The 8th note, 16th note and quarter note have almost similar shape of distribution which is almost symmetric. Majority of the notes are in the range of 30 $s^{-1}$ to 400 $s^{-1}$. The range of 8th note distribution is around 20 $s^{-1}$ to 1300 $s^{-1}$ while te range of 16th note distribution is around 20 $s^{-1}$ to 1400 $s^{-1}$. Half note has similar distribution of majority of the notes but postively skewed with the mode around 100 $s^{-1}$. The whole note has a mode around 80 $s^{-1}$ with majority of the notes is in the range of 20 $s^{-1}$ to 200 $s^{-1}$. The complex note has the range of distribution of 0 $s^{-1}$ to 1400 $s^{-1}$ with majority of the notes is in the range of 0 $s^{-1}$ to 400 $s^{-1}$. Both breve note and 32nd note has almost the same shape of distribution with almost same modes around 100 $s^{-1}$. Also, both have the same range of distribtion which from 0 $s^{-1}$ to around 360 $s^{-1}$.

## Treble Clef

<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/multivariate_analysis/durations_vs_pitch_frequency_treble.png"  width="800" />
</p>
<p align="middle">
    <em>Violnin Plot of Duration against Pitch Frequency for Treble Clef Data.</em>
</p>

The half note, quarter note, 8th note and 16th note have almost similar shape of distribution which is slight positively skewed with almost similar range where most notes are in the range of 200 $s^{-1}$ to 1000 $s^{-1}$ with the distribution range of 200 $s^{-1}$ to 2900 $s^{-1}$. The whole note has a mode around 450 $s^{-1}$ with distribution range of 150 $s^{-1}$ to 1000 $s^{-1}$. The complex note has the longest range of distribution of 0 $s^{-1}$ to 3000 $s^{-1}$. The breve note distribution is the only negatively skewed in the treble clef dsitribution, the breve note distribution has mode around 500 $s^{-1}$ with the range of 200 $s^{-1}$ to 800 $s^{-1}$. The 32nd note distribution has mode around 500 $s^{-1}$ with the range of 0 $s^{-1}$ to 1750 $s^{-1}$ with the majority of the notes lies in the range of 200 $s^{-1}$ to 800 $s^{-1}$. 

## Both Clef
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/multivariate_analysis/durations_vs_pitch_frequency_both.png"  width="800" />
</p>
<p align="middle">
    <em>Violnin Plot of Duration against Pitch Frequency for Both Clef Data.</em>
</p>

The 8th note and 16th note have almost similar shape of distribution which is positively skewed with similar range where most notes are in the range of 30 $s^{-1}$ to 2800 $s^{-1}$ and mode of 200 $s^{-1}$ with majority of the notes lies in the range of 100 $s^{-1}$ to 1000 $s^{-1}$. Half note has similar distribution range but the distribution is symmetric. The quarter note distribution has notable mode around 250 with the range of 0 $s^{-1}$ to 1200 $s^{-1}$ with majority of the notes lies in the range of 100 $s^{-1}$ to 500 $s^{-1}$. The whole note distribution is positively skewed with the mode around 150 $s^{-1}$ with distribution range of 0 $s^{-1}$ to 1100 $s^{-1}$ with the majority of notes lies in the range of 50 $s^{-1}$ to 500 $s^{-1}$. The complex note has the longest range of distribution of 0 $s^{-1}$ to 3000 $s^{-1}$. Both breve note and 32nd note, both are positively skewed but different shape and range. The range of distribtion of 32nd note is a bit longer compared to the range of distribtion of breve note while both have almost the same mode around 200 $s^{-1}$.

# Outliers Analysis
## Bass Clef
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/outlier_analysis/outliers_bass.png"  width="800" />
</p>
<p align="middle">
    <em>Box Plot of Music Elements for Bass Clef Data.</em>
</p>

From the plot, the median of the bass clef distribution is at 200 $s^{-1}$ with the interquartile range of 150 $s^{-1}$ to 250 $s^{-1}$. The bass clef distribution has maximum of around 500 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 500 $s^{-1}$ are identfied as outliers.

## Treble Clef
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/outlier_analysis/outliers_treble.png"  width="800" />
</p>
<p align="middle">
    <em>Box Plot of Music Elements for Treble Clef Data.</em>
</p>

From the plot, the median of the treble clef distribution is at 500 $s^{-1}$ with the interquartile range of 400 $s^{-1}$ to 750 $s^{-1}$. The bass clef distribution has maximum of around 1300 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 1300 $s^{-1}$ are identfied as outliers.

## Both Clef
<p align="middle">
<img src="https://github.com/dimashidayat99/Recomposing_Classical_Music_With_GAI/blob/main/eda/outlier_analysis/outliers_both.png"  width="800" />
</p>
<p align="middle">
    <em>Box Plot of Music Elements for Both Clef Data.</em>
</p>

From the plot, the median of the both clef distribution is at 300 $s^{-1}$ with the interquartile range of around 150 $s^{-1}$ to 500 $s^{-1}$. The both clef distribution has maximum of around 1000 $s^{-1}$ and minimum of around 50 $s^{-1}$. The notes above 1000 $s^{-1}$ are identfied as outliers.

The outliers analsis shows there are many outliers in the data. However, the technique used to deal with outliers is simply keep the outliers in the data. Dealing with outliers by removing will affect the sequences of the notes which make the music have high degree of disorderness in the notes sequences which may cause worst output of AI-generate music.

