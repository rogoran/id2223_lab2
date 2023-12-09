Link to app: https://huggingface.co/Siphh


Dataset used: 

50% of common voice swedish dataset: https://commonvoice.mozilla.org/sv-SE 


Default hyperparameters:

<img width="760" alt="Skärmavbild 2023-12-06 kl  10 21 50" src="https://github.com/rogoran/id2223_lab2/assets/98389590/5d7210e0-2ac1-4613-83be-188a3d60114e">

Result

| Step | Training Loss | Validation Loss | WER       |
|------|---------------|------------------|-----------|
| 1000 | 0.059500      | 0.327605         | 118.8067  |
| 2000 | 0.002400      | 0.421270         | 59.4952   |
| 3000 | 0.000800      | 0.440430         | 69.7147   |
| 4000 | 0.000500      | 0.447096         | 70.4064   |


We now want to improve the model performance which can be done in different ways. One could use a model-centric approach, or a data-centric.

## Model-centric: 

# Tune hyperparameters

From the baseline result we learn that with more steps:
- Training loss decreases
- Validation loss increases
- WER is initially very high, then hits its lowest value for 2000, and then increases again.

This means that the model probably overfits at some point around 2000.

To prevent the model overfitting, we tried to add weight decay because applying it to the parameters of your seq2seq model can help prevent overfitting and improve generalization performance. 
Loss function changes to the following: 

![Skärmavbild 2023-12-09 kl  15 37 37](https://github.com/rogoran/id2223_lab2/assets/98389590/550b4939-f837-4db7-a298-59fdb00841ec)
Hence preventing that certain weights affect the outcome too much. 

We also decreased the learning rate to prevent the weights to overshoot and miss the optimal values. This produced drastically worse results than the baseline which could be seen just after 2000 steps, and therefore the training was stopped. We tried again by only adding weight decay.

"Fine tuned" parameters:

![Skärmavbild 2023-12-09 kl  15 27 41](https://github.com/rogoran/id2223_lab2/assets/98389590/bb88d4b6-ed2e-4eb0-a3b0-77b2eb71d3bc)

Result

| Step | Training Loss | Validation Loss | WER       |
|------|---------------|------------------|-----------|
| 1000 | 0.059600      | 0.326396         | 111.4624  |
| 2000 | 0.006700      | 0.386743         | 86.8785   |
| 3000 | 0.001300      | 0.408694         | 84.5223   |
| 4000 | 0.000900      | 0.418169         | 88.0566   |

Unfortuntaley, this did not result in a desired outcome as validation loss keeps increasing and WER values are too high. This may be due to weight decay being too small hence not hjaving the desired effect. Another possible explanation is that the amount of data we used is not sufficient for the complexity of the model. We may have gotten better result by using a less complex model but unfortunately was limited due to time constraints.

# Modify model architecture
Fine-tuning can be done through modification of the model architecture which can be done by removing or adding layers, changing the number of nodes in a layer etc. In our case we would like to try reducing the amount of layers, or units per layer, to test if the complexity of the model is causing the overfitting, or perhaps change to a smaller model.

Adjusting the model architecture requires a deeper understanding of the current transformer architecture. As time and computation power were constraints for us we focused on tuning the hyperparameters instead.


## Data-centric approach - identify new data sources that enable you to train a better model that one provided in the blog post

The following paper evaluated how data from L2 speakers affect the performance of a ASR model

Knowles, A., & Mattsson, F. (2022). Understanding Automatic Speech Recognition for L2 Speakers and Unintended Discrimination in Artificial Intelligence (Dissertation). Retrieved from https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-319360

The paper shows how retraining a model with data from L2 speakers improves the model performance (lower WER score). We identified these data sources since they are WAV files which can be encoded and used as training data for the Whisper model.

Using additional, but different data can make the model more nuanced due to the following factors: 

Diversity of Speech Patterns:
- L2 speakers often exhibit diverse speech patterns, including different accents, intonations, and pronunciation variations compared to native speakers.
- Adding data from L2 speakers can help the ASR model become more robust and adaptable to a wider range of speech styles and linguistic characteristics.
  
Improved Generalization:
- By incorporating data from L2 speakers, the ASR model may improve its ability to generalize across different linguistic backgrounds.
- This helps the model to better handle variability in pronunciation and linguistic nuances that may not be present in the training data consisting solely of native speakers.

Reducing Bias and Discrimination:
- Training an ASR model solely on data from native speakers may lead to biases and discrimination against non-native speakers.
- Including data from L2 speakers can help mitigate such biases and promote fairness in the model's performance across diverse user groups.

Domain Adaptation:
- L2 speakers may use the language in different contexts or domains compared to native speakers.
- Retraining the model with data from L2 speakers helps it adapt to the specific characteristics of the target user group, potentially leading to better performance in real-world scenarios.

Increased Vocabulary Coverage:
- L2 speakers may use a broader vocabulary or different terminology than native speakers.
- Incorporating data from L2 speakers can enhance the model's vocabulary coverage, making it more effective in recognizing a wider range of words and phrases.

However, it's important to note that the effectiveness of retraining with L2 speaker data depends on various factors, including the quality and quantity of the added data, the initial model architecture, and the characteristics of the target user population. The specific insights from the paper you mentioned would provide more context and details regarding the observed improvements in ASR performance for L2 speakers.

The paper used datasets Ville (~2 hours of labeled speech) and Språkcafé (unknown length). We tried to contact the authors to retrieve the data but to no success.

