What the folders contain: 

| Folder Name       | Description                                                                                                            |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `chunks`          | Contains segmented portions of track_id. Each chunk contains a group of 5,000 unique track IDs. |
| `chunks_popularity` | The 'chunks_popularity' folder contains data obtained by requesting track popularity information from Spotify using the [Spotipy](https://spotipy.readthedocs.io/en/2.22.1/) library. Each chunk within this folder corresponds to a group of tracks and includes their respective popularity data. |

 
Datasets that are combined together and subsequently processed to derive the ultimately refined dataset:

| File Name                | Link                                                                                                   |
| ------------------------ | -------------------------------------------------------------------------------------------------------------- |
| `audio_features.csv`     | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=audio_features.csv) |
| `sp_artist.csv`          | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_artist.csv) |
| `sp_release.csv`         | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_release.csv) |
| `sp_track.csv`           | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_track.csv) |
| `sp_artist_release.csv`  | [Download](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features/?select=sp_artist_release.csv) |
| `popularity_data.csv`    | [Download](https://drive.google.com/file/d/1V1SfnekzyCiKUz-ft0Tat4o9-irox0Pd/view?usp=sharing) (Stitched version of the data in chunks_popularity) |


Final dataset obtained: **integrated_data.csv** [LINK](https://heriotwatt-my.sharepoint.com/:x:/g/personal/dev2000_hw_ac_uk/EUT-uSUV_PZDj8zgGrZVQZABZrio9RcaP9xO2Iez4ZSRCQ?e=rGr155)



Final processed data: **processed_data.csv** [LINK](/data/processed_data.csv)
