# music-genre-classification
For this project, we are building a machine learning pipeline for music genre classification. The system will be trained to match songs with their corresponding genre based on audio files and/or song stats.  

## Datasets

### GTZAN Audio Dataset
~\MLP2\rawdata\genres  
This dataset contains a total of 1,000 30-second waveform audio files, divided into 10 genres: blues, classical, disco, hip-hop, jazz, metal, pop, reggae, and rock.  

#### Attributes
Genre: a discrete class label indicating the song's genre, which will act as our expected outputs  
Predictive attributes/features were extracted from the audio.  
The features we have extracted from the audio are as follows:  
- BPM  
- Zero-Crossing Rate (rate of sign changes from positive to negative)  
- Spectral Centroid (weighted mean of frequencies present in the song)  
- Spectral Rolloff (measures of shape of the signal, models human voice characteristics)  
- Mel-Frequency Cepstral Coefficients (measures shape of spectral envelope)  
- Chroma Frequencies (measure of frequencies of different pitches, separated into 12 bins)  
- Intensity: loudness in dB (relative to max possible loudness)  

#### Size
1000 instances (100 for each genre, each 30-seconds in length)

### Kaggle Dataset
~\MLP2\rawdata\music_genre.csv  
This is a csv file containing statistics and genres of several songs (audio features were provided by spotify).  
The advantage of this dataset is that the features (energy, valence, etc.) are already present in the dataset.  
We are planning on building our model with the audio file dataset, but we will try to extract features from the waveform files that are also present in the csv.  
Therefore, we can refit the model to a second dataset.  

#### Attributes
instance_id: unique identifier for each song  
artist_name: name of the artist who released the song  
track_name: name of the song  
popularity: defines the amount of listens the song has received relative to other tracks (on a scale from 0 to 99)  
acousticness: the level of acousticness (between 0 and 1)  
danceability: a numerical measure of how easy the song is to dance to (between 0 and 1)  
duration: The length of the song (seconds)  
energy: a numerical measure of how energetic the song is (between 0 and 1)  
instrumentalness: the level of instrumentalness (between 0 and 1)  
key: A discrete value to indicate the song's key  
liveness: the level of liveness (between 0 and 1)  
loudness: how loud the song is (measured in dB)  
mode: whether the song is major or minor (discrete)  
speechiness: the level of speech detected in the song (between 0 and 1)  
tempo: the song's tempo (BPM)  
obtained_date: the date the author obtained the instance (not relevant to our model)  
valence: a numerical measure of the song's mood (between 0 and 1, with 0 having the least positive mood and 1 having the most positive mood)  
music_genre: a discrete class label indicating the song's genre, which will act as our expected outputs  

#### Size
50005 instances (rows)  
18 attributes (columns)  

#### Data Cleaning
For the GTZAN audio dataset, we applied normalization to all of the features we extracted. This was done by:  
- taking the means of each feature value for each song (there was a value for each time a song was sample)  
- applying normalization to the means (on a scale from 0 to 1)  
We also applied normalization to the popularity, duration, loudness, and tempo attributes.  
Many tracks have an unknown duration and tempo (indicated by "-1" and "?" respectively).  
We experimented with both dropping instances with null data and replacing fields with the mean value to see how the model results compare once we build the model.  
