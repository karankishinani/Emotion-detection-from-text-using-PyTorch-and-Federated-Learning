# Emotion Detection from text using PyTorch

## Collaborators

Name | Slack handle |
--- | --- |
Karan Kishinani | @Karan Kishinani |
Kapil Chandorikar | @Kapil Chandorikar |
Aditya Kumar | @Aditya kumar |

## Project Notebook

Open project [notebook](Emotion_detection_from_text_using_PyTorch.ipynb).

## The Project

### What is the project about?
This project is about performing emotion detection from text using PyTorch and Federated Learning.
For this project, we implemented an NLP task of creating a model to detect the emotion from text. We developed this using the PyTorch library where we created our Deep Neural Network using GloVe Word Embeddings, LSTMs and fully connected layers. Additionally we added the Federated Learning framework for decentralized training.

### Why?
This project serves as a demonstration of the concepts taught in the *Secure and Private AI Challenge*, by Udacity and Facebook along with some of the members of the `#sg_caffeine_coders` Study Group. This is our submission for the Project Showcase Challenge for this program.

### Dataset

Phase | Instances | File |
--- | --- | --- |
Training | 132 | train.csv |
Testing | 56 | test.csv |

* Each sentence contains maximum 10 words.     
* GloVe Embedding used: `glove.6B.50d.txt`   
The embedding can be downloaded from [here](https://worksheets.codalab.org/rest/bundles/0x97c870dd60eb4f0fa53f257978851c60/contents/blob/glove.6B.50d.txt ).

For example:

| Sentence | Emotion   |
|----------|-----------|
|food is life|  🍽 Foodie|
|I love you mum|  ❤️ Loving|
|Stop saying bullshit|  😞 Annoyed|
|congratulations on your acceptance|  😄 Happy|
|The assignment is too long|    😞 Annoyed|
|I want to go play| ⚽️ Playful|
|she did not answer my text| 😞 Annoyed|
|Your stupidity has no limit| 😞 Annoyed|
|how many points did he score|  ⚽️ Playful|
|my algorithm performs poorly| 😞 Annoyed|
|I got approved|  😄 Happy|


### Emotions

We will create an emotion detection for the following 5 emotions:

| Emotion | Emoji   | Label   |
|------|------|------|
|Loving| ❤️| 0|
|Playful| ⚽️| 1|
|Happy| 😄| 2|
|Annoyed| 😞| 3|
|Foodie| 🍽| 4|

### Model
We will build an LSTM model that takes as input word sequences that will take word ordering into account. We will use 50-dimensional GloVe pre-trained word embeddings to represent words. We will then feed those as an input into an LSTM that will predict the most appropiate emotion for the text.
![Model Architecture](https://drive.google.com/uc?id=1s-KYhU5JWF-jvAlZ2MIKKugxLLDdhpQP "Model Architecture")

### Results
We are able to succesfully create a model that could achieve an accuracy of `84.4%` in our training set and also were able to use our model on user inputted sentences and were able to get expected emotion outputs.

`Test Loss: 1.064..  Test Accuracy: 0.844`

The following results are emotion predictions on user inputted sentences:
```

Input Text: 	I hate you
Emotion: 	😞 Annoyed

Input Text: 	I want a pizza
Emotion: 	🍽 Foodie

Input Text: 	Lets see the match
Emotion: 	😞 Annoyed

Input Text: 	I love you Lisa
Emotion: 	❤️ Loving

Input Text: 	This is the best day of my life
Emotion: 	😄 Happy

```

### Open Issues
We additionally added Federated Learning in our project and our code is  is meant to work out of the box, however at the time of project submission, there is an open issue in PySyft that causes an error with the LSTM implementation in PyTorch while performing Federated Learning. 

The problem is that GRUs and LSTMs from PyTorch use the method `.size()` to get the shape of tensors. It works well in PyTorch code, but it doesn’t in PySyft, because while performing Federated Learning with remote tensors, the `.size()` of a pointer is always `0` and we only can use `.shape` on pointers to get the shape of the tensor.

You can look at the following open issue in PySyft which was also brought up by a fellow scholar from the SPAIC program `@André Farias`:

https://github.com/OpenMined/PySyft/pull/2349

Once the issue has been resolved this code should work after PySyft has been updated.

## Final Comments
Security and Privacy is what gives our model a powerful existence and this is where Federated learning comes. Federated learning doesn't just allow us to train model at user end or at neutral aggregators end it also acts as technique to manage the data aggregation happening from multiple teaching devices. Being able to train on distributed text data (mimicking the concept of getting and deploying trained models or summary from teachers in this case devices like - mobile and Computers) can make this idea of emotion detection from text useful and efficient for modern day keyboards prediction and emoji prediction on the fly.

Please take a look at our project [notebook](Emotion_detection_from_text_using_PyTorch.ipynb) for a more detailed view on our project. 
