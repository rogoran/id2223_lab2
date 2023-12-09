Link to app: https://huggingface.co/Siphh


Dataset used: 

50% of common voice swedish dataset: https://commonvoice.mozilla.org/sv-SE 

Work done in effort to improve model performance: 
(a) model-centric approach 


Default hyperparameters:

<img width="760" alt="Skärmavbild 2023-12-06 kl  10 21 50" src="https://github.com/rogoran/id2223_lab2/assets/98389590/5d7210e0-2ac1-4613-83be-188a3d60114e">

Result

| Step | Training Loss | Validation Loss | WER       |
|------|---------------|------------------|-----------|
| 1000 | 0.059500      | 0.327605         | 118.8067  |
| 2000 | 0.002400      | 0.421270         | 59.4952   |
| 3000 | 0.000800      | 0.440430         | 69.7147   |
| 4000 | 0.000500      | 0.447096         | 70.4064   |


From the baseline result we learn that with more steps:
- Training loss decreases
- Validation loss increases
- WER is initially very high, then hits its lowest value for 2000, and then increases again.

This means that the model probably overfits at some point around 2000.

To prevent the model overfitting, we tried to add weight decay because applying it to the parameters of your seq2seq model can help prevent overfitting and improve generalization performance. 
Loss function changes to the following: 

![Skärmavbild 2023-12-09 kl  15 37 37](https://github.com/rogoran/id2223_lab2/assets/98389590/550b4939-f837-4db7-a298-59fdb00841ec)
Hence preventing that certain weights affect the outcome too much. 


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

(b) data-centric approach - identify new data sources that enable you to train a better model that one provided in the blog post

Unfortunately we couldn't access any new data sources, but we would like to try this dataset:
HÄMTA LÄNK TILL ALFREDS

We believe this data could improve the model since it Swedish
