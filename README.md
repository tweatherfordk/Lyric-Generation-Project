# Lyric Generation Project
## Overview
Inpired by my curiosity as to whether I could create a model to approximate the way I write in journal entries, I decided to see if I could capture the spirit and poetic whimsy of some of my favorite band's lyrics. 

![image](https://user-images.githubusercontent.com/110851861/212820687-f6523072-2e39-465f-adb1-5f6090594fdf.png)

## Business Understanding
Lyrics are often impressionistic in nature and their ability to convey emotion within the conetext of a song is often just as important as their narrative function. 

## Data Collection
In order to scrape lyric data, I registered for a client access token for Genius’s API. Using the package “lyricsgenius”, which streamlines the process of pulling information from the Genius API with concise commands. By searching for each artist’s specific ID number, I collected all of the lyrics to each of their entire discographies, then created a corpus dataframe of 1254 different songs in string format.

## Data Preprocessing
First, I used a function to clean the text by removing punctuation, lowercasing all characters, remove any trailing whitespace, and splitting by line. Next, I used Keras’s Tokenizer to assign a numerical value to each word in the corpus, and then converted each line into a sequence of it’s tokens. Then all of the words were One Hot Encoded to use in training the model as a way to measure the text prediction against the word orders in the actual lyrics. At the end of the preprocessing, the text lyrics from the corpus have been converted to numerical data in sequential format that are now ready to be fed into a model.

## GloVe Embeddings
Word embeddings are a way to model the relationship between words in a vector (or multidimensional) space. They encode the meanings of words, with words that are closer together having more similar meanings. GloVe (Global Vectors for Word Representation) is an unsupervised learning algorithm that was developed at Stanford University to map out these relationships between words. It maps co-occurrences between words across a whole corpus and generates the embedding from them. I constructed an embedding matrix using GloVe and then created an untrainable embedding layer to use in the model for preserving the relationship between the words.

## Modeling

First, I initialized a sequential model, and added the pretrained GloVe embedding layer as the first layer. Next, a bidirectional LSTM model was added with 20 units in the layer. 
Then, a dense layer was added with the softmax function as the activation function as it normalizes the network output for the different output classes across a probability distribution. In our case, it is which token should come next in the text generation model. 

## Sample Lyrics

### Seed 1
Inspired by [this clip](https://www.youtube.com/watch?v=H7vk5keNbRc&ab_channel=ScantRegard) from 1984 Hair Metal drama Spinal Tap, our seed text was as follows:  “I want you to lick my pump baby". Limiting it to 100 words, the algorithm produced:
> i want you to lick my pump baby and all the waves is gone to play to bring in me im stuck lie on myself run my heart sit the man that you wants to turn the takes in the virgins and makebelieve moon and over of metal gorgeously that trick that if no to cant at my on us in a glimmering through trees tonight razor better bare next kiss all me showed inside of a bong on the bathroom summers ahh hand some live wearing you aground not needs twenty gripping morning as this is nobody from live of medicine other ways i fought now im

Key phrases include:
- “razor better bare next kiss all me showed inside of a bong on the bathroom summers”
- “ahh hand some live wearing you aground”
- “im stuck lie on myself run my heart sit the man”

While not grammatically correct because the model uses probability to determine the next most likely word, this example shows that indeed, the poetic whimsy and vivid imagery of good lyrics is indeed alive and well within this model.

### Seed 2
Seed Text: “Tormented in the bagel shop” 
> Tormented in the bagel shop variety christened again on bended aiming mansion fleurs nurse both guitar shivering curaetion lyricsinstrumental intro and video that actually much to be to see you she told my fucking golf and kiss meyou might also seeing im against time for the way me by a dancer no he dont would stay to the of darkness exciting like my structure come into the the up and walk in the beating as i going by the things you and all the different ways i was sure though why you believe know there come and let you help it must be coming home

Selected Snippets:
- “variety christened again on bended aiming mansion fleurs”
- “golf and kiss meyou might also seeing im against time”
- “of darkness exciting like my structure come into the the up and walk in the beating”

## Future Work
In order for its function to be expanded past an idea generator, a springboard of inspiration for the songwriter to piggy-back off of, a way to introduce grammatical rules would be necessary. Whether it is achieved through a larger corpus, a greater number of epoch to train over, or an entirely different model architecture, this would be the next step of the process. It is also worth looking into website hosted chatbots so playing with this tool is more readily accessible without having to access the code yourself.
