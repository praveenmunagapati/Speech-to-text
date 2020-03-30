# Development of Speech-to-Text Solutions

As a part of my corporate research project we worked with WeWyse to do a landscape assessment of Automated Speech Recognition.  ASR is the necessary first step in processing voice. In ASR, an audio file or speech spoken to a microphone is processed and converted to text, therefore it is also known as Speech-to-Text (STT). 

##  Alternatives Compared

##### **Service Based** 
You sign-up for a SaaS, get key/credentials, and you are all set to use it in your code, either through HTTP endpoints or libraries in the programming languages of your choice. However, for reasonably large usage, it typically costs more money. **Two prominent example of service are - Google Speech-to-Text and Microsoft Azure Speech

##### **Software packages**
They offer you full control as you are hosting it, and also the possibility of creating smaller models tailored for your application, and deploying it on-device/edge without needing network connectivity. But it requires expertise and upfront efforts to train and deploy the models. We are here using **Mozilla DeepSpeech for this project.

#### Mozilla DeepSpeech
This open-source project is made by Mozilla based on Baidu’s popular DeepSpeech research paper. Deepspeech model uses Google’s Tensorflow to run it easier and it has 5 hidden layers. The first 3 layers are RelU, 4th layer is LSTM and the last layer is the Softmax activation function. However, the model requires powerful hardware to train it. Because of this limitation, we used a pre-trained model from the Deepspeech project. A pre-trained English model is available for use and can be downloaded, and used as it is an open source project. Pre-built binaries which can be used for performing inference with a trained model can be installed with pip3. Then the deepspeech binary can be used to do speech-to-text on an audio file.
There is a GPU compatible build available as well. The GPU capable builds (Python, NodeJS, C++, etc) depend on the same CUDA runtime as upstream TensorFlow. Currently with TensorFlow 1.15 it depends on CUDA 10.0 and CuDNN v7.6
Google Speech-to-Text

#### Google has speech-to-text as one of the Google Cloud services.
It has libraries in C#, Go, Java, JavaScript, PHP, Python, and Ruby. It supports both batch and stream modes.It enables developers to convert audio to text by applying powerful neural network models in an easy-to-use API. The API recognizes more than 120 languages and variants. Google has patented the handling of acronyms and digits in speech recognition and text-to-speech engine. Which makes it difficult to evaluate the performance of the Google Speech-to-Text service as compared with other competitors which don’t perform such post processing.

#### Microsoft Azure Speech Cloud Service
 Microsoft Azure Speech Services have Speech to Text service. It is a paid service from Microsoft, and we used the functionality to see the type of results it gives just to have a qualitative study and not a quantitative one.
 
## Evaluation Criterion
The most common way to evaluate the performance of the automatic speech recognition model is “word error rate/WER”. There are also sentence error rate/SER, which calculates the error of the full sentence and character error rate/CER, evaluation based on each character.

WER=(Insertions+Deletions+Substitutions)/Total number of words

Insertions – word added that wasn’t said  

Deletions – word left out from the speech  

Substitutions – a word that changed during a speech recognition  

WER is important when you choose between models and automatic speech recognition services. But other factors, such as the quality of the speech, microphone, pronunciation of the speaker and accent can contribute to the error rate.

## Dataset used
LibriSpeech cleaned asudio file data was used since it offered us the possibility to use labeled sentences without background noise. The part of LibriSpeech we used was the test set, "clean" speech which was approx. 2,700 audio files of 346 MB. After loading the dataset we converted the files from .flac to .wav files because most models accept the wav file format as in input.

## Results

Comparing DeepSpeech and Google Speech-to-text API, DeepSpeech performs better than the other in terms of word error rate.
| Mozilla DeepSpeech WER     | Google Speech-to-text WER |
| ----------- | ----------- |
| 0.079   | 0.127      |


## Conclusion
The results seem to be counterintuitive. The reason for the lower WER for Google STT as compared to Mozilla Deep Speech is the patented technology by Google for processgin the transcribed text.

For example Google Speech-to-Text returns “Mr.” instead of “Mister” and “7” for “seven”. 

Since all abbreviations and numbers are written out in the labeled dataset, the WER is higher for Google Speech-to-Text as it is supposed to be. 

