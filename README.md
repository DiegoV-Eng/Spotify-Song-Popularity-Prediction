[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/58HShPQN)
# Data Mining and Machine Learning Group Coursework

## Group Members

1. Alex Varbanov @verbal-ale
2. Diego Velasquez @Diego15457
3. Alexandra Cures @ac234
4. Saiprasad Murali @saiprasadm1998
5. Sankalp Arora @sankalp-s

## Initial Project Proposal

### Project Plan
 1. Meet the team.
 2. Work on project proposal:
    - [x] Select a theme;
    - [x] Define project topic and direction.
 3. Data collection and selection:
    - [x] Explore available datasets;
    - [x] Compare and contrast;
    - [x] Define research questions;                   <!-- Clear questions and objectives based on the selected theme/datasets, identify specific problems or hypotheses to be addressed-->
    - [x] Select the data best fitting the scope of the project;
    - [x] State motivation of selection.               <!-- Explain how the data can be used for all models-->
 4. Exploratory data analysis:
    - [x] Visualise the data                                           <!--communicate insights and trends within the dataset // use Seaborn, Plotly or Matplotlib-->
    - [x] Preprocessing: clean up, address missing values, outliers, data quality issues;                <!-- use notebooks/scripts for that-->
      - [x] Set up Git LFS.
 5. Model selection and development:
    - [x] Research and select a set of supervised and unsupervised ML models;
    - [x] Discuss how the data can be used with those;                   <!-- including any formatting/manipulation or modifications to the data-->
    - [x] Research proof of concepts for the different models                             <!-- lab exercises/recommended reading-->
    - [x] **develop the model and document the process using Jupyter notebooks and Python scripts;**       <!-- number the books in order of execution -->
    - [x] **commit and push the model to the GitHub repository;**
 6. Evaluation and Analysis:
    - [x] Evaluate the performance of the models;      <!-- use notebooks/scripts for that-->
    - [x] Analyse the results and draw conclusions;   <!-- use notebooks/scripts for that-->
    - [x] **commit and push the evaluation code to the GitHub repository;**

  #### Additional Planning
  - [x] Feature Engineering to improve the predictive power of the models   <!-- explain the process and its impact on the performance-->
  - [x] Model Explainability and Interpretability                           <!-- do some research on this-->
  - [x] Cross-Validation                                    <!-- k-fold or time series CV to obtain a more robust model performance estimates-->
  - [x] Deployment                                   <!-- provide instructions on how to access and use the models-->
  - [ ] Continuous Integration                 <!-- how to set up CI/CD pipeline to automate testing/building/deploying code changes to ensure code reliability -->
  - [ ] Technical Blog                   <!-- weekly update of technical blog to showcase members work-->
  - [ ] Project Sustainability         <!-- how can this be maintained and improved in the future -->
  - [ ] Testing, including unit tests and integration tests           <!-- to ensure code reliability -->
  - [ ] Error Handling                                        <!-- gracefully handle unexpected situations -->
  - [ ] Documentation for End-users
  - [x] Compliance and Regulations

  - [ ] \(Optional) User Interface

### Milestones

> [!NOTE]
> Create a bullet list of the key milestones for your project. Discuss these with your group. You may need to update these as the project progresses.
>
 - R1. Project Topic, Direction, and Questions  ** Deadline: 29/09/23**
 - R2. Data Analysis and Exploration - ** Deadline: 06/10/23**
 - R3. Clustering - ** Deadline: 03/11/23**
 - R4. Decision Trees - ** Deadline: 05/11/23**
 - R5. Neural Networks and CNN - ** Deadline: 17/11**

## Findings Report

<!-- Below you should report all of your findings in each section. You can fill this out as the project progresses. -->

### Research objectives
1. **Feature Importance and Popularity:**
   - To identify the most influential audio and metadata features contributing to a song's popularity.
2. **Temporal Trends and Seasonal Variations:**
   - To analyze how music preferences and trends have evolved over time and to identify seasonal variations in the popularity of different music types.
3. **Spectrogram Analysis:**
   - To explore the potential of converting audio data into spectrograms and assess training machine learning models on spectrograms.

<!-- What questions you are trying to answer? -->

### Datasets
We are using the [10+ M. Beatport Tracks / Spotify Audio Features](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features?select=sp_track.csv) data set available on Kaggle
as a starting point.

### Motivation of selection:

The dataset we have compiled can be used for various machine learning and statistical models in the following ways

1. **Classification Models (e.g., Logistic Regression):** By defining a threshold for popularity, we can create a binary or multi-classification model to categorize songs' popularity. Features and metadata can be input to train the model to make these binary predictions.

2. **Decision Trees and Random Forests:** These models are valuable for understanding feature importance. They can help identify which audio and metadata features have the most influence on song popularity.

3. **Neural Networks:** Deep learning models, like neural networks, can handle complex patterns in the data and may be used to predict popularity, categorize genres, or detect trends. Spectrograms can be integrated into these models for image-based analysis.

4. **Clustering Models:** These models can group songs with similar audio characteristics or other features. Clustering can be used for market segmentation or to discover common patterns among popular songs.

The dataset's versatility in audio features, metadata, and even spectrograms enables us to explore various modelling techniques tailored to address specific research questions and objectives within the music industry and analytics domain.

#### Dataset description
<!-- Briefly describe your task and dataset -->
We chose this set in particular for its large size both in number of samples and sample features.
It contains information about music (tracks, artist, labels and releases) from the major online music platform: **Spotify**.

