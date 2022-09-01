# Speech Enhancement

I originally developed this code within Kaggle (https://www.kaggle.com/code/tariqblecher/speech-enhancement-tensorflow-unet-softmask). Please check the Kaggle environment for access to the datasets.


Speech Enhancement Algorithm based on Tensorflow and Keras

Data I mixed clean speech data from RAVDESS dataset with noise data from the UrbanSound8K dataset. As tensorflow was unable to read the raw files, I rewrote the original datasets locally and uploaded them back onto Kaggle. I also downsampled the datasets back to 8K - this captures most of the Speech signal.

This is quite a limited dataset for speech enhancement. My goal for this project was primarily to check how well this algorithm generally to a completely different unseen dataset.

ALGORITHM This algorithm takes an Short Time Fourier Transform (STFT) of the audio files to return the transformed signal as a 2D array of dimensions time and frequency. The transformed signal is complex, but the algorithm only operates on the amplitude. The amplitude is passed through a softmask + UNet algorithm. This is a re-worked version from https://github.com/karolzak/keras-unet where I added the softmask component.

Loss Function

I started with just an MSE loss between the clean speech amplitude and the reconstructed speech amplitude, however, this had the problem that it treated keeping noise equivalent to losing speech. As it is much more important to keep speech than to reduce noise, I created a custom loss function which features both a MSE term and another term which focuses specifically on

METRIC The PESQ metric is used in the industry as an automatic way to measure speech quality. It is not without it's problems but it still works as a first pass. I would advise you to listen to the output files (clean, corrupted and corrected) to get a better sense of how the algorithm performs.

Unseen data test In the Notebook below I test the model on a completely different dataset featuring 150+ different english accents mixed with hospital noise. https://www.kaggle.com/tariqblecher/speech-enhancement-unseen-data-test

Results On the validation data, we saw an average increase of +0.44 in the PESQ score (from 2.08 to 2.52) In the unseen test data, we saw an average increase of +0.17 in the PESQ score (from 2.13 to 2.30)

Please cite this notebook if you use it.

contact : tariq.blecher@gmail.com
