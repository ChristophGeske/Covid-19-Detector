# Covid-19-Cough-Rapid-Test for Android

## Why is this relevant?

With the emergence of the Omicron variant we will soon (mid January 2022 peak in 15.01.2022) see a spike in cases including increased hospitalizations and a need for rapid antigen tests, according to the [latest models](https://youtu.be/rRIiJcqyIpY). Also latest studies show that current tests are less accurate in detecting Omicron and the recommendation ist to use 2 tests instead of one which further increases demand for tests.

However with a doubling of cases every 3.5 days it is hardly imaginable how demand for tests can keep up.

Research over the last year showed that detecting Corona from cough sounds alone is possible, but so far no app making use of this technology was made available to the public. 

The development of a publically available Covid test using only the microphone in widly available Android and iOS phones could help reduce the impact the Omicron wave will have.

## Current state of the project

A simple model (not for cough data yet) was trained and imported into an Android app. The model used in the app is just an proof of concept and needs to be replaced with a real model able to detect cough data. The App needs to be extended to record cough sounds and put them through the model returning an positiv/negative result. 

## Prerequesits

#### Available public code projects:

* [Covid cough Classification on GitHub](https://github.com/rosikand/covid-cough-test)
  * convolutional neural network (CNN) 
  * Uses Mobile Net an image classification network to train on [MEL spectograms](https://medium.com/analytics-vidhya/understanding-the-mel-spectrogram-fca2afa2ce53) 
    * Not sure why to transformed the spectrogram into a ML spectrogram since the mel scale is only relevant to adjust the sound to human hearing, which we don't need if only the computer is "hearing" and analysing the cough sound. So why the added complexity?
  * A similar well documented instrument classification project named [Musical Genre Classification on GitHub](https://github.com/lelandroberts97/Musical_Genre_Classification) is available with an [easy to understand article](https://towardsdatascience.com/musical-genre-classification-with-convolutional-neural-networks-ff04f9601a74) explaining the concepts.
* [CNN-Audio-Classifier-with-Keras-Tensorflow](https://github.com/adanRivas/CNN-Audio-Classifier-with-Keras-Tensorflow)
  * transfear learning done using the [ESC-50 dataset](https://github.com/karolpiczak/ESC-50) containing 2000 environmental audio recordings
  * mel spectograms
  * Not a Covid sounds dataset only sounds of diseased sound dataset [here](https://osf.io/tmkud/files/) 
  * [Wiki page](https://osf.io/tmkud/wiki/home/) 

#### Available public sound Datasets:

- No Covid sounds found yet

#### Paper List:

* [Review Paper:](https://arxiv.org/ftp/arxiv/papers/2112/2112.07285.pdf) Lella, Kranthi Kumar, and Alphonse Pja. "Automatic COVID-19 disease diagnosis using 1D convolutional neural network and augmentation with human respiratory sound based on parameters: cough, breath, and voice." AIMS Public Health 8.2 (2021): 240.

* [Paper: Detection with Android-App (AI4COVID-19):](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7318970/) Imran, Ali, et al. "AI4COVID-19: AI enabled preliminary diagnosis for COVID-19 from cough samples via an app." Informatics in Medicine Unlocked 20 (2020): 100378.
  * App seems not available to public
  * They use "transfer leraning" to make up for missing cough sound data

* [MIT Paper claiming asymptomatic detection via cough sound data](https://ieeexplore.ieee.org/document/9208795)
  * Uses "transfer learning" on alzheimers dataset, showing improvements in accuracy

#### Further relevant projecs:

* [COVID-19 Sounds App](https://www.covid-19-sounds.org/en/) maybe as a source for more trainings data.
  * Sounds, Spectrograms and MEL-Spectrograms avaialable
  * MEL-Spectrograms could be used directly, reducing complexity and the steps needed for training
  

## Implementation details (Work in progress)

1. We start with a new Android Studio project. Using the "Basic Activity template", API level 23 Marshmallow (for >95% device coverage) and Java as the programming language.  
2. Train the model with Kares in Google Colab resulting in a .h5 and .tflite file. See the SimpleExampleOfTrainigATesnsorflowModel.ipynb for details.
3. Add the functionality of running pretrained models on android following [this guide](https://medium.com/geekculture/train-ml-model-and-build-android-application-using-tensorflow-lite-keras-6bf23d07309a) and [this github repo](https://github.com/ShuklaAnuja/Python-ML---Android-Kit)
4. Created an asset folder and add the tflite file you trained with Google Colab and downloaded in the previous steps. https://stackoverflow.com/questions/18302603/where-to-place-the-assets-folder-in-android-studio
5. ...

## Some thought for later implementation

- transfer lerning looks like a must
- the cough sounds must be cropped to have the same length for training and detection!
- 'selective Training' idealy we collect personalised cough data of the user before he gets covid to reduce the false positive rate of the app. Gender, age, ... or just use user recordings to classefy the user and train a better personalized model with trining data similar to the user.
- Put disclaimers everywhere with the exact accuracy of the test, using graphics and simple clear sentences!
