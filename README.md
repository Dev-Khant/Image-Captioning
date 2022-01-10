# Image Captioning Using EfficientNet and GRU

### Models & Dataset
- EfficientNetB0 which is state of the art model for image processing is used. The model and its variantes are [here](https://github.com/qubvel/efficientnet).
- Attention Mechanism is used to focus on certain parts of images. Here is a nice explanation for [Attention](https://towardsdatascience.com/attention-in-neural-networks-e66920838742).
- Gated Recurrent Unit(GRU) is model used for processing text.
- The Dataset used here is [Flickr(30K)](https://www.kaggle.com/hsankesara/flickr-image-dataset).
- The Dataset contains 30k images along with 5 annotations for each image. Here I have used only first annotation of each image.

### Parameters & Libraries
- Tensorflow, NLTK, Numpy, Pandas are used.
- For converting text to embedding vectors **TextVectorization** is used with vocabulary size of 5000, sequence length of 25 and with embedding dimension of 256.
- The image size for EfficientNet is (224, 224, 3). EfficientNet was loaded with weights from ImageNet.
- Units for GRU are 512.

### Training & Evaluation
- Here training is done on batch size of 64 for 25 epochs.
- Encoder consists of EfficientNet and a FC layer for fine tunning. Decoder consists of GRU along with Attention Mechanism.
- First the image is passed to EfficientNet and image context vector is obtained then along with image context vector hidden_state(intial state of decoder) is passed to Attention layer now its output is passed to GRU along with embedding vector of "[start]" token.
- Here Teacher Forcing is used which is while training we pass the word vector of target sentence to GRU.
- While testing the model input to GRU is previous output along with Attention output.
- Loss obtained by model is 0.511. And BLEU score on test data is 0.129
- Here are 2 examples after training.


<br> &nbsp; &nbsp; ![ex1](https://user-images.githubusercontent.com/57898986/148728161-4937f8a5-7f10-4355-b660-e650f322f237.png)
&nbsp; ![Screenshot 2022-01-06 151649](https://user-images.githubusercontent.com/57898986/148727521-b678fec3-2e68-4d1b-a942-b3568b8b7f86.png)



