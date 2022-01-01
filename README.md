# Covid-19-Cough-Rapid-Test for Android

## Why is this relevant?

With the emergence of the Omicron variant we will soon (mid January 2022 peak in 15.01.2022) see a spike in cases including increased hospitalizations and a need for rapid antigen tests, according to the [latest models](https://youtu.be/rRIiJcqyIpY). 
New studies also show that current tests are less accurate in detecting Omicron and the recommendation ist to use 2 tests instead of one which further increases demand for tests.

However with a doubling of cases every 3.5 days it is hardly imaginable how demand for tests can keep up.

Research over the last year showed that detecting Corona from cough sounds alone is possible, but so far no app making use of this technology was made available to the public. 

But the latest research has also shown, that Omicron affects the upper airways more than the lung which might be the reason for less sevarity and might result in decreased accurecy when only relying on cough data. Therefore a focous should be put on other sounds like voice and breathing as well!

The development of a publically available Covid test using only the microphone in widly available Android and iOS phones could help reduce the impact the Omicron wave will have.

## Current state of the project

A simple model (not for cough data yet) was trained and imported into an Android app. The model used in the app is just an proof of concept and needs to be replaced with a  model able to detect real covid cough data. The App needs to be extended to record cough sounds and put them through the model returning a positiv/negative result. 

## Prerequesits

#### Available public code projects:

* [Covid cough Classification on GitHub](https://github.com/rosikand/covid-cough-test)
  * convolutional neural network (CNN) 
  * Uses Mobile Net an image classification network to train on [MEL spectograms](https://medium.com/analytics-vidhya/understanding-the-mel-spectrogram-fca2afa2ce53) 
    * Not sure why to transform the spectrogram into a ML spectrograms since the mel scale is only relevant to adjust the sound to human hearing, which we don't need if only the computer is "hearing" and analysing the cough sound.
  * A similar well documented instrument classification project named [Musical Genre Classification on GitHub](https://github.com/lelandroberts97/Musical_Genre_Classification) is available with an [easy to understand article](https://towardsdatascience.com/musical-genre-classification-with-convolutional-neural-networks-ff04f9601a74) explaining the concept.
* [CNN-Audio-Classifier-with-Keras-Tensorflow](https://github.com/adanRivas/CNN-Audio-Classifier-with-Keras-Tensorflow)
  * transfear learning done using the [ESC-50 dataset](https://github.com/karolpiczak/ESC-50) containing 2000 environmental audio recordings
  * mel spectograms
  * [Dataset of sounds of symptoms associated with respiratory sickness](https://osf.io/tmkud/files/) this is not a covid cough dataset!
  * [Wiki page](https://osf.io/tmkud/wiki/home/) 

* [COUGHVID: REDME and Code for data pre-processing](https://c4science.ch/diffusion/10770/)



#### Available public sound Datasets:

* [COUGHVID](https://coughvid.epfl.ch/about/) 
  * [public dataset](https://zenodo.org/record/4498364)
  * over 25,000 crowdsourced cough recordings  
  * size of 1.3 GB
  * more data may be available on request coughvid@epfl.ch

#### Paper List:

* [Automatic COVID-19 disease diagnosis using 1D convolutional neural
network and augmentation with human respiratory sound based on
parameters: cough, breath, and voice](https://arxiv.org/ftp/arxiv/papers/2112/2112.07285.pdf) 
  * Review Paper

* [AI4COVID-19: AI enabled preliminary diagnosis for COVID-19 from cough samples via an app](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7318970/)
  * Android-App (AI4COVID-19) seems not available to public
  * App sends data to the cloud for analysis, which has the adventage of being able to keep the model up to date for all users. But the disadventage of requiring an internet connection.
  * They use "transfer leraning" to make up for missing cough sound data

* [COVID-19 Artificial Intelligence Diagnosis Using Only Cough Recordings](https://ieeexplore.ieee.org/document/9208795)
  * asymptomatic detection
  * "transfer learning" on alzheimers dataset, showing improvements in accuracy

* [“Hi Sigma, do I have the Coronavirus?”: Call for a New Artificial Intelligence
Approach to Support Health Care Professionals Dealing With The COVID-19
Pandemic](https://arxiv.org/ftp/arxiv/papers/2004/2004.06510.pdf)
  * "transfer learning" CNN trained on regular speech dataset
  * three types of sounds used: Cough, digits from 0 to 9, word “Ommmmmmm”, with “m” sound extending for 12 seconds
  * 0.99 second long raw audio files used

* [COUGHVID crowdsourcing dataset, a corpus for the study of large-scale cough analysis algorithms](https://www.nature.com/articles/s41597-021-00937-4)

* [Automatic diagnosis of COVID-19 disease using deep convolutional neural network with multi-feature channel from respiratory sound data: Cough, voice, and breath](https://www.sciencedirect.com/science/article/pii/S1110016821003859?via%3Dihub)
  * good review of other Papers (see the summary table 1) with the realization that: -> "No accurate model for diagnosing COVID-19 disease symptoms exists. Implementing a deep CNN model along with multi-feature channels (De-noising Auto Encoder, GFCC, and IMFCC) leads to better results"
  * using voice, dry cough, and breath results in better accuracy (95.45%) and performance compared to cough only (see table 4)
  * show differnt methods for Augmentation of the data like shifting pitch adding bg noise. (see section 3.1.2.)
  * regularization techniques like dropout (see section 4.)

* [Exploring Automatic Diagnosis of COVID-19 from Crowdsourced Respiratory Sound Data](https://dl.acm.org/doi/pdf/10.1145/3394486.3412865)
  * the mobile app gathers data from single individuals up to every two days, allowing for potential tracking of disease progression

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

* transfer lerning looks like a must
* the cough sounds must be cropped to have the same length for training and detection!
* 'selective Training' idealy we collect personalised cough data of the user before he gets covid to reduce the false positive rate of the app. Gender, age, ... or just use user recordings to classefy the user and train a better personalized model with trining data similar to the user.
* Put disclaimers with the accuracy of the test, using graphics comparing the accuracy with rapid antigen and PCR tests for comparison
* Inform user on what sound is best for detection and dicurrage users with bg noise or other respiratory deseases to use the app since its not clear if it works well for them.
* Output should include the confidence of the model and the information that the disclaimer that the results can be wrong even if confidence is high. Also It should be very simple by presenting a probability of having covid and giving the user the option to see more detailed data of his recording analysis.
* A combination of cloud based analysis when an internet connection is available and a on device analysis tool for offline use would be ideal.
* According to [Andrew Ng famous ML lecture](https://youtube.com/playlist?list=PLkDaE6sCZn6Ec-XTbcX1uRg2_u4xOEky0) 
   * CNNs are good for image detection but RNNs are better for sounds
   * larger network and more data are the 2 main factors for improving the network
   * ReLU speeds up training compared to sigmoid [activation function](https://youtu.be/Xvg00QnyaIY), but sigmoid should be used for the last(output) layer since we only have 0 or 1 as an output
   * [Hyperparameters](https://youtu.be/VTE2KlfoO3Q) are Alpha (Learning rate), # of iterations of Gradient Descent, find the right number of [hidden layers](https://youtu.be/2gw5tE2ziqA), # of hidden Units (nodes per layer),  which activation function in which layer, momentum, min-batch size, regularization parameters, .... -> use trial and error and itterate to find optimum.
   * [train/dev/test set](https://youtu.be/1waHlpKiNyY) should have a ration of 60%/20%/20% when dealing with limited amount of data as in our case of covid sounds.
   * Make sure that dev and test set come from the same distribution but it is ok if training set comes from an other distribution e.g. for the sake of more data
   * If the result has [high bias(underfitting) and/or high variance(overfitting)](https://youtu.be/C1N_PDHuJ6Q) try: bigger network (until bias shrinks), train longer (never hurts), different nural network arcitecture, more data and [regularization](https://youtu.be/NyG-7nRpsW8) (in case of high variance).  



