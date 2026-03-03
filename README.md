# midwest_survey_models

A couple of quick models designed for the dataset midwest survey.

# How to

- Fork this repository.
- Clone it locally.
- Run `pixi install` to create a clean virtual environment.
- Run `pixi run convert-to-notebooks` if you prefer to work with notebooks rather than python files. 
- If you have too much trouble with pixi, you can use your usual virtual env system, and use the requirements.txt.
- Answer the questions below based on your exploration.
- Run `pixi run convert-to-python-files` if you worked in notebooks.
- Push your code and your answers to your fork.

# Steps of the tutorial

1. Look for a file called "security_breach.txt" in your computer. How was it created?
   
Le fichier security_breach.txt a été créé par l’un des modèles pré entraînés au moment du chargement ou de l’exécution de son code .

2. This file created is quite harmless; could you give an example of something that could have been done more harmful?
   
Chiffrer ou voler des données locales et les envoyer sur un serveur externe.

3. Implement a new way to safely share models (hint: check the library skops)

from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

import skops.io as sio

iris = load_iris()
X, y = iris.data, iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=0, stratify=y
)

model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)

sio.dump(model, "logreg_iris.skops")

unknown_types = sio.get_untrusted_types("logreg_iris.skops")
loaded_model = sio.load("logreg_iris.skops", trusted=unknown_types)

y_pred = loaded_model.predict(X_test)
print("Accuracy after reload:", accuracy_score(y_test, y_pred))

Once all these are done, you can continue to the third part of this guided work: prepare a presentation with your group.
