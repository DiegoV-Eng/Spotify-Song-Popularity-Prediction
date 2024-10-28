# Data Integration
The [```data_integration.ipynb```](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/data%20integration/data_integration.ipynb) notebook takes the raw data from the [10+ M. Beatport Tracks / Spotify Audio Features](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features), combines into a single .csv file along with the popularity we obtained from Spotify for each individual track. 
## Requirements
Due to the large size of the raw data files we are working with theses locally. To produce the final integrated data CSV file the following need to be present in the folder:
```
'.../data/raw kaggle data/'
```

| File Name                | Link                                                                                       |
| -------------------------|------------------------------------------------------------------------------------------- |
| `audio_features.csv`     | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=audio_features.csv) |
| `sp_artist.csv`          | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_artist.csv) |
| `sp_release.csv`         | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_release.csv) |
| `sp_track.csv`           | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_track.csv) |
| `sp_artist_release.csv`  | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_artist_release.csv) |

## Process

1. Select popular releases of type single
   - The same track can be released more than once in different releases and the measured popularity is recorded independently, so we will only be examining single releases.
3. Extract all tracks from these releases
4. Add individual track popularity obtained from Spotify Web API
   - Once we had the list of tracks contained in popular releases we obtained the their popularity using [```get_track_popularity.ipynb```](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/data%20integration/get_track_popularity.ipynb)
6. Add track data from remaining CSV files 
7. Clean up the final set
