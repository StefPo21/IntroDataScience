Data Practical 3
================
Stefano Politi
(20 juin 2022)

-   [External Data](#external-data)
    -   [Importing Data](#importing-data)
    -   [Filtering Data](#filtering-data)
    -   [Structuring Data](#structuring-data)
    -   [Summarizing data](#summarizing-data)
    -   [Removing NAs](#removing-nas)
-   [R Pre-loaded Data](#r-pre-loaded-data)
    -   [Joining data](#joining-data)
-   [References](#references)

``` r
library(dslabs)
library(readxl)
library(knitr)
library(dplyr)
```

## External Data

### Importing Data

The following dataset is described
[here](https://github.com/StefPo21/IntroDataScience/tree/main/3_data/2_Data.md#Importing-External-Data)
(Dataset 2).

``` r
GEMMES <- read_xlsx("Exp2A-GEMMES_Binomial.xlsx", sheet = 1)
```

### Filtering Data

The dataset contains multiple copies for each participant. For the
purpose of this practice, the duplicates will be removed.

``` r
GEMMES_clean <- GEMMES %>%
  select(-VISU, -VISU_Value, -VISU_Binomial)
GEMMES_clean <- unique(GEMMES_clean)
kable(head(GEMMES_clean, 10))
```

| Participant_ID    | Sex | Age | Musician_type | Excerpt_id               | Excerpt_GEMS     | feat_ENT_Agitated | feat_ENT_Animated | feat_ENT_Beat | feat_ENT_Dance | feat_ENT_Entrained | feat_ENT_Move | feat_ENT_PCvic | feat_ENT_Pcmot | feat_ENT_Physio | feat_ENT_Resonate | feat_ENT_Rhythm | feat_KNOW | feat_PC1 | feat_PC2 | feat_PC3 | feat_PC4 | feat_PC_ENT | feat_articulation | feat_atonality | feat_dissonance | feat_melody | feat_mode | feat_rhythm_complexity | feat_rhythm_stability | feat_norm_ENT_Agitated | feat_norm_ENT_Animated | feat_norm_ENT_Beat | feat_norm_ENT_Dance | feat_norm_ENT_Entrained | feat_norm_ENT_Move | feat_norm_ENT_PCvic | feat_norm_ENT_Pcmot | feat_norm_ENT_Physio | feat_norm_ENT_Resonate | feat_norm_ENT_Rhythm | feat_norm_KNOW | feat_norm_PC1 | feat_norm_PC2 | feat_norm_PC3 | feat_norm_PC4 | feat_norm_PC_ENT | feat_norm_articulation | feat_norm_atonality | feat_norm_dissonance | feat_norm_melody | feat_norm_mode | feat_norm_rhythm_complexity | feat_norm_rhythm_stability | feat_norm_fact_ENT_Agitated | feat_norm_fact_ENT_Animated | feat_norm_fact_ENT_Beat | feat_norm_fact_ENT_Dance | feat_norm_fact_ENT_Entrained | feat_norm_fact_ENT_Move | feat_norm_fact_ENT_PCvic | feat_norm_fact_ENT_Pcmot | feat_norm_fact_ENT_Physio | feat_norm_fact_ENT_Resonate | feat_norm_fact_ENT_Rhythm | feat_norm_fact_KNOW | feat_norm_fact_PC1 | feat_norm_fact_PC2 | feat_norm_fact_PC3 | feat_norm_fact_PC4 | feat_norm_fact_PC_ENT | feat_norm_fact_articulation | feat_norm_fact_atonality | feat_norm_fact_dissonance | feat_norm_fact_melody | feat_norm_fact_mode | feat_norm_fact_rhythm_complexity | feat_norm_fact_rhythm_stability | BEST_GEMS             | GEMS_JoyfulActivation | GEMS_Nostalgia | GEMS_Peacefulness | GEMS_Power | GEMS_Sadness | GEMS_Tenderness | GEMS_Tension | GEMS_Transcendence | GEMS_Wonder | BEST_VA    | VA_Arousal | VA_Valence | BEST_VISU     | VISU_Flow | VISU_Force | VISU_Interior | VISU_Movement | VISU_Wandering |
|:------------------|:----|----:|--------------:|:-------------------------|:-----------------|------------------:|------------------:|--------------:|---------------:|-------------------:|--------------:|---------------:|---------------:|----------------:|------------------:|----------------:|----------:|---------:|---------:|---------:|---------:|------------:|------------------:|---------------:|----------------:|------------:|----------:|-----------------------:|----------------------:|-----------------------:|-----------------------:|-------------------:|--------------------:|------------------------:|-------------------:|--------------------:|--------------------:|---------------------:|-----------------------:|---------------------:|---------------:|--------------:|--------------:|--------------:|--------------:|-----------------:|-----------------------:|--------------------:|---------------------:|-----------------:|---------------:|----------------------------:|---------------------------:|:----------------------------|:----------------------------|:------------------------|:-------------------------|:-----------------------------|:------------------------|:-------------------------|:-------------------------|:--------------------------|:----------------------------|:--------------------------|:--------------------|:-------------------|:-------------------|:-------------------|:-------------------|:----------------------|:----------------------------|:-------------------------|:--------------------------|:----------------------|:--------------------|:---------------------------------|:--------------------------------|:----------------------|----------------------:|---------------:|------------------:|-----------:|-------------:|----------------:|-------------:|-------------------:|------------:|:-----------|-----------:|-----------:|:--------------|----------:|-----------:|--------------:|--------------:|---------------:|
| R_10q7ugZebPq8d4x | M   |  28 |             3 | bach_brandenburgconcerto | Sadness          |            1.5000 |            2.2250 |        1.3375 |         1.0625 |             1.1500 |        1.1250 |       1.661875 |      0.8827812 |          2.1625 |            2.9000 |          2.3125 |  1.720497 | -0.36749 | -1.17243 | -1.72126 |  1.01693 |  -1.2484457 |               2.4 |            7.6 |             3.6 |         8.2 |       6.2 |                    4.8 |                   5.4 |              0.1458886 |              0.2269939 |          0.1763285 |           0.2059925 |               0.1574586 |          0.1350575 |           0.1764437 |           0.1771151 |            0.1523810 |              0.2673267 |            0.2436975 |      0.1711538 |     0.5714844 |     0.4090526 |     0.1691048 |     0.6131462 |        0.1822885 |              0.1666667 |                0.70 |            0.2592593 |        0.8333333 |           0.64 |                   0.5294118 |                  0.3666667 | a33                         | a33                         | a33                     | a33                      | a33                          | a33                     | a33                      | a33                      | a33                       | a33                         | a33                       | a33                 | b66                | b66                | a33                | b66                | a33                   | a33                         | c100                     | a33                       | c100                  | b66                 | b66                              | b66                             | GEMS_Nostalgia        |                     8 |             48 |                28 |         14 |           47 |              35 |            7 |                 25 |          26 | VA_Arousal |         48 |         34 | VISU_Flow     |        55 |         22 |            49 |            24 |             27 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | bach_goldberg            | Tenderness       |            1.3250 |            2.3250 |        1.5125 |         1.4375 |             1.4375 |        1.5375 |       1.693850 |      1.1289062 |          2.0250 |            3.0500 |          2.6125 |  1.521739 | -3.96652 | -1.76827 | -0.23215 | -0.08823 |  -1.0380916 |               2.4 |            7.2 |             2.8 |         7.8 |       3.8 |                    4.2 |                   4.2 |              0.1087533 |              0.2515337 |          0.2101449 |           0.3183521 |               0.2209945 |          0.2298851 |           0.1881196 |           0.2588350 |            0.1000000 |              0.3069307 |            0.3109244 |      0.1403846 |     0.2387508 |     0.3394752 |     0.3476164 |     0.4642383 |        0.2267283 |              0.1666667 |                0.60 |            0.1111111 |        0.7500000 |           0.16 |                   0.3529412 |                  0.1666667 | a33                         | a33                         | a33                     | a33                      | a33                          | a33                     | a33                      | a33                      | a33                       | a33                         | a33                       | a33                 | a33                | b66                | b66                | b66                | a33                   | a33                         | b66                      | a33                       | c100                  | a33                 | b66                              | a33                             | GEMS_Tenderness       |                    29 |             52 |                61 |          3 |           25 |              63 |            0 |                 20 |          41 | VA_Valence |         47 |         69 | VISU_Flow     |        63 |         12 |            43 |            26 |             29 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | bach_passacaglia         | Power            |            2.4250 |            2.3250 |        0.9125 |         0.4625 |             1.0625 |        1.0375 |       2.009750 |      0.6552813 |          2.7500 |            3.4750 |          2.4125 |  1.763975 | -0.76462 | -2.38908 |  0.55701 |  3.88807 |  -1.1029243 |               1.4 |            5.2 |             5.2 |         5.0 |       5.8 |                    4.0 |                   4.6 |              0.3421751 |              0.2515337 |          0.0942029 |           0.0262172 |               0.1381215 |          0.1149425 |           0.3034726 |           0.1015792 |            0.3761905 |              0.4191419 |            0.2661064 |      0.1778846 |     0.5347694 |     0.2669819 |     0.4422194 |     1.0000000 |        0.2130316 |              0.0000000 |                0.10 |            0.5555556 |        0.1666667 |           0.56 |                   0.2941176 |                  0.2333333 | b66                         | a33                         | a33                     | a33                      | a33                          | a33                     | a33                      | a33                      | b66                       | b66                         | a33                       | a33                 | b66                | a33                | b66                | c100               | a33                   | a33                         | a33                      | b66                       | a33                   | b66                 | a33                              | a33                             | GEMS_Power            |                     3 |             22 |                 9 |         59 |           44 |               1 |           25 |                 36 |           5 | VA_Arousal |         61 |         13 | VISU_Force    |        15 |         66 |            44 |             9 |             11 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | bach_prelude19inamajor   | Peacefulness     |            1.6500 |            2.5500 |        1.9250 |         1.7625 |             1.7875 |        1.6625 |       1.671875 |      1.3531250 |          1.9500 |            2.6625 |          2.4625 |  1.403727 | -6.54898 |  0.61909 |  2.17336 |  0.04202 |  -0.8780754 |               2.6 |            6.4 |             3.8 |         7.0 |       3.4 |                    5.0 |                   5.2 |              0.1777188 |              0.3067485 |          0.2898551 |           0.4157303 |               0.2983425 |          0.2586207 |           0.1800953 |           0.3332815 |            0.0714286 |              0.2046205 |            0.2773109 |      0.1221154 |     0.0000000 |     0.6182522 |     0.6359843 |     0.4817880 |        0.2605336 |              0.2000000 |                0.40 |            0.2962963 |        0.5833333 |           0.08 |                   0.5882353 |                  0.3333333 | a33                         | a33                         | a33                     | b66                      | a33                          | a33                     | a33                      | b66                      | a33                       | a33                         | a33                       | a33                 | a33                | b66                | b66                | b66                | a33                   | a33                         | b66                      | a33                       | b66                   | a33                 | b66                              | b66                             | GEMS_Tenderness       |                    29 |             48 |                57 |          6 |           17 |              60 |            3 |                 17 |          34 | VA_Valence |         36 |         67 | VISU_Flow     |        60 |         10 |            34 |            19 |             34 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | bach_preludeincminor     | Tension          |            4.2875 |            4.4375 |        3.6375 |         2.1000 |             3.4500 |        4.0125 |       2.968775 |      2.4947812 |          2.9500 |            4.3000 |          4.2375 |  2.416149 | -6.38467 |  2.43520 |  0.60942 | -1.42618 |   1.2080483 |               6.0 |            6.8 |             3.8 |         4.2 |       5.8 |                    3.4 |                   5.4 |              0.7374005 |              0.7699386 |          0.6207729 |           0.5168539 |               0.6657459 |          0.7988506 |           0.6536671 |           0.7123410 |            0.4523810 |              0.6369637 |            0.6750700 |      0.2788462 |     0.0151906 |     0.8303231 |     0.4485022 |     0.2839646 |        0.7012522 |              0.7666667 |                0.50 |            0.2962963 |        0.0000000 |           0.56 |                   0.1176471 |                  0.3666667 | c100                        | c100                        | b66                     | b66                      | c100                         | c100                    | b66                      | c100                     | b66                       | b66                         | c100                      | a33                 | a33                | c100               | b66                | a33                | c100                  | c100                        | b66                      | a33                       | a33                   | b66                 | a33                              | b66                             | GEMS_Tension          |                    39 |             25 |                 7 |         49 |           14 |              15 |           50 |                 27 |          31 | VA_Valence |         52 |         57 | VISU_Movement |        22 |         56 |            27 |            65 |             45 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | bach_preludio            | JoyfulActivation |            3.9875 |            4.3500 |        3.3375 |         2.4875 |             4.1500 |        4.0000 |       2.872275 |      2.6557812 |          2.7875 |            4.2125 |          4.2250 |  2.521739 |  1.02015 |  1.12237 |  0.37829 | -1.12309 |   1.2301380 |               6.2 |            8.8 |             3.6 |         6.8 |       3.8 |                    4.4 |                   5.2 |              0.6737401 |              0.7484663 |          0.5628019 |           0.6329588 |               0.8204420 |          0.7959770 |           0.6184295 |           0.7657972 |            0.3904762 |              0.6138614 |            0.6722689 |      0.2951923 |     0.6997730 |     0.6770212 |     0.4207948 |     0.3248026 |        0.7059190 |              0.8000000 |                1.00 |            0.2592593 |        0.5416667 |           0.16 |                   0.4117647 |                  0.3333333 | c100                        | c100                        | b66                     | b66                      | c100                         | c100                    | b66                      | c100                     | b66                       | b66                         | c100                      | a33                 | c100               | c100               | b66                | a33                | c100                  | c100                        | c100                     | a33                       | b66                   | a33                 | b66                              | b66                             | GEMS_JoyfulActivation |                    65 |              9 |                17 |         38 |            2 |              15 |           46 |                 21 |          57 | VA_Valence |         61 |         77 | VISU_Movement |        24 |         45 |            13 |            65 |             42 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | beethoven_violindmajor   | Wonder           |            4.1000 |            4.7250 |        4.6625 |         3.4750 |             4.8625 |        4.7500 |       3.070975 |      3.3611562 |          3.0250 |            4.2375 |          4.8625 |  2.211180 |  1.30413 |  3.85298 | -2.79566 | -0.54899 |   1.9349691 |               5.8 |            6.8 |             3.4 |         7.4 |       3.4 |                    4.8 |                   5.8 |              0.6976127 |              0.8404908 |          0.8188406 |           0.9288390 |               0.9779006 |          0.9683908 |           0.6909861 |           1.0000000 |            0.4809524 |              0.6204620 |            0.8151261 |      0.2471154 |     0.7260272 |     0.9958803 |     0.0403078 |     0.4021561 |        0.8548230 |              0.7333333 |                0.50 |            0.2222222 |        0.6666667 |           0.08 |                   0.5294118 |                  0.4333333 | c100                        | c100                        | c100                    | c100                     | c100                         | c100                    | c100                     | c100                     | b66                       | b66                         | c100                      | a33                 | c100               | c100               | a33                | b66                | c100                  | c100                        | b66                      | a33                       | c100                  | a33                 | b66                              | b66                             | GEMS_Power            |                    57 |              6 |                10 |         69 |            1 |               9 |           57 |                 34 |          51 | VA_Valence |         68 |         75 | VISU_Movement |        33 |         63 |            12 |            70 |             54 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | bruch_violin1gminor      | Wonder           |            4.2375 |            4.8250 |        4.4125 |         3.1875 |             4.8625 |        4.5500 |       3.213575 |      3.2194062 |          3.4250 |            4.5750 |          4.7750 |  4.118012 |  1.24479 |  2.66567 | -2.35112 |  0.55244 |   1.9482020 |               5.6 |            6.8 |             3.8 |         6.0 |       3.6 |                    4.4 |                   5.0 |              0.7267905 |              0.8650307 |          0.7705314 |           0.8426966 |               0.9779006 |          0.9224138 |           0.7430575 |           0.9529353 |            0.6333333 |              0.7095710 |            0.7955182 |      0.5423077 |     0.7205412 |     0.8572356 |     0.0935984 |     0.5505614 |        0.8576186 |              0.7000000 |                0.50 |            0.2962963 |        0.3750000 |           0.12 |                   0.4117647 |                  0.3000000 | c100                        | c100                        | c100                    | c100                     | c100                         | c100                    | c100                     | c100                     | b66                       | c100                        | c100                      | b66                 | c100               | c100               | a33                | b66                | c100                  | c100                        | b66                      | a33                       | b66                   | a33                 | b66                              | a33                             | GEMS_Power            |                    28 |             54 |                24 |         61 |           31 |              39 |           25 |                 35 |          56 | VA_Arousal |         78 |         62 | VISU_Movement |        23 |         68 |            16 |            70 |             54 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | buxtehude_allegro        | JoyfulActivation |            3.1500 |            3.7500 |        3.7375 |         3.3875 |             4.0500 |        4.0500 |       2.343125 |      2.8997813 |          2.1875 |            3.2750 |          3.6500 |  1.658385 |  2.79275 |  0.99199 | -1.14172 | -1.73163 |   0.9080550 |               5.0 |            6.8 |             3.4 |         7.2 |       3.4 |                    6.0 |                   6.6 |              0.4960212 |              0.6012270 |          0.6400966 |           0.9026217 |               0.7983425 |          0.8074713 |           0.4252068 |           0.8468115 |            0.1619048 |              0.3663366 |            0.5434174 |      0.1615385 |     0.8636515 |     0.6617965 |     0.2385789 |     0.2428087 |        0.6378751 |              0.6000000 |                0.50 |            0.2222222 |        0.6250000 |           0.08 |                   0.8823529 |                  0.5666667 | b66                         | b66                         | b66                     | c100                     | c100                         | c100                    | b66                      | c100                     | a33                       | b66                         | b66                       | a33                 | c100               | c100               | a33                | a33                | b66                   | b66                         | b66                      | a33                       | b66                   | a33                 | c100                             | b66                             | GEMS_JoyfulActivation |                    67 |              8 |                21 |         21 |            3 |              23 |           20 |                 11 |          55 | VA_Valence |         45 |         71 | VISU_Movement |        26 |         28 |            16 |            58 |             43 |
| R_10q7ugZebPq8d4x | M   |  28 |             3 | geminiani_adagio         | Nostalgia        |            1.5500 |            2.4875 |        1.5000 |         1.4500 |             1.5625 |        1.7500 |       1.749150 |      1.1973125 |          1.9375 |            3.1375 |          2.6375 |  1.763975 |  3.10183 | -2.95625 |  0.28141 |  1.23641 |  -0.9285856 |               2.0 |            7.0 |             2.2 |         9.0 |       6.2 |                    3.0 |                   6.4 |              0.1564987 |              0.2914110 |          0.2077295 |           0.3220974 |               0.2486188 |          0.2787356 |           0.2083128 |           0.2815477 |            0.0666667 |              0.3300330 |            0.3165266 |      0.1778846 |     0.8922263 |     0.2007522 |     0.4091810 |     0.6427187 |        0.2498628 |              0.1000000 |                0.55 |            0.0000000 |        1.0000000 |           0.64 |                   0.0000000 |                  0.5333333 | a33                         | a33                         | a33                     | a33                      | a33                          | a33                     | a33                      | a33                      | a33                       | b66                         | a33                       | a33                 | c100               | a33                | b66                | b66                | a33                   | a33                         | b66                      | a33                       | c100                  | b66                 | a33                              | b66                             | GEMS_Nostalgia        |                    14 |             54 |                37 |         16 |           35 |              37 |            5 |                 24 |          29 | VA_Valence |         46 |         49 | VISU_Flow     |        48 |         19 |            41 |            32 |             25 |

Here the focus will be exclusively on the music excerpts associated to
GEMS emotions of “Power” and “Tension” and on their respective highest
participant ratings for GEMS, VA and GEMMES.

``` r
GEMMES2 <- GEMMES_clean %>%
  filter(Excerpt_GEMS %in% c("Power", "Tension")) %>%
  select(Participant_ID, Excerpt_GEMS, BEST_GEMS, BEST_VA, BEST_VISU)
kable(head(GEMMES2, 10))
```

| Participant_ID    | Excerpt_GEMS | BEST_GEMS    | BEST_VA    | BEST_VISU     |
|:------------------|:-------------|:-------------|:-----------|:--------------|
| R_10q7ugZebPq8d4x | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_10q7ugZebPq8d4x | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_10q7ugZebPq8d4x | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_10q7ugZebPq8d4x | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_114PdEdPKywn259 | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_114PdEdPKywn259 | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_114PdEdPKywn259 | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_114PdEdPKywn259 | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_12ydg3AdKtciy0m | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_12ydg3AdKtciy0m | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |

``` r
kable(tail(GEMMES2, 10))
```

| Participant_ID    | Excerpt_GEMS | BEST_GEMS    | BEST_VA    | BEST_VISU     |
|:------------------|:-------------|:-------------|:-----------|:--------------|
| R_pz34kCAcgieWqNX | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_pz34kCAcgieWqNX | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_vZvN6Uzp9xd6ZgZ | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_vZvN6Uzp9xd6ZgZ | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_vZvN6Uzp9xd6ZgZ | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_vZvN6Uzp9xd6ZgZ | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_yKj22r0Qp02Mayd | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |
| R_yKj22r0Qp02Mayd | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_yKj22r0Qp02Mayd | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_yKj22r0Qp02Mayd | Power        | GEMS_Power   | VA_Arousal | VISU_Force    |

### Structuring Data

The structure of the filtered dataset shows 1 600 observation of 4
variables.

The variables are listed here with their respective data types:

-   BEST_GEMS: character variable (qualitative, categorical) indicating
    the GEMS emotion with the highest rating for each participant.
-   BEST_VA: character variable (qualitative, categorical) indicating
    highest rating of either valence or arousal for each participant.
-   BEST_VISU: character variable (qualitative, categorical) indicating
    the GEMMES metaphor with the highest rating for each participant.

``` r
str(GEMMES2)
```

    ## tibble [320 × 5] (S3: tbl_df/tbl/data.frame)
    ##  $ Participant_ID: chr [1:320] "R_10q7ugZebPq8d4x" "R_10q7ugZebPq8d4x" "R_10q7ugZebPq8d4x" "R_10q7ugZebPq8d4x" ...
    ##  $ Excerpt_GEMS  : chr [1:320] "Power" "Tension" "Tension" "Power" ...
    ##  $ BEST_GEMS     : chr [1:320] "GEMS_Power" "GEMS_Tension" "GEMS_Tension" "GEMS_Power" ...
    ##  $ BEST_VA       : chr [1:320] "VA_Arousal" "VA_Valence" "VA_Arousal" "VA_Arousal" ...
    ##  $ BEST_VISU     : chr [1:320] "VISU_Force" "VISU_Movement" "VISU_Force" "VISU_Force" ...

When ordering the data by the GEMS emotion to which each music excerpt
is associated, there seems to be a strong correlation with the
participant’s ratings.

``` r
GEMMES2 <- GEMMES2 %>%
  arrange(Excerpt_GEMS)
kable(head(GEMMES2, 20))
```

| Participant_ID    | Excerpt_GEMS | BEST_GEMS  | BEST_VA    | BEST_VISU  |
|:------------------|:-------------|:-----------|:-----------|:-----------|
| R_10q7ugZebPq8d4x | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_10q7ugZebPq8d4x | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_114PdEdPKywn259 | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_114PdEdPKywn259 | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_12ydg3AdKtciy0m | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_12ydg3AdKtciy0m | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1F9RF9PbduE06R2 | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1F9RF9PbduE06R2 | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1JDYMlmhePPFO3I | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1JDYMlmhePPFO3I | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1JJSpPDbw7NRBbP | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1JJSpPDbw7NRBbP | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1MJT0JEKjvV631o | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1MJT0JEKjvV631o | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1N8wvygRcQHT5y9 | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1N8wvygRcQHT5y9 | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1Ov6eSlBZNipCuw | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1Ov6eSlBZNipCuw | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1Q9fMwwKkH5lsar | Power        | GEMS_Power | VA_Arousal | VISU_Force |
| R_1Q9fMwwKkH5lsar | Power        | GEMS_Power | VA_Arousal | VISU_Force |

``` r
kable(tail(GEMMES2, 20))
```

| Participant_ID    | Excerpt_GEMS | BEST_GEMS    | BEST_VA    | BEST_VISU     |
|:------------------|:-------------|:-------------|:-----------|:--------------|
| R_WdRdPjxhqvB7Y8V | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_WdRdPjxhqvB7Y8V | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_XpKNFDse3fruONb | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_XpKNFDse3fruONb | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_Xq5CFWYR1M2gXFn | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_Xq5CFWYR1M2gXFn | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_Zz38Dzo6xIcTCZH | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_Zz38Dzo6xIcTCZH | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_bxx8twDjylE54at | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_bxx8twDjylE54at | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_cCIwD6nyh5pN9Lz | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_cCIwD6nyh5pN9Lz | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_dnxb67c1jnKXuLf | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_dnxb67c1jnKXuLf | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_pz34kCAcgieWqNX | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_pz34kCAcgieWqNX | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_vZvN6Uzp9xd6ZgZ | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_vZvN6Uzp9xd6ZgZ | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |
| R_yKj22r0Qp02Mayd | Tension      | GEMS_Tension | VA_Valence | VISU_Movement |
| R_yKj22r0Qp02Mayd | Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |

### Summarizing data

To be able to verify this correlation, the data must be grouped and the
occurrences of each rating counted.

The results show indeed a strong correlations:

-   “Power” is 100% correlated with ratings of “Power”, “Arousal” and
    “Force”.
-   “Tension” is 100% correlated with ratings of “Tension”, as well as:
    -   50% correlated with ratings of “Arousal” and “Force.
    -   50% correlated with ratings of “Valence” and “Movement”.

``` r
GEMMES3 <- GEMMES2 %>%
  group_by(Excerpt_GEMS) %>%
  count(BEST_GEMS, BEST_VA, BEST_VISU)
kable(print(GEMMES3))
```

    ## # A tibble: 3 × 5
    ## # Groups:   Excerpt_GEMS [2]
    ##   Excerpt_GEMS BEST_GEMS    BEST_VA    BEST_VISU         n
    ##   <chr>        <chr>        <chr>      <chr>         <int>
    ## 1 Power        GEMS_Power   VA_Arousal VISU_Force      160
    ## 2 Tension      GEMS_Tension VA_Arousal VISU_Force       80
    ## 3 Tension      GEMS_Tension VA_Valence VISU_Movement    80

| Excerpt_GEMS | BEST_GEMS    | BEST_VA    | BEST_VISU     |   n |
|:-------------|:-------------|:-----------|:--------------|----:|
| Power        | GEMS_Power   | VA_Arousal | VISU_Force    | 160 |
| Tension      | GEMS_Tension | VA_Arousal | VISU_Force    |  80 |
| Tension      | GEMS_Tension | VA_Valence | VISU_Movement |  80 |

### Removing NAs

There are no NA values are present in the filtered dataset.

``` r
GEMMES4 <- na.omit(GEMMES2)
str(GEMMES4)
```

    ## tibble [320 × 5] (S3: tbl_df/tbl/data.frame)
    ##  $ Participant_ID: chr [1:320] "R_10q7ugZebPq8d4x" "R_10q7ugZebPq8d4x" "R_114PdEdPKywn259" "R_114PdEdPKywn259" ...
    ##  $ Excerpt_GEMS  : chr [1:320] "Power" "Power" "Power" "Power" ...
    ##  $ BEST_GEMS     : chr [1:320] "GEMS_Power" "GEMS_Power" "GEMS_Power" "GEMS_Power" ...
    ##  $ BEST_VA       : chr [1:320] "VA_Arousal" "VA_Arousal" "VA_Arousal" "VA_Arousal" ...
    ##  $ BEST_VISU     : chr [1:320] "VISU_Force" "VISU_Force" "VISU_Force" "VISU_Force" ...

## R Pre-loaded Data

### Joining data

The
[results_us_election_2016](https://www.rdocumentation.org/packages/dslabs/versions/0.7.4/topics/polls_us_election_2016)
dataset, from the dslabs package, describes the poll results of the US
2016 presidential elections.

``` r
kable(head(results_us_election_2016))
```

| state        | electoral_votes | clinton | trump | others |
|:-------------|----------------:|--------:|------:|-------:|
| California   |              55 |    61.7 |  31.6 |    6.7 |
| Texas        |              38 |    43.2 |  52.2 |    4.5 |
| Florida      |              29 |    47.8 |  49.0 |    3.2 |
| New York     |              29 |    59.0 |  36.5 |    4.5 |
| Illinois     |              20 |    55.8 |  38.8 |    5.4 |
| Pennsylvania |              20 |    47.9 |  48.6 |    3.6 |

The
[murders](https://www.rdocumentation.org/packages/dslabs/versions/0.7.4/topics/murders)
dataset, also from the dslabs package, describes gun murder data from
FBI reports in the US, organized by state.

``` r
kable(head(murders))
```

| state      | abb | region | population | total |
|:-----------|:----|:-------|-----------:|------:|
| Alabama    | AL  | South  |    4779736 |   135 |
| Alaska     | AK  | West   |     710231 |    19 |
| Arizona    | AZ  | West   |    6392017 |   232 |
| Arkansas   | AR  | South  |    2915918 |    93 |
| California | CA  | West   |   37253956 |  1257 |
| Colorado   | CO  | West   |    5029196 |    65 |

Joining the two datasets might be useful to investigate the relationship
between the amount of gun murders in a state and the tendency of its
citizens to vote for either Trump of Clinton.

``` r
joinedData <- full_join(results_us_election_2016, murders)
kable(head(joinedData, 10))
```

| state          | electoral_votes | clinton | trump | others | abb | region        | population | total |
|:---------------|----------------:|--------:|------:|-------:|:----|:--------------|-----------:|------:|
| California     |              55 |    61.7 |  31.6 |    6.7 | CA  | West          |   37253956 |  1257 |
| Texas          |              38 |    43.2 |  52.2 |    4.5 | TX  | South         |   25145561 |   805 |
| Florida        |              29 |    47.8 |  49.0 |    3.2 | FL  | South         |   19687653 |   669 |
| New York       |              29 |    59.0 |  36.5 |    4.5 | NY  | Northeast     |   19378102 |   517 |
| Illinois       |              20 |    55.8 |  38.8 |    5.4 | IL  | North Central |   12830632 |   364 |
| Pennsylvania   |              20 |    47.9 |  48.6 |    3.6 | PA  | Northeast     |   12702379 |   457 |
| Ohio           |              18 |    43.5 |  51.7 |    4.8 | OH  | North Central |   11536504 |   310 |
| Georgia        |              16 |    45.9 |  51.0 |    3.1 | GA  | South         |    9920000 |   376 |
| Michigan       |              16 |    47.3 |  47.5 |    5.2 | MI  | North Central |    9883640 |   413 |
| North Carolina |              15 |    46.2 |  49.8 |    4.0 | NC  | South         |    9535483 |   286 |

## References

Schaerlaeken, S., Glowinski, D., & Grandjean, D. (2022). Linking musical
metaphors and emotions evoked by the sound of classical music.
*Psychology of music*, 50(1), 245-264.
