
# Week 4

## Wed 04/10
*Present: Alex Alexandra Diego Sai Sankalp*
Sankalp joined the group after switching course. 

As we were analysing the data sets an issue arose regarding popularity. This is the feature we are using as our target variable but is only included in the Spotify releases data set and it measures the popularity of a certain release (album) rather than tracks cointained in it. We decided the best thing to do is to create a list of all tracks contained in popular releases, i.e. the popularity of the release is > 0 and obtain their popularity from spotify's API. Then we will create our final data set where we'll initialise the popularity at 0 and then update it with the popularities obtained as previously described. 

## Thu 05/10
*Present: Alex Diego Sai Sankalp*

As we were researching how to access Spotify's API, we went over [Spotify's Developer Terms](https://developer.spotify.com/terms) which have limitations under which  the scope of our project falls. As our work is purely academic we decided to proceed, however caution must be taken to ensure that none of our work gets published anywhere and is kept secure.

## Fri 06/10
*Present: Alex Alexandra Diego*

A list containing all **track_id**s from **release_id**['popularity'] > 0 was generated. From Spotify API, we than gathered the popularities of the first 50 tracks, to see if your code was working. We discussed pontential feature engineering and planned our next steps of preprocessing and data gathering. 

We ideally want to measure the popularity in relation of the **isrc** (International Standard Recording Code). This is unique for every song. **track_id** on the other hand is referencing a track on a release, so a single **isrc** can be linked to multiple **track_id**s, which will have multiple popularity scores, even though it is the same song.  We need to figure out how tackle this. 

To complete the inital dataset we'll use the AUDIO_FEATURES as a starting point and possibly add the following from other sets (or gather ourselves):
- track_popularity
- track_title
- performing_artist(s) (could be more than one)
- track_id(s) (all relevant id's linked to the **isrc**)
- label (the label a track has been released under, note: we need to investigate if this could have multiple values as well as e.g. a track that has been re-released years later, when the artist has signed with a different label)
- release_date (this will come from SP_RELEASE, so again will have multiple values assosiated with a track, so we need to decide how we want to tackle this.  

Quite some time we spent discussing our github workflow. Some handwritten notes were taken and will be shared with everyone who couldn't attend.

At first we have decided to use PyTorch for creating specrogramm from audio sample, but we have ran into issues that image created was too large both in file size and dimensions of the image. Then we decied to use Parselmouth. Parselmouth is a Python library for the Praat software. Praat is a free computer software package for speech analysis in phonetics. This week we optimiesd our script for creating Specrograms. They are now both smaller is size(<100kB) and dimentions. Audio and spectrogram are now also saved accordingly in separate folders, but the audio file now is deleted after Spectrogramm is created.

## Task for next week: ##
 
TO DO:
- Create Spotify Dev accounts (everyone) and complete the popularity scores.
- Begin drafting a notebook for visualisation to plug our data once it's all set up.
- Finalise completing the dataset.
- Complete EDA and start Feature engineering.
- Figure out how to average popularity over a few different tracks with the same **track_id**
- Research Clusters and Desicion trees so we can start implementing straight away once the data is done
