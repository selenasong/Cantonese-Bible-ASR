### Cantonese Bible Speech-To-Text System

## Abstract 
Downloaded audio clips and scraped transcription from an online multilingual Bible corpus. 
Created a 14-hour dataset by force alignment with SpeechBrain and segmentation to clips of 1 to 5 seconds. 
Fine-tuned on a pretrained Cantonese wav2vec model on Hugging Face with the self-created dataset. 
Character error rate on the same test set decreased from 0.48 to 0.28 after fine-tuning. 

## Dataset 
# Training set
All audio in the training corpus come from one of the available recordings for Cantonese bible New Testament on bible.is, with a total length of more than 20 hours. 
However, since there are lots of files that too big to be processed, around 6 hours of data were discarded. 
Now the training set has in total 14 hours 39 minutes and 3 seconds of recordings.

Audio files from this website are of high quality. 
Speakers pronounce the characters correctly and clearly, pause long between sentences, and speak with strong emotions when there are punctuations such as exclamation mark. 
Besides, there is no noise at all. 
Other than a male speaker who talks for most of the time, there are some other speakers involved, both male and female, when there are conversations. 

A drawback of not only this data set, but all data, is that the time stamps provided by the speechbrain model is not 100% accurate. 
After chopping the audios up according to these time stamps, there are some words that are cut in the middle of the pronunciation. 
Fortunately, this is not seen in lots of files, and this only appears at the beginning or the end of clips. 

Transcripts were also extracted from the same website. 
For each file of transcript, to make the speechbrain model perform normally, we separated paragraphs of texts into lines according to punctuations, after which we removed all punctuations and added space between Chinese characters. 
Audio files and transcripts were later sent to speechbrain model to do force alignment, based on whose output we chopped recordings into at most 10 seconds ones and created each clip’s corresponding transcript. 

# Dev set
To avoid speaker overlapping, audio files in this corpus come from another website that also have bible recordings for a list of languages (https://www.wordproject.org/bibles/audio/13_cantonese/index.htm). 
To avoid extra work of extracting texts, audio files for the dev set is also about New Testament. Resampled audio and their corresponding line-by-line transcripts were then sent to do force alignment and segmentation as in training set. 

The main speaker is also male, but it should be a different speaker from the on in the training data judging by the difference of their voices. 
Compared with the audio files from bible.is, audios from this website are of lower quality – there are some noises, the speaker does not speak super clearly, and there is not much emotion involved. 
This speaker talks like a normal people reading a book out loud, instead of like a professional. Although the content in the audios in dev set can completely be found in training set (i.e., they share the same transcript), since they are recorded with different speakers and they are of different quality, this dev set should still be useable data for the machine learning in the next assessment. 

# Test set
The source and the data processing are the same with dev set, and the content can again be found in the training set because they are also recordings on New Testament. For the test set, the main speaker is a female. Chapters of bible covered in this set is totally different from those in the dev set. 
![image](https://github.com/selenasong/Cantonese-Bible-ASR/assets/127460254/3c1260ad-e936-4afa-a77f-f09b9baa9d06)
