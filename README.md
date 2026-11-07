# Irregularly Irregular

Can a smartwatch-style ECG catch atrial fibrillation?

AF is the most common heart rhythm disorder. It often has no symptoms, yet it raises stroke risk by around five times. Smartwatches record a single-lead ECG, so I wanted to see if that one lead is enough to spot it.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lamisahk/irregularly-irregular/blob/main/IrregularlyIrregular.ipynb)

## Data
[PhysioNet/CinC Challenge 2017](https://physionet.org/content/challenge-2017/1.0.0/): 8,528 single-lead ECGs, 9 to 60 seconds long, labelled normal, AF, other rhythm, or too noisy. AF is only 9% of the recordings.

## Part 1: rhythm features
I built a beat detector, measured how uneven the gaps between beats are, and trained two models with 5-fold cross-validation.

| Model | Challenge score | AF caught | AF specificity |
|---|---|---|---|
| Logistic regression | 0.616 | 81% | 0.924 |
| Gradient boosting | 0.745 | 73% | 0.975 |

The features the model relied on most (RMSSD, RR range, pNN50) all measure beat-to-beat irregularity, which is what cardiologists look for in AF.

It struggles with the "other rhythm" class and with noisy recordings, where the beat detector marks the wrong points. Beat timing also can't show missing P waves, the second sign of AF.

## Progress
- [x] Part 1: data exploration and baseline models
- [ ] Part 2: CNN on the raw ECG, with highlights showing what it looked at
- [ ] Part 3: interactive demo

## Reference
Clifford GD et al. AF Classification from a Short Single Lead ECG Recording: the PhysioNet/Computing in Cardiology Challenge 2017. *Computing in Cardiology*, 2017.
