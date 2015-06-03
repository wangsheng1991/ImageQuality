# Brisque
Image Quality Evaluator

## Usage ##

Put **OpenCV** in '/BrisqueFeatureExtractor/OpenCV' folder. 

Instantiate Brisque with the text from a model file (demo project includes default BRISQUE model, and custom trained model)

```C#
var modelText = File.ReadAllText("modelfile");
var brisque = new Brisque(modelText);
```

Score images with the following code:

```C#
var fileBytes = File.ReadAllBytes(fileName);
var score = brisque.Score(fileBytes);
```

If you have multiple models, get the features and score with each model using them.

```C#
var fileBytes = File.ReadAllBytes(fileName);
var features = brisque.Features(fileBytes);
var score = brisque.Score(features);
```

Start training a new model. The DMOS score is from 0 (best) to 100 (worst).

```C#
brisque.Train(fileBytes, 50);
```

Save and resume training if required

```C#
var trainingData = brisque.SaveTraining();
brisque.ResumeTraining(trainingData);
```

Create a new model from current trained data, or specify data to train model with.
Use the result to create a new model

```C#
var newModel = brisque.CreateModel();
newModel = brisque.CreateModel(trainingData);

var newModelBrisque = new Brisque(newModel);
```

## Acknowledgements ##
**Paper:**
Blind/Referenceless Image Spatial Quality Evaluator.Signals, Systems and Computers (ASILOMAR), 2011 Conference Record of the Forty Fifth Asilomar Conference on. Mittal, A. ; Moorthy, A.K. ; Bovik, A.C.

**SVM.NET Library:**
http://www.matthewajohnson.org/software/svm.html

**Ported from:**
https://github.com/pbypby/BRISQUE