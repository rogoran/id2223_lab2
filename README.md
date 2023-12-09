Link to app: https://huggingface.co/Siphh


Work done in effort to improve model performance: 
(a) model-centric approach 


Default hyperparameters:

<img width="760" alt="Skärmavbild 2023-12-06 kl  10 21 50" src="https://github.com/rogoran/id2223_lab2/assets/98389590/5d7210e0-2ac1-4613-83be-188a3d60114e">

Baseline

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



(b) data-centric approach - identify new data sources that enable you to train a better model that one provided in the blog post

