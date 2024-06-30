## Project Description
This project aims to create a browser extension that corrects Turkish text typed using an English keyboard. The Turkish alphabet contains additional letters compared to the English alphabet, leading to multiple Turkish equivalents for some English letters.  
For instance, the English letter 'c' can correspond to both 'c' and 'ç' in the Turkish alphabet. Therefore, to generate accurate corrections, multiple variations of the typed word must be created by substituting letters with their Turkish equivalents.

![generatingVariations](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/2b387849-7737-476a-ad0f-9c1b4219c1f4)
    
However, generating variations results in 2^n new words, where n is the number of letters in the word that have multiple equivalents. As n increases, processing these variations becomes increasingly difficult. To manage this, some of the generated words are eliminated through a dictionary lookup, ensuring that only valid Turkish words are considered. 
    
![eliminatingVariations](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/e1be9de8-9367-4e9f-af05-818e75f6c8e7)

Additionally, due to the nature of the Turkish language, it is challenging to cover all words using a dictionary alone. Therefore, major and minor vowel harmonies are implemented to aid in the elimination process.
    
![vowelHarmonies](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/52cb6761-1e80-481c-a8f4-a60730b24a02)

After the elimination of invalid words, the remaining variations are combined to form sentences. This process may result in one or many sentences.

![combiningWords](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/b749d78d-8614-4ebc-9a49-5ec9680f66c3)

If only one sentence is formed, it is considered the correct sentence. However, if multiple sentences are formed, the correct one must be chosen wisely using a deep learning model.

The deep learning model must select one of the sentences as the correct one. To achieve this, a dataset is created by extracting texts from the Turkish Wikipedia dump and splitting them into valid sentences. Since a binary classifier is required, invalid sentences are also needed. An invalid sentence is very similar to a valid sentence, except that one word is not valid in the context of the sentence. To train the deep learning model to distinguish valid sentences from invalid ones, it must be trained with sentences following this logic. Therefore, invalid sentences are created by replacing one of the words in a valid sentence with another valid Turkish variation of that word.

![creatingDataset](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/4d20e899-9b36-496f-8272-73ec1aef03cf)

A sequential deep learning model is created for this project, consisting of multiple layers:

1. **Embedding Layer** : This layer tokenizes the words according to their frequency, which is necessary for transforming the words into a format suitable for processing by the neural network.
2. **Bidirectional LSTM Layers** : These layers capture dependencies in the sentence, allowing the model to understand the context from both directions (past and future) within the sentence.
3. **Dense Layer** : This layer has a positive effect on the accuracy of the deep learning model by enabling complex transformations and interactions within the data.
4. **Dropout Layer** : This layer reduces overfitting by randomly setting a fraction of input units to 0 at each update during training time, which helps to prevent the model from relying too much on any particular set of features.
    
![deepLearningModel](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/5ca11c43-4120-430c-b476-bb8461957fbf)

After the deep learning model is created, it is trained with 3 million valid sentences and 3 million invalid sentences.
    
![trainingResults](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/a638d9d2-853a-4b75-9a6d-89ca58758182)

The deep learning model is converted into TensorFlow.js format for use in the browser. Additionally, a user interface is created. When a user types a sentence ending with a punctuation mark ('!', '.', '?'), it automatically corrects each word. However, if the deep learning model is not confident about a word (with a prediction score difference of two sentences are less than 0.1), it underlines the word in orange and provides alternative options for the user to select when they right-click on it.

![userInterface](https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/6302acfa-26b9-446f-b5e3-eb2a55c4c2b5)

## Files and Folders

**finalDL** : Contains TensorFlow.js format of the deep learning model.

**presentations and report** : Contains presentations and report of the project.

**deepLearningModel.ipynb** : The code for creating and training the deep learning model.

**logo.png** : The logo of the plugin.

**manifest.json** : Manifest file of the plugin.

**tokens.txt** : Contains words and their tokens.

**words.txt** : Contains valid Turkish words.

## Preview

https://github.com/ecagri/ecagri-Turkish-Text-Corrector-Plugin/assets/101584509/eff97137-c5cd-4f6d-8f57-90944327ec1b


    
