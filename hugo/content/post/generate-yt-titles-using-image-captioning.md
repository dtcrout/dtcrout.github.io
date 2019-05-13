---
author: Darshan Crout
title: "Generate YouTube Titles Using Image Captioning"
date: 2019-05-11
draft: true
---

I watch a lot of YouTube. In fact a lot of younger people watch more YouTube then they do television. If you're like me, YouTube not only acts as an endless source of entertainment
but it also serves as a source of knowledge and information. The platform has videos on just about anything, from how to make [fermented food](https://www.youtube.com/watch?v=zx8pYMkkKXg),
[cracking the Sega Saturn](https://www.youtube.com/watch?v=jOyfZex7B3E), and [Joe Rogan interviewing himself](https://www.youtube.com/watch?v=-xY_D8SMNtE).
However, if you've been on the platform as long as I have, you have probably realized by now certain patterns in how YouTubers structure their content. For example, content creators engage in
tactics such as using [clickbait](https://en.wikipedia.org/wiki/Clickbait) titles and thumbnails to engage consumers of the platform and to optimize for search engine optimization (SEO).

And so while YouTube acts as a great bastion of information, YouTube's community has developed it's own unique culture and language as a consequence of the pursuit of this SEO.
Motivated bycuriosity, I thought about what it would be like to train a machine learning model based on this unique and strange internet subculture. Using LSTMs and an encoder-decoder model,
I trained an image caption model on YouTube thumbnails and their titles to generate new titles. The code can be found on [GitHub](https://github.com/dtcrout/yt-title-generator).

![They take time!](static/images/koji.png)

## Getting the Data

If we want to get a good representation of what YouTube represents today, we look no further than the trending videos found on its homepage. Doing some searching, I found a Kaggle dataset
which has all trending YouTube videos based on region, e.g. US, Canada, and the UK. There are `40,949 records` in the US dataset. If we want to generate some decent captions,
we will need much more data than that. Below is a breakdown the US, CA and GB datasets:

* US videos: `40,949 records`
* CA videos: `40,881 records`
* GB videos: `38,916 records`

Joining all three datasets and dropping all duplicates, we get a total of `111,394 records` out of a total `120,746 records`. This doesn't seem too bad of a number, however not all of them are
English only. Furthermore, there's no indicator to separate English vs non-English videos. Therefore for the sake of simplicity, we proceed with training on just US videos.

## Modelling and Results

To caption the images, we use LSTMs with an encoder-decoder model. Model architecture and generation code was adapted from
[Machine Learning Mastery](https://machinelearningmastery.com/develop-a-deep-learning-caption-generation-model-in-python/). The model architecture is shown below:

```bash
__________________________________________________________________________________________________
Layer (type)                    Output Shape         Param #     Connected to
==================================================================================================
input_2 (InputLayer)            (None, 43)           0
__________________________________________________________________________________________________
embedding_1 (Embedding)         (None, 43, 256)      1993728     input_2[0][0]
__________________________________________________________________________________________________
input_1 (InputLayer)            (None, 4096)         0
__________________________________________________________________________________________________
dropout_1 (Dropout)             (None, 43, 256)      0           embedding_1[0][0]
__________________________________________________________________________________________________
dense_1 (Dense)                 (None, 256)          1048832     input_1[0][0]
__________________________________________________________________________________________________
lstm_1 (LSTM)                   (None, 256)          525312      dropout_1[0][0]
__________________________________________________________________________________________________
add_1 (Add)                     (None, 256)          0           dense_1[0][0]
                                                                 lstm_1[0][0]
__________________________________________________________________________________________________
dense_2 (Dense)                 (None, 256)          65792       add_1[0][0]
__________________________________________________________________________________________________
dense_3 (Dense)                 (None, 7788)         2001516     dense_2[0][0]
==================================================================================================
```

Image features were generated using VGG16 and the titles were minimal preprocessed by just removing symbols. The vocabulary size was `7,788 words`.
The dataset was split into a `70/30` test/train ratio and the model was trained for 10 epochs using `Adam` as our optimizer.

After training the model, captions were generated for all thumbnails and compared to the original titles. Immediately we notice
something strange...

For a given thumbnail and starting word, we choose the next most probable following word. In our models case, we see that one word has a higher
probability of all other words. In order to generate less non-sensical answers, let's instead uniformly choose a random word from all words.

We definitely have titles now that have some structure. However we do have words which repeat. Removing repeating consecutive words, we are presented with much better titles.

## Further Work

It's no surprise why we have less than desirable results, a couple of reasons being a lack of data and an imbalance of different categories of videos. It certainly would be nice to
have more data, however this project was more of an indulgence of my curiosity than anything.

Some other things we can consider in order to improve this model can be:

#### Adding heuristics the text generation process

Specifically I'm talking about how to make the text generated appear as real titles. One possible way would be to incorporate part-of-speech tagging to the generation.
This can add some overall structure to the titles, therefore making them appear less nonsensical.

#### Use more sophisticated models
Attention models are big right now for image captioning. However your model is only as good as the data you train it on, and if we're only working with `41,000` records,
most of which are non-sensical in the first place, attention models might not give us fantastic results. Nonetheless, it would be interesting to see the results.

If we happen to create a decent caption generation, then we would like to validate our captions using something like a BLEU score.
