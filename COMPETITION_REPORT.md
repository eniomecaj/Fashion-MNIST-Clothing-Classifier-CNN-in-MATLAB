# AI Competition Report Summary — Group B

MSc Artificial Intelligence Architectures (EG4227/EG7227) | University of Leicester, 2025–26

## Group Members

| Name | Username |
|------|----------|
| Enio Mecaj | em591 |
| Ankit Sharma | as1778 |
| Kai (Nguyen Gia Hy Truong) | nght1 |
| Adrian Alimohammadi | ma1163 |

---

## Stage 1 — Baseline CNN (Group)

The group first trained a standardised CNN architecture on the Fashion MNIST training set using the following configuration:

- Optimiser: SGDM, learning rate 0.01
- Data augmentation: resize to 28x28 pixels only

**Baseline test accuracy: 89.85%**

The most commonly misclassified class was **Shirt**, with the model frequently confusing it with T-shirts, Coats, Dresses, and Pullovers — all visually similar flat garment categories.

---

## Stage 2 — Optimised CNN (Group)

The group then tuned the training configuration to improve generalisation. The optimised setup was re-run 5 times to obtain a stable average and standard deviation.

**Group optimised accuracy: 91.21% ± 0.18%**

### Key parameter choices

**Optimiser: Adam** — chosen over SGDM for its adaptive learning rate per parameter, leading to faster and more stable convergence.

**Mini-batch size: 256** — balances gradient stability with memory efficiency.

**Data augmentation** — random rotation (±5°) and translation (±2px) applied to simulate real-world variability and improve generalisation to unseen images.

**L2 Regularisation (0.0005)** — applied to penalise large weights and reduce overfitting risk.

**Learning rate schedule** — piecewise decay with a drop factor of 0.2 every 7 epochs, preventing the model from stalling at local minima.

MaxEpochs: 25 | ValidationFrequency: 50 | GradientThreshold: 2

One of the five previously misclassified images (index 438) was correctly classified after optimisation.

---

## Stage 3 — Individual Custom Architectures

Each group member designed their own CNN architecture (maximum 25 layers) using the group's optimised training configuration from Stage 2.

### Enio Mecaj — 92.40% ± 0.06%

The standard architecture was extended by increasing filter depth from 8→16→32 to **32→64→128**, allowing the network to extract higher-level features such as textures and complex outlines. A **dropout layer** was introduced before the fully connected layer to prevent overfitting by forcing the network to learn distributed features rather than memorising individual pixel patterns. The max-pooling layer was removed to preserve higher spatial resolution for the final classification stage, which proved particularly helpful in distinguishing visually similar classes such as shirts and t-shirts. Correctly classified 3 of the 5 previously misclassified images (indices 41, 118, 438).

---

## Results Summary

| Stage | Configuration | Accuracy |
|-------|--------------|----------|
| Baseline (Group) | Standard SGDM architecture | 89.85% |
| Optimised (Group) | Adam, augmentation, L2 reg | 91.21% ± 0.18% |
| Enio Mecaj (Individual) | 32→64→128 filters, dropout | 92.40% ± 0.06% |

---

## Key Takeaways

Increasing filter depth (32→64→128) enabled the network to learn finer feature representations, which was most impactful for distinguishing visually similar classes. Replacing L2 regularisation with dropout proved more effective in Enio's architecture, as it forced the network to learn generalisable features rather than relying on weight penalisation alone. Removing max-pooling preserved spatial resolution that was critical for fine-grained classification at the final layer.