We are interested in examining technical **audio features** and **metadata** of a track and how they relate to its **popularity**. A few things to note:
1. [10+ M. Beatport Tracks / Spotify Audio Features](https://www.kaggle.com/datasets/mcfurland/10-m-beatport-tracks-spotify-audio-features?select=sp_track.csv) was gathered in the context of electronic music genre classification which imposes a limitation in terms of audio features.
2. The popularity of a song is influenced by factors not present in our data.
3. The popularity of a song is measured on a specific point in time.
4. We only have the measured popularity of releases and not indivudual tracks.
5. [Spotify's Developer Terms](https://developer.spotify.com/terms) which have limitations under which  the scope of our project falls. As our work is purely academic we decided to proceed, however caution must be taken to ensure that none of our work gets published anywhere and is kept secure.

We will be focusing on _Spotify_ (prefix sp_*) only as it contains the said features.

<details>
  <summary> *note on file size:</summary>

  This data set is broken down into 10 smaller subsets. As some of these files exceed the allowed 100Mb limit on GitHub we will work with them locally, as we still need to configure the Git LFS. We will be using the following to create our inital dataset:

  |file name              | file size |
|-----------------------|-----------|
| audio_features.csv    | 470Mb     |
| sp_artist.csv         | 37Mb      |
| sp_release.csv        | 125Mb     |
| sp_track.csv          | 1.25Gb    |
| sp_artist_release.csv | 260Mb     |
</details>

#### Data Integration
We combined the data from the following datasets: 
```
"audio_features.csv," "sp_artist.csv," "sp_release.csv," "sp_track.csv," "sp_artist_release.csv"
```
using the shared indentifiers: 
```
'release_id', 'artist_id', 'isrc'
```
To acquire song popularity information, we started by making a list of all tracks contained in releases that have some popularity. We then individually initiated a [Spotify developer account](https://developer.spotify.com/) and utilized the [Spotipy](https://spotipy.readthedocs.io/en/2.22.1/) library to request and gather song popularity data. These diverse data sources were merged  to form our final, all-encompassing dataset.

For more information see: [data integration](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/tree/main/notebooks/data%20integration).

#### Key Features
Here is a table of notable features and their descriptions:

|feature     |value range| description |
|------------|------------|-------------|
| **track_id**        |                                                 | unique id of a track.|
| **explicit**           |true = yes it does; false = no it does not OR unknown | Whether or not a track has explicit lyrics.|
| **preview_url**        | can be null                                                 | A link to a 30 second preview (MP3 format) of a track.|
| **acousticness**       |between 0.0 and 1.0, 1.0 represents high acousticness  |A confidence measure  of whether the track is acoustic|
| **danceability**       |between 0.0 and 1.0, 1.0 represents high dancibility |Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity.|
| **duration_ms**        |above 0.0| Measurement of length of track in seconds|
| **energy**             |between 0.0 and 1.0, 1.0 represents high energy |Energy represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale. Perceptual features contributing to this attribute include dynamic range, perceived loudness, timbre, onset rate, and general entropy.|
| **instrumentalness**   |between 0.0 and 1.0, 1.0 represents high instrumentalness. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0. |Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly "vocal". The higher the value, the greater likelihood the track contains no vocal content. |
| **key**                |-1 = no key detected, 0 = C, 1 = C♯/D♭, 2 = D, and so on. |The key the track is in. Integers map to pitches using standard Pitch Class notation.|
| **liveness**           |between 0.0 and 1.0, 1.0 represents high liveness. A value above 0.8 provides strong likelihood that the track is live. | Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live.|
| **loudness**           |typically range between -60 and 0 db |The overall loudness of a track in decibels (dB). Loudness values are averaged across the entire track and are useful for comparing relative loudness of tracks. Loudness is the quality of a sound that is the primary psychological correlate of physical strength (amplitude).|
| **mode**               |1 for major, 0 for minor |Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived.|
| **speechiness**        |between 0.0 and 1.0, 1.0 represents high speechiness. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks.|Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value.|
| **tempo**              | Should be >0, Here are "typical" tempo ranges for a number of common genres: Dub: 60-90 bpm. Hip-hop: 60-100 bpm. House: 115-130 bpm just for example. |The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration.|
| **valence**            |between 0.0 and 1.0, 1.0 represents high valence |A measure describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry).|
| **artist_name**        | |The name of the artist.|
| **popularity**         |between 0 and 100, with 100 being the most popular           |The popularity is calculated by algorithm and is based, in the most part, on the total number of plays the track has had and how recent those plays are. Generally speaking, songs that are being played a lot now will have a higher popularity than songs that were played a lot in the past.* Duplicate tracks (e.g. the same track from a single and an album) are rated independently. Artist and album popularity is derived mathematically from track popularity.|
| **release_date**       |                                                            | The date an album was first released.|

*_Note: the popularity value may lag actual popularity by a few days: the value is not updated in real time._

#### Dataset examples
<!--DROP format : track_id, isrc, explicit to boolean, drop track_title, URL  drop, release id, -->

| track_id            | explicit | preview_url                                                | acousticness | danceability | duration_ms | energy | instrumentalness | key | liveness | loudness | mode | speechiness | tempo | valence | artist_name  | popularity | year | month |
|---------------------|----------|-----------------------------------------------------------|--------------|--------------|------------|--------|------------------|-----|----------|----------|------|-------------|---------|-----------------------|-------------|------------|------|-------|
| 6QXxvRGql81hrkNKl1sJNy | f | [Link](https://p.scdn.co/mp3-preview/1883d8ef8a5628f0...) | 0.60300 | 0.656 | 188781 | 0.336 | 0.522000 | 3 | 0.0721 | -13.096 | 1 | 0.0345 | 82 | 0.119 | Evate | 21.0 | 2019 | 9 |

*_Note: release_date is split into year and month columns._

<!-- Drop from dataset, release_pop, album_type, updated_on,  -->
Dataset format:

|   Index   | Column             | Non-Null Count   | Dtype   |
|-------|--------------------|------------------|--------|
|   0   | acousticness        | 477862 non-null  | float64|
|  1   | danceability        | 477862 non-null  | float64|
|  2   | duration_ms         | 477862 non-null  | int64  |
|  3   | energy              | 477862 non-null  | float64|
|  4   | instrumentalness    | 477862 non-null  | float64|
|  5   | key                 | 477862 non-null  | int64  |
|  6   | liveness            | 477862 non-null  | float64|
|  7   | loudness            | 477862 non-null  | float64|
|  8   | mode                | 477862 non-null  | int64  |
|  9   | speechiness         | 477862 non-null  | float64|
|  10   | tempo               | 477862 non-null  | int64  |
|  11   | valence             | 477862 non-null  | float64|
|  12   | popularity          | 477862 non-null  | float64|

dtypes: float64(9), int64(4)
<!-- Add a couple of example instances and the dataset format -->

#### Dataset exploration

1. Size of the dataset:

| Number of Rows | Number of Columns |
| -------------- | ------------------ |
| 489,524        | 19                |

2. Summary Statistics of the dataset:

| Statistic          | acousticness | danceability | duration_m  | energy | instrumentalness | liveness | loudness | speechiness | tempo  | valence | popularity |
|-------------------- |-------------- | ------------ | ------------- | ------ | ---------------- | -------- | -------- | ----------- | ------ | ------- | ---------- |
| Mean               | 0.083         | 0.687         | 5.509         | 0.748  | 0.589            | 0.171   | -8.344  | 0.086       | 128.468 | 0.402   | 5.289     |
| Standard Deviation  | 0.185         | 0.140         | 1.866         | 0.190  | 0.356            | 0.159   | 3.672   | 0.082       | 20.268  | 0.254   | 8.197     |
| Median             | 0.008         | 0.715         | 5.588         | 0.785  | 0.783            | 0.109   | -8.075  | 0.058       | 126.000 | 0.373   | 2.000     |
| Minimum            | 0.000         | 0.023         | 0.256         | 0.000  | 0.000            | 0.004   | -58.660 | 0.022       | 31.000  | 0.000   | 0.000     |
| Maximum            | 0.996         | 0.995         | 80.510        | 1.000  | 0.999            | 0.994   | -0.001  | 0.968       | 250.000 | 1.000   | 83.000    |
| 25th Percentile    | 0.001         | 0.613         | 4.133         | 0.632  | 0.210            | 0.082   | -10.225 | 0.045       | 121.000 | 0.185   | 0.000     |
| 75th Percentile    | 0.056         | 0.794         | 6.736         | 0.903  | 0.880            | 0.188   | -6.003  | 0.087       | 135.000 | 0.592   | 7.000     |

Key Feature Observations

| Feature         | Observation                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------|
| Acousticness    | A mean of 0.083 indicates that, on average, songs in the dataset have a low level of acoustics, suggesting the dataset mainly consists of electronic music.                   |
| Danceability    | A high mean of 0.687 indicates that the songs are, on average, quite danceable, with a relatively narrow distribution.      |
| Duration_ms     | The average song duration is 5.5 minutes, providing a reference for identifying outliers.       |
| Energy          | A high mean of 0.748 indicates that, on average, songs in the dataset are energetic.             |
| Instrumentalness | A mean of 0.589 suggests that, on average, songs are mostly instrumental.                       |
| Liveness        | A mean of 0.171 indicates that the dataset contains fewer live recordings.                        |
| Loudness        | The "loudness" feature has a mean of -8.344, indicating that songs in the dataset are, on average, relatively loud.         |
| Speechiness     | The "speechiness" feature has a low mean of 0.086, indicating that, on average, songs have a low level of speech-like features, making them more beat-oriented, possibly electronic music. |
| Tempo           | The "tempo" feature has a mean of 128.468, representing the average tempo in BPM (Beats Per Minute), indicating that the average songs in the dataset are fast and bright, which are characteristics of electronic music. |
| Valence         | A mean of 0.402 indicates that, on average, songs in the dataset have a moderate positive valence. The standard deviation of 0.254 suggests variation in emotional tone. |
| Popularity      | The 75th percentile has a value of 7.000, indicating that 75% of the songs have a popularity level of 7 or lower. This suggests that a majority of the songs in the dataset might fall into the lower to moderate popularity range. |

These observations provide insights into the characteristics of the dataset's features, aiding in understanding the music data's composition and distribution.

<!-- What is the size of the dataset? -->
<!-- Train, validation, split? -->
<!-- Summary statistics of your dataset -->
<!-- Visualisations of your dataset -->
<!-- Analysis of your dataset -->

### Data Analysis

### 1. EDA 
Code notebook: [EDA_final.ipnynb](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/EDA/EDA_Final.ipynb)


Detailed documentation: [EDA_readme](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/EDA/README.md)

#### 1.1 Environment Setup and Data Import
The environment is configured, and essential libraries for data analysis and visualization are imported. The dataset ["integrated_data.csv"](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/tree/main/data) is loaded which is the raw, unprocessed data compiled from various sources, which will undergo extensive data processing and analysis.

#### 1.2 Data Preprocessing
The dataset is prepared through a series of steps:
- The "release_date" column is split into year, month, and day components.
- Unnecessary columns are removed.
- Rows with missing values in specific columns are dropped.
- Relevant columns are transformed into their appropriate data types.
- Columns are scaled to enhance visualization and comprehension.

#### 1.3 Handling Numerical Data
Emphasis is placed on numerical features, with the following actions:
- Identifying and addressing outliers.
- Creating informative visualizations to gain insights.
  
#### 1.4 Handling Categorical Data
Categorical variables "key" and "mode" are one-hot encoded, transforming them into binary variables.

#### 1.5 Feature Selection
Feature selection is conducted using two methods:


1.5.1 **Correlation-Based Feature Selection:** Identifying features with the strongest positive or negative correlations with the target variable "popularity."


1.5.2 **Tree-Based Model Feature Selection:** Evaluating feature importance through Decision Tree and Random Forest models.

#### 1.6 Informative Visualizations
Various visualizations enhance data comprehension. These include visualizations of popularity distributions, box plots, scatter plots, mean popularity by year, mean popularity by season, and mean popularity by artist.

#### 1.7 Categorization
The target variable "popularity" is categorized into three labels: "low," "medium," and "high."

#### 1.8 Addressing Class Imbalance
Class imbalance is tackled through oversampling techniques: Random Oversampler and SMOTE (Synthetic Minority Over-sampling Technique).

#### 1.9 Data Normalization
Certain numerical features are normalized using standard scaling for consistent scaling.

*_Note: For detailed documentation on how specific features are handled and the details of specific features, please refer to the following link: [Eda_readme](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/EDA/README.md)._

---


### 2. Visualizations

These visualizations cover a wide range of aspects, including feature distributions, correlations, and relationships with the target variable. They serve as a critical resource for understanding the dataset's characteristics and trends, aiding in the decision-making process for subsequent data analysis and modeling. The visualizations are organized and labeled for easy reference, ensuring that all essential aspects of the data are visually represented and accessible for further exploration and analysis.

#### 2.1 Feature Distribution Analysis

In this section, we examine the distributions of various features from our dataset using distribution plots. Each subplot in the grid provides insights into the distribution characteristics of different features.

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/Distplots.png" alt="Distribution plots" width="850" height="750">
</p>

The key observations are as follows:

- The duration (duration_m) of songs exhibits a right-skewed distribution with a prominent peak at shorter durations.
- The instrumentalness feature's distribution is right-skewed, signifying a significant presence of non-instrumental tracks.
- A substantial portion of songs displays low acousticness, indicating a preference for non-acoustic music.
- The loudness feature's distribution is centered around the mean, suggesting a relatively uniform spread.
- Popularity scores follow a right-skewed distribution, with the majority of songs concentrated in the lower popularity range.

The feature selection analysis in [EDA_Final.ipynb](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/EDA/EDA_Final.ipynb) utilized correlation-based matrices and tree-based models to identify key features 

Using heatmaps as a visualization tool.

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Heatmap.png" alt="Distribution plots" width="800" height="750">
</p>

Using tree-based models to get the feature importance scores:

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Regressors.png" alt="Distribution plots" width="500" height="450">
</p>

In conclusion, these 4 features exert a substantial influence on a song's popularity:
- **Acousticness**
- **Instrumentalness**
- **Danceability**
- **Energy**

To visualize the relationships between these key features and popularity, scatter plots are created using Seaborn's [`sns.scatterplot`](https://seaborn.pydata.org/generated/seaborn.scatterplot.html):

| Acousticness vs Popularity   | Instrumentalness vs Popularity |
| ---------------------------  | ------------------------------ |
| ![Image 1](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/Acousticness.png) | ![Image 2](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/Instrumentalness.png) |
| Danceability vs Popularity   | Energy vs Popularity         |
| ![Image 3](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/danceability.png) | ![Image 4](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/energy.png) |

#### 2.2 Understanding target variable (popularity)

The distribution of the 'popularity' feature, which serves as the target variable in our analysis, is visualized. This visualization is crucial for understanding the distribution of song popularity scores in the dataset, allowing us to assess central tendency measures like the mean and median and facilitating the identification of patterns and trends. These insights are considered valuable for subsequent data analysis and modeling tasks.

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Popularity_hist.png" alt="Distribution plots" width="800" height="450">
</p>

To detect the potential outliers and extreme values in the 'popularity' feature box plot visualization are used.

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Popularity_box.png" alt="Distribution plots" width="800" height="450">
</p>

#### 2.3 Underlying patterns (Changes in mean popularity with years, average duration of songs, seasonal popularities)

In this section, an examination is conducted to unveil underlying patterns and insights pertaining to song popularity. Mean popularity trends over the years are scrutinized, seasonal variations in song reception are identified, and an improved understanding of how works by different artists are received by the audience is gained. Additionally, a weighted mean for song duration by year is computed, facilitating an exploration of how song lengths have evolved and whether any noticeable trends in listener preferences can be identified. These analyses provide a richer context for understanding the dynamics of music popularity within the dataset.

2.3.1 Mean Popularity by Year

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Mean_pop_year.png" alt="Distribution plots" width="800" height="450">
</p>

A more accurate representation of the data is achieved by considering variations in importance or significance among the data points when using the weighted mean.

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Weighted%20mean%20popularity.png" alt="Distribution plots" width="800" height="450">
</p>

The observed exponential increase in the weighted popularity of songs after 2008 suggests a notable surge in the audience's interest, particularly in the realm of electronic music (since our dataset mostly comprises electronic music). This trend indicates an expanding fan base and heightened appreciation for electronic music genres since 2008.

2.3.2 Average Duration by Year

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Average_duration.png" alt="Distribution plots" width="800" height="450">
</p>

The graph depicting the average duration by year reveals a predominant range of 5 to 7.5 minutes for song durations. Furthermore, it illustrates a declining trend in average song durations over the years.

2.3.3 Mean Popularity by Seasons

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Popularity%20with%20seasons.png" alt="Distribution plots" width="600" height="500">
</p>

The visualization of mean popularity by seasons, including autumn, spring, summer, and winter, showcases subtle variations in popularity. Songs released in summer tend to have slightly higher mean popularity (5.42), while those in spring and autumn hover around similar popularity levels (5.26 and 5.23, respectively). This suggests that the season of release might have a minor influence on song popularity, with summer releases attracting a slightly larger audience.

2.3.3 Relative frequencies

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/assets/Freq_dist.png" alt="Distribution plots" width="550" height="500">
</p>

In the analysis, an imbalanced relative frequency distribution of the 'popularity' categories was observed, with the 'low' popularity category being identified as the majority class, while the 'medium' and 'high' popularity categories were represented as the minority classes. Imbalanced datasets may result in model bias and reduced performance, as the predictions tend to be dominated by the majority class, while the minority classes receive less attention. To mitigate this issue and ensure that fair predictions can be made across all popularity categories, the Synthetic Minority Over-sampling Technique (SMOTE) was employed. SMOTE is systematically used to generate synthetic samples from the minority classes, thus creating a more balanced dataset. This approach allows performance improvement in the model and the reduction of bias when predicting popularity categories, ensuring that the 'medium' and 'high' categories receive the attention they deserve in our analysis."

**With these preprocessing steps completed, our dataset is now primed and prepared for training on various classification models.**
### Clustering

#### Examining Popularity with Clustering
This is a short summary of our findings, for the full report see [Examining Popularity with Clustering](/notebooks/models/Clustering//README.md)

Notebooks: 

[001_clustering_mehtod_selection](/001_clustering_mehtod_selection.ipynb)

[002_clustering_popularity_analysis](/002_clustering_popularity_analysis.ipynb)


#### Experimental design

In this section of the project, we explore the concept of clustering to uncover patterns and groupings within the Spotify dataset. The goal is to identify any inherent structures or natural divisions among songs based on their audio features. To achieve this, we adopted the following experimental design:

1. **Data Preparation**: We began by selecting a subset of relevant audio features, such as ```acousticness```, ```instrumentalness```, ```energy```, and ```danceability```, which offer insights into a song's characteristics. We examined their relationship through scatter plots. 

2. **Clustering**: We selected a  few suitable clustering algorithms to group songs based on their audio feature similarity. While we considered various clustering techniques, we had limitations in stemming from the size of our dataset and its homogeneity. We evaluated the performance of each algorithm using The Silhouette Coefficient, the Calinski-Harabasz Index and the Davies-Bouldin Index. 

3. **Clustering Analysis**: We looked at how the clusters are formed in terms of audio features and gave those a suitable name. We then explored the differences in popularity within every category. 

#### Results
1. **The Raw Data**: We found that the data is quite homogenous and does not form intuitive clusters. After examining the probability density plots of each of the 4 key features we determined that there could be at most 8 meaningful groups. 
<img src="/assets/4_key_feats_kde_plots.png" alt="Raw Data KDE Plots" width="650"/>
<img src="/assets/4_key_feats_scatter_plots.png" alt="Raw Data Scatter Plots" width="650"/>

2. **Clustering**: We examined four clustering algoritms in total: **K-means, Bisecting K-means, BIRCH and DBSCAN**. We found that K-means with K=3, gives the most well-defined groupings, while DBSCAN with ```eps=0.7``` has the best average evaluation, it only produced 2 clusters, split on ```instrumentalness``` and no difference in popularity was detected.

3. **Clustering Analysis:** Using radar plots we got a better understanding of what the categories are. We defined labels for the clusters and added them to the raw dataset to investigate how they are relating to the popularity of tracks. The labels are as follows:

**Balanced Relaxing** - (vis. in purple) has mid danceability and energy, high acousticness and instrumentalness. 

**Party Instrumental** - (vis. in teal) that has an average high instrumentalness, danceability and energy. We note that it has essentially no acousticness.

**Party Lyrical** - (vis. in yellow) has high energy and danceability, but essentially no acousticness and instrumentalness.  

![clustered radar plots](/assets/k-means_radar_plots.png)
![clustered pie chart](/assets/k-means_pie_chart.png)

Finally we investigated the popularity within each cluster. As the data is heavily skewed we examined the IQR as well.

![clustered popularity histogram](/assets/populaity_in_k-means_clusters_hist.png)
![clustered popularity IQR histogram](/assets/populaity_in_k-means_clusters_IQR_hist.png)

The mean popularity in each category is: 
```
Party Lyrical Mean Popularity:      7.910419974812462
Party Instrumental Mean Popularity: 4.905751311391957
Balanced Relaxing Mean Popularity:  7.2391912147724495
```
We can see that **tracks that are lyrical are more likely to be popular** than tracks that are not. Lyrical tracks with high energy/danceability are slightly more popular than the minorty of balanced ones present in the data.

##### Limitations and applicability
When considering the results of the clustering experiment one should keep in mind the composition of the raw data. As seen in the exploratory stage as well as when looking for an optimal value for the distance between data points, the data is extremely homogeneous, so the clustering itself is not very substantial. This comes from the fact that the dataset consists of mainly electronic music, i.e. a single genre and the features describing the tracks are too general to capture the nuances between sub-genres. Perhaps, a similar genre-specific experiment could be conducted using more technical-specific data in terms of audio features. Or, if the data spans over several genres, the same experiment could produce more meaningful results.


#### Results

The clustering process yielded several notable results:

1. **Optimal K Value**: After a thorough evaluation using the Elbow Method and Silhouette Score, we determined that the optimal number of clusters for this dataset is K=5. This value was chosen as it represents a balance between granularity and interpretability.

2. **Cluster Assignments**: Each song in the dataset was assigned to one of the five clusters based on the similarity of their audio features. This assignment allowed us to examine the characteristics shared by songs within the same cluster.

3. **Interpretation of Clusters**: By exploring the central tendencies of the features within each cluster, we could infer the audio characteristics that define each group. This helped in understanding the audio profiles of different song categories.

4. **Classification Report: Precision, Recall, and F1-Score**
   
|   | Precision | Recall | F1-Score | Support  |
|---|-----------|--------|----------|----------|
| High  | 0.94 | 1.00 | 0.97 | 131,264 |
| Low   | 0.75 | 0.65 | 0.70 | 130,755 |
| Medium| 0.70 | 0.75 | 0.73 | 130,631 |
|---|-----------|--------|----------|----------|
| Accuracy |     |       | 0.80     | 392,650 |
| Macro Avg| 0.80| 0.80  | 0.80     | 392,650 |
| Weighted Avg| 0.80 | 0.80 | 0.80  | 392,650 |

<details>
  <summary> *Detailed classification report:</summary>


  High Popularity Category
- **Precision (0.94)**: In the "high" popularity category, our model achieved a high precision score. This indicates that when the model predicted a song as "high" popularity, it was correct 94% of the time.
- **Recall (1.00)**: The recall score for the "high" category is remarkably high, signifying that the model successfully identified all "high" popularity songs from the dataset.
- **F1-Score (0.97)**: The F1-score, a harmonic mean of precision and recall, is 0.97 for the "high" category. This suggests a strong balance between precision and recall.

Low Popularity Category
- **Precision (0.75)**: In the "low" popularity category, the model displayed a precision score of 0.75. This implies that 75% of songs classified as "low" popularity were accurate predictions.
- **Recall (0.65)**: The recall for the "low" category is 0.65, indicating that the model correctly identified 65% of actual "low" popularity songs.
- **F1-Score (0.70)**: The F1-score for the "low" category is 0.70, demonstrating a reasonable balance between precision and recall.

Medium Popularity Category
- **Precision (0.70)**: For the "medium" popularity category, the model achieved a precision score of 0.70. This implies that 70% of the songs predicted as "medium" popularity were accurate.
- **Recall (0.75)**: The recall score for the "medium" category is 0.75, indicating that the model correctly identified 75% of actual "medium" popularity songs.
- **F1-Score (0.73)**: The F1-score for the "medium" category is 0.73, representing a reasonable balance between precision and recall.

Model Accuracy and Summary
- **Accuracy (0.80)**: The overall model accuracy, calculated as the ratio of correct predictions to the total number of predictions, is 0.80. This suggests that our model accurately classified 80% of songs into their respective popularity categories.

</details>

Additionally, the choice of clustering algorithm and feature set may impact the results, and sensitivity to these choices should be considered in further research.

<!-- Tables showing the results of your experiments -->

#### Discussion

The clustering results provide valuable insights into the inherent structure of the Spotify dataset based on audio features. The identification of clusters can have several implications:

1. **Music Recommendation**: Clustering can be used to enhance music recommendation systems by grouping songs with similar audio profiles. This could lead to more accurate and diverse song recommendations for users.

2. **Playlist Generation**: Clusters can be used to create playlists that offer a diverse mix of songs. Songs within the same cluster might complement each other, resulting in more enjoyable listening experiences.

3. **Music Genre Identification**: Clusters could potentially represent different music genres or sub-genres. This unsupervised approach can serve as a complementary method to existing genre classification techniques.

<!-- A brief discussion on the results of your experiment -->

### Decision Trees
Notebooks:
[Model: Decision Tree Classifier](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/models/Decision%20Tree/Decision_Tree_Model.ipynb)


#### Experimental design

The model of DecisionTree will be useful to classify the popularity of our dataset based on audio features of Spotify's songs as according to literature this model provide good performance. To carry out this model, it has been applied the next steps. 

1. **Data Preparation**: Firsly, it was neccesary to select the most relevant audio features to be considered in the training dataset. In this sense, using the technique of Recursive Feature Elimination staying like the most significant the followings: acousticness', 'liveness', 'loudness' and 'valence'. Moreover, the original dataset encompasses unbalanced data, therefore, it has to be applied specific techniques to achieve a balanced dataset to equilibrate the minority classes using the next methods: SMOTE(previously explained), SMOTETomek and RandomOverSample. These two lasts help to resample the unbalanced dataset.  

2. **Feature Scaling**: It is important to scale the information of the dataset to improve the performance of the model. To perform this, it was applied the standard, min-max and robust scaler methods. Adittionally, it was also considered the original data without feature scaling just for compairing the impact on it. As, it can see the original dataset is unbalanced and it may provoke low values in metrics of recall and F1

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/Original_dataset.png" 
alt="Distribution plots" width="500" height="350">
</p>  

3. **Decision Tree Model**: This dataset (Spotify's songs) has unbalanced classes due to there is a majority class ('Low') y two others minitority class ('Medium' and 'High'). So, to address the condition of the dataset, it has been applied the model DecisionTreeClassifier considering different approaches in order to find the best evaluator. As first step, it necessary to balance the dataset applying resample techniques such as, SMOTE, SMOTETomek (SMK) and RandomOverSampler (ROS). As it can appreciate in the imabe below, with the resampled dataset it is better to apply algorithms for classifying.
   
<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/resampled_data.png" 
alt="Distribution plots" width="500" height="350">
</p>  
 Finally, we have considered a **ensemble method** called **Random Forest** which is based on the multiple decision tree.

4. **Final Aspects**: For every approach detailed in the model, it has been considered a variety of paramters in order to evaluate the model that provides the best performance for the dataset.   

#### Results

**1.** Feature scaling is important to improve the performance of the model; however, it has been demonstrated that there is no sensitive in DecisionTree model applying standardization method as their accuracy got in training dataset are almost similar with a gap of 2.1% (maximum gap) as much as test dataset. In the image below, for every resample technique (SMOTE, SMK and ROS) with different scaling methods there is hardly any gap in the accuracy among itself. Therefore, it allows to claim either unscaled the training dataset or with application, the results on the accuracy would be almost similar. 

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/Feature_Scaling_Decision_Tree.png" alt="Distribution plots" width="800" height="350">
</p>

In this scenery, the RandomOverSample (ROS) technique provides the best accuracy; however, it tends to overfit the result of the dataset lacking of flexibility. Therefore, a model which provides better generalisation would be SMK; in other words, the selected resample technique is SMOTETomek with the method of Robust Scaler to improve the performance of the model. 

**2.** As second approach, it has been applied the DecisionTreeClassifier considering the dataset already resampled with the technique SMK and modifying the parameter "class_weight" of the model. It was taken a range from 1 to 80 to assess the best depth of the model also, achieving identify in which depth is presented the lowest error in test, then the class_weight is considered according to level of disproportion in the dataset between the majority class and its minority classes. 
Weight for Class ('Medium') : 29.77
Weight for Class ('High') : 1101

<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/DT_class_weight.png" 
alt="Distribution plots" width="500" height="350">
</p>

According to the image above, it appreciates that test error converges since max_depth = 50. To sum up this point, the table below shows the performance of this model with an accuracy of 90%. Additionally, other metrics such as precision and recall show high values for every class. 
|   | Precision | Recall | F1-Score | Support  |
|---|-----------|--------|----------|----------|
| Low   | 0.86 | 0.84 | 0.85 | 86,165 |
| Medium| 0.85 | 0.86 | 0.86 | 86,772 |
| High  | 0.98 | 0.99 | 0.99 | 87,103 |
|---|-----------|--------|----------|----------|
| Accuracy |     |       | 0.90     | 260,040 |
| Macro Avg| 0.90| 0.90  | 0.90     | 260,040 |
| Weighted Avg| 0.90 | 0.90 | 0.90  | 260,040 |

<details>
  <summary> *Confussion Matrix for Decision Tree modifying class_weights:</summary>
<p align="center">
  <img src="https://github.com/dmml-heriot-watt/group-coursework-machine-learners/raw/main/assets/Confusion Matrix _ DT_weight_class.png" 
alt="Distribution plots" width="500" height="350">
</p>  

</details>

**3.** The last approach is based on the application of ensemble method called random forest. This method comprises different decision tree and at the same time with feature randomness (subspace sampling). Thus, we get a robust model to make realible predictions. For this application it has taken into account the result of resampled technique (SMK) on the dataset. Definitely, this approach aims to the highest accuracy with an adequate sensibility in the prediction achieving a powerful model. 



#### Discussion
1) It is clear that combination between the RandomOverSample technique and the feature scaling of Robust Scaler providing the better accuracy (very near 1) is not the better option due to it is overfitting the design of the model. So, taking into account this aspect, the best selected model will be considering SMOTETomek technique and robust scaler as feature scaling as they, in conjunction, offer more flexibility to evaluate whatever input.
  #### Classification Report (SMOTETomek)
|   | Precision | Recall | F1-Score | Support  |
|---|-----------|--------|----------|----------|
| Low   | 0.86 | 0.82 | 0.84 | 86,146 |
| Medium| 0.84 | 0.87 | 0.86 | 86,332 |
| High  | 0.98 | 0.99 | 0.99 | 87,566 |
|---|-----------|--------|----------|----------|
| Accuracy |     |       | 0.90     | 392,650 |
| Macro Avg| 0.89| 0.89  | 0.89     | 392,650 |
| Weighted Avg| 0.90 | 0.90 | 0.90  | 392,650 |

<details>
  <summary> *Classification report for SMOTE and ROS:</summary>
  
As part of the research, it has the classification report using the other resample techniques.
  
     #### Classification Report (SMOTE)
|   | Precision | Recall | F1-Score | Support  |
|---|-----------|--------|----------|----------|
| Low   | 0.85 | 0.82 | 0.84 | 87,002 |
| Medium| 0.84 | 0.86 | 0.85 | 87,510 |
| High  | 0.98 | 0.99 | 0.99 | 87,255 |
|---|-----------|--------|----------|----------|
| Accuracy |     |       | 0.89     | 261,767 |
| Macro Avg| 0.89| 0.89  | 0.89     | 261,767 |
| Weighted Avg| 0.90 | 0.90 | 0.89  | 261,767 |

     #### Classification Report (ROS)
|   | Precision | Recall | F1-Score | Support  |
|---|-----------|--------|----------|----------|
| Low   | 0.99 | 0.92 | 0.95 | 87,002 |
| Medium| 0.93 | 0.99 | 0.96 | 87,510 |
| High  | 1.08 | 1.00 | 1.00 | 87,255 |
|---|-----------|--------|----------|----------|
| Accuracy |     |       | 0.97     | 261,767 |
| Macro Avg| 0.97| 0.97  | 0.97     | 261,767 |
| Weighted Avg| 0.97 | 0.97 | 0.97  | 261,767 |

</details>

  The accuracy is 90%, therefore we can claim the model has a good performance including similar precision values for every class. That is why the training dataset was resampled to avoid low precision for minority class like "MEDIUM" or "HIGH". In addition, the F1-score value with since 84% indicates that there is a good balance among the data and the obtained marks as Precision as Recall.

2) It is reliable to use the model of Decision Tree as classifier on this dataset as it allows to get best performance and also, the selected features such as acousticness', 'liveness', 'loudness' and 'valence' have contributed greatly to the performance being sufficient to get proper marks. So, for feature assessments, since the relevant audio features which has been mentioned, it will be neccesary just to predict the popularity of them.

3) According to the results, the random forest method is the best model basing on several decision tree as it provides the best accuracy and sensibility without overfitting the results. Although, it is well-known the random forest method is sufficiently robust to work with unbalanced data, the coefficient of the class give an idea of how much severe is this proportion regarding to majority class. That contribution of having a good proportion comes from the previous consideration of working with resampled dataset (technique: SMK).
    
   
### Neural Networks

#### Experimental design

 The application of Neural Networks for classifying the popularity of songs in the dataset involves the following inital steps:

 1. Data Loading: Loaded the integrated dataset containing audio features and populairty labels of the songs.

 2. Image Extraction: Extracted spectrogram images for each track using the provided 'preview_url' and linked the images to the dataset.

 3. Popularity Binning: The 'popularity' column was binned into three categories: low, medium, and high.

 4. Data Sampling: Sampled 10,000 values from the dataset, ensuring each entry is associated with a sprectogram image. 

#### Analyzing Spectrograms

 Spectrograms serve as a powerful tool for converting the audio features of songs into visual representations. Understanding the nuances of spectrogram images is crucial for comprehending how the neural network interprets and learns from these representations.

 1. Frequency Analysis:

      Spectrograms represent the distribution of frequencies in an audio signal. The horizontal axis represents time and the vertical axis represents frequency. The color intensity represents the magnitude of the frequencies. Darker areas indicate more intense frequencies while lighter areas indicate less intense frequencies.

 2. Patterns:

      Changes in color intensity in the spectrogram represents patterns within the audio signal. For instance, distinct patterns may represent beats, tempo, or other features in the song. The network can learn to associate these patterns with different levels of popularity.

 3. Feature Extraction:

      Spectrogram images capture essential features of the audio, such as music keys, instrumentalness, or vocal patterns. The neural network uses these features to make predictions about the popularity of songs.

 Sample Spectrogram Images:

![Untitled-3-2](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/assets/89276533/b8a082d8-2546-4d98-b906-bc320957bdd1)

 In these samples, we can clearly identify the following aspects:

 1. Distinct Patterns: This indicates the varying musical elements.
 2. Intensity Variations: This indicates the changes in the audio signal.
 3. Time-Frequency Relationship: This indicates how the frequency changes over the course of song's duration.

 The neural network processes these spectrogram images to identify intricate features such as the presence of certain instruments, the complexity of the audio, or the density of frequency content.


#### Neural Network Architecture

 The Neural Network Architecture is a critical aspect of the experiment, outlining the structure and layers of the Convolutional Neural Network (CNN). It is defined using Keras Sequential Model.

 1. Input Layer:
 
      The input layer accepts the spectrogram images derived from the audio features and serves as the entry point of the neural network. 

 2. Convolutional Layer:

      This layer acts as the backbone of the neural network. In our model, convolutional layer is applied to filter the input images to extract relevant features. The choice of 32 filters of size(3,3) is common in image processing tasks. It provides the network with abilty to get 32 feature maps. The choice of using ReLU function was based on that it helps the model learn complex patterns within the images. 

 3. MaxPooling Layer:

      Following the convolutional layer, Maxpooling layer is applied to reduce the complexity of data. This layer uses a size of (2,2) which reduces the quantity of pixels in the images.

 4. Flattening Layer:

      This layer transforms the 2D array obtained from the previous layer into 1D array. This prepares the data for the subsequent dense layers.

 5. Dense Layers:

      These layers are fully-connected layers used to process the flattened data to learn high-level representations. In our model, 64 dense layers are applied with ReLU activation function. This facilitated the network to read more complex patterns in the data.

 6. Dropout Layer: 

      A Dropout Layer with a dropout rate of 0.5 is applied to prevent overfitting. Therefore, it randomly drops out 50% of the neurons during trainning. This regularization technique enhances the model's ability to generalize the unseen data.

 7. Output Layer:

      The final layer consists of three neurons, each representing a popularity category (Low, Medium, or High). The softmax activation function is applied to obtain a probaility distribution across these categories.


#### Results

 Trainning Performance:

 The neural network was trainned over 10 epochs on the sampled dataset and the results are summarized below:

 1. The model quickly achieved a high trainning accuracy of approximately 96%. 
 2. Training loss had a steady decline.
 3. Validation loss maintained stability

 Testing Performance:

 The trained neural network was evaluated on the test set, and the following results were obtained:

 1. The test accuracy was 96.35%
 2. This confirmed the model's capability to classify song popularity based on spectrogram images.

![Untitled-4-2](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/assets/89276533/484ceba1-8ba4-4785-9999-25269a13f5ed)

#### Discussion

 Model Performance:

 The achieved test accuracy of 96.35% reflects the model's efficiency in classifying songs into their respective popularity categories. This high accuracy suggests that the neural network can effectively learn and generalize patterns from spectrogram images.

 Quick Convergence:

 The model quickly converges during the initial epochs, indicating efficient learning from the training data. This quick convergence is a positive aspect, especially considering the large dataset and complex image features.

 Stable Trainning Performance:

 The stability of the training accuracy throughout the epochs indicated the model's ability to consistently learn and adapt. This makes the neural network architecture robust.

 Generalization to Unseen Data:

 The model's ability to maintain a high level of accuracy on the test set implies successful generalization to previously unseen data. This affirms the model's potentiality for real-world applications.


### Conclusion
<!-- Final conclusions regarding your initial objectives -->
