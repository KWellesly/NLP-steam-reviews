# NLP-steam-reviews

## Setup

* Download glove.6B.zip from https://nlp.stanford.edu/projects/glove/. Unzip it and add it to the `data/` directory.
* Install required Python libraries: `python install -r requirements.txt`

## For testing exising models [RECOMMENDED]:
#### Option 1- Download base transfer learning model and train on top
* Download base transfer learning model: https://drive.google.com/open?id=1tS9x5Iqs71IafdEBGDokTW1Ax7ttPjfh
 * Note. Trained with pre-trained GloVe embedding, 100 embedding dimensions, 64 LSTM dimensions, attention layer. 84.4% evaluation accuracy.
* Place the model in `models/`
* Use `model_training_recommendation_transfer_learning_steam.ipynb` to do transfer learning on top of the downloaded model.
#### Option 2- Download the final most optimal model and test it's evaluation accuracy [RECOMMENDED]
* Download the final model: https://drive.google.com/open?id=1W12w4z9S92u_1LGHvYULoiJbXG3CdTOS
* Place the model in `models/`
* Open `model_training_recommendation_transfer_learning_steam.ipynb`. Run all the cells, but **skip the cell titled # training loop**. Running the **# evaluate** cell will output the evaluation accuracy of the model.

## For end2end testing of the pipeline and training from scratch [NOT RECOMMENDED]:
#### Option 1 - download raw data and run through `data_cleaning_steam.ipynb` and `data_cleanin_amazon.ipynb` [NOT RECOMMENDED]
* Download the Steam dataset from: https://www.kaggle.com/luthfim/steam-reviews-dataset and place the data inside the `data/` directory.
* Download the Amazon dataset from: http://jmcauley.ucsd.edu/data/amazon/. Get the Video Games `5-core (231,780)` dataset and place the data inside the `data/` directory.
#### Option 2 - download cleaned data [RECOMMENDED]
* Download the cleaned Amazon dataset from: https://drive.google.com/open?id=1FZRi7vqQ0a2B7qXUd-f8cBWN2ObTzK6m [314MB]
* Download the cleaned Steam dataset from: https://drive.google.com/open?id=1JIAaOocsdo4ZkIERzM0lhxuidjY0lSp8 [284MB]
* Place all the data in the `data/` directory.
#### Training Pipeline
* NOTE: All training is done on local GPU. If GPU memory is a constraint, please remove the `.cuda()` on ALL model parameters
* The first step is to train the base model on Amazon's video game dataset used in transfer learning. Open `model_training_recommendation_amazon.ipynb`. Run all cells. At the end, please save the model to your desired path. EX: `PATH = 'models/amazon_model_1.pt'`
* Next, open `model_training_recommendation_transfer_learning_steam.ipynb`. When loading in the pre-trained Amazon model, use the same path as above, ex: `PATH = 'models/amazon_model_1.pt'` right before the `.load_state_dict()` call.
  * Running through to the evaluation step will show the final evaluation accuracy
