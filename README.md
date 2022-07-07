# Overview of the FLERT-Matcher model at LivingNER shared task (https://temu.bsc.es/livingner/)

- Subtask 1: We trained a NER model based on the FLERT approach. This model consists of fine-tuning a pre-trained language model
  but considering the document-level context.

- Subtask 2: Based on the predictions of subtask 1, we matched the entity mentions with the definitions of codes found in the training corpus and the NCBI taxonomy. This was done using the Levenshtein Distance.

- Subtask 3: We trained a NER model based on the FLERT approach to address each binary classification problem. We merged the output of each model with the predictions of subtask 2. Finally, we grouped the mentions by document and transformed the predictions to document-level.

## Install

1. Create an enviroment: `python -m venv venv` and activate it.
2. Run `pip install -r requirements.txt` to install all dependencies
3. Download the statistical model to perform the tokenization: `python -m spacy download es_core_news_lg`
4. In case you use a GPU NVIDIA RTX 3090, then install this PyTorch version: `pip install torch==1.10.1+cu111 torchvision==0.11.2+cu111 torchaudio==0.10.1 -f https://download.pytorch.org/whl/torch_stable.html`

## Creating data for NER Training

Place the folder training_valid_test_background_multilingual (https://zenodo.org/record/6768606) inside the folder src/data/ner_utils.

Subtask 1 (Species)

`cd src/data/ner_utils`
`python main.py --subtask 1`

Subtask 3 (Food, Animal Injury, Pet, Nosocomial)

`cd src/data/ner_utils`
`python main.py --subtask 3 --subtask3_entity_type FOOD`
`python main.py --subtask 3 --subtask3_entity_type ANIMALINJURY`
`python main.py --subtask 3 --subtask3_entity_type PET`
`python main.py --subtask 3 --subtask3_entity_type NOSOCOMIAL`

NER files will be placed in ner_data folder.

## Training NER Models

`cd src/models/ner-flair/src`

Training parameters can be changed in `config.yaml` file

Run the script `python main.py`. The results will be printed to console.

## Predictions

Go back to the home directory of this repository. Place the trained NER models in the `models` folder with the following names: `species.pt`, `animal.pt`, `pet.pt`, `nosocomial.pt`, and `food.pt`.

Run the script in the main folder. `python main.py`

## Contact

Authors: - Matías Rojas - Jose Barros - Mauricio Araneda - Jocelyn Dunstan

Mail: matias.rojas.g@ug.uchile.cl
