# Introduction
This is my entry to [Kaggle's Melanoma Classification competition](https://www.kaggle.com/c/siim-isic-melanoma-classification). The goal of the competition was to create a model that could look at a number of images if malanoma on a patient and predict if any were dangerous.

# First approach - Transfer Learning
My first approcah, Which you can view in the [Exploration notebook](https://github.com/HarveyBrezinaConniffe/MClass/blob/master/Exploration.ipynb) used transfer learning. I ran each image through a pretrained InceptionV3 network and trained a classifier on the output.
This worked surprisingly well, Reaching 0.80 AUC on the public test set. However this model used no context, It looked at each melanoma individually without knowing about other melanoma on the patient.

# Second approach - Transformer based network
My second approach was a more ambitious attempt, Using context. Each image was fed through a ConvNet to generate a 1D vector of features( The 'embedding' of that image ). For each patient I then constucted a sequence of embedding vectors( One per melanoma image )
These sequences were then run through a [Tranformer network](https://arxiv.org/abs/1706.03762). The transformer network outputted a new sequence of embeddings of the same length( One per image ), The sequences hopefully contained a representation of the image with context to the other images.
Finally each embedding was run though a Dense neural net to produce a prediction.
Unfortunately this method did not manage to beat the performance of my first approach, Only ever achieving 0.6 AUC on the test set. However I do believe with more time and improvements this method has the potential to perform very well.

# NOTE
At some point I hope to neaten up/improve this README and the notebooks here.
