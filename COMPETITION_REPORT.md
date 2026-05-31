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

The group trained a standardised 15-layer CNN architecture on the Fashion MNIST training set using the following configuration:

- Optimiser: SGDM, learning rate 0.01
- Data augmentation: resize to 28x28 pixels only
- Architecture: 3 stages of convolution, batch normalisation and ReLU, with max pooling after stages 2 and 3. Filter depth 8→16→32, followed by a fully connected layer (10 units), softmax, and classification output layer.

**Baseline test accuracy: 89.85%**

### Misclassification Analysis

The most commonly misclassified class was **Shirt**, which the model frequently confused with T-shirts, Coats, Dresses, and Pullovers. Five example misclassified images were identified from the test set:

| Image Index | True Class | Predicted Class |
|-------------|------------|-----------------|
| 41 | T-shirt | Shirt |
| 118 | Coat | Shirt |
| 148 | Dress | Shirt |
| 245 | Pullover | Shirt |
| 438 | Coat | Shirt |

This pattern reflects the visual similarity between flat garments when represented as 28x28 greyscale images, where texture and outline are the primary distinguishing features.

---

## Stage 2 — Optimised CNN (Group)

The group tuned the training configuration to improve generalisation. The optimised setup was re-run 5 times to obtain a stable average and standard deviation.

**Group optimised accuracy: 91.21% ± 0.18%**

### Parameter Choices and Justification

**Optimiser: Adam** — chosen over SGDM for its adaptive learning rate per parameter, leading to faster and more stable convergence.

**Mini-batch size: 256** — balances gradient stability with memory efficiency.

**Data augmentation** — random rotation (±5°) and translation (±2px) applied to simulate real-world variability and improve generalisation to unseen images.

**L2 Regularisation (0.0005)** — applied to penalise large weights and reduce overfitting risk.

**Learning rate schedule** — piecewise decay with a drop factor of 0.2 every 7 epochs, preventing the model from stalling at local minima.

MaxEpochs: 25 | ValidationFrequency: 50 | GradientThreshold: 2

After optimisation, image index 438 (previously misclassified as Shirt) was correctly classified.

---

## Stage 3 — Individual Custom Architectures

Each group member designed their own CNN architecture (maximum 25 layers) using the group's optimised training configuration from Stage 2.

### Enio Mecaj — 92.40% ± 0.06%

The standard architecture was extended by increasing filter depth from 8→16→32 to **32→64→128**, allowing the network to extract higher-level features such as textures and complex outlines. A **dropout layer** was introduced before the fully connected layer to prevent overfitting by forcing the network to learn distributed features rather than memorising individual pixel patterns. The max-pooling layer was removed to preserve higher spatial resolution for the final classification stage, which proved particularly helpful in distinguishing visually similar classes such as shirts and t-shirts.

Previously misclassified images now correctly classified: indices 41, 118, 438.

### Adrian Alimohammadi — 92.42% ± 0.15%

A 22-layer architecture built around 4 convolutional blocks, with filters scaled up to 256 to capture micro-details in clothing textures. A dropout layer (0.25) was added before the fully connected layer to prevent overfitting from the increased network capacity. Test-Time Augmentation (TTA) was also applied, averaging predictions across original and mirrored images to significantly boost prediction confidence.

### Kai (Nguyen Gia Hy Truong) — 93.43% ± 0.25%

A custom 23-layer architecture, chosen over the 15-layer baseline because the additional depth significantly increased accuracy. The number of filters was increased from 64 to 256 to capture much wider fine-grained details than the baseline's maximum of 32 filters, directly addressing the underfitting observed in earlier experiments.

### Ankit Sharma — 93.47% ± 0.19%

Architecture designed for progressive feature extraction, with early layers targeting fine details such as edges and textures, and deeper layers capturing larger structural patterns such as curves and garment shapes.

---

## Results Summary

| Member | Configuration | Accuracy |
|--------|--------------|----------|
| Baseline (Group) | Standard SGDM, 15-layer architecture | 89.85% |
| Optimised (Group) | Adam, augmentation, L2 regularisation | 91.21% ± 0.18% |
| Enio Mecaj | 32→64→128 filters, dropout, no max-pooling | 92.40% ± 0.06% |
| Adrian Alimohammadi | 4 conv blocks, filters to 256, dropout, TTA | 92.42% ± 0.15% |
| Kai (Nguyen Gia Hy Truong) | 23-layer, filters to 256 | 93.43% ± 0.25% |
| Ankit Sharma | Progressive feature extraction, 23 layers | 93.47% ± 0.19% |

---

## Ethical Considerations

The group assessed the ethical implications of deploying a system of this type in a real-world commercial setting, specifically a scenario where the trained CNN is applied to real-time CCTV footage in shopping centres to automatically identify clothing items worn by shoppers, with plans to extend to full colour 4K resolution and expanded categories to recommend trends to retailers.

### 1. Fairness — Bias and Discrimination

The Fashion MNIST dataset is Western-centric and does not include categories for religious or cultural garments such as hijabs, saris, or turbans. This means the system may misclassify or exclude certain demographics from trend analysis entirely.

Mitigation: Audit the dataset for cultural representation. Retrain with a more diverse global dataset before deployment.

### 2. Accountability — Who is Responsible?

If the system misidentifies a shopper, for example by falsely flagging someone based on their clothing, it is not clear who bears responsibility: the store operator, the AI developer, or the platform provider.

Mitigation: Establish a human-in-the-loop protocol where the AI only flags trends and never makes automated decisions about individuals. Developers must provide clear documentation of accuracy limits, for example that a 93% accurate system still misclassifies 7 in every 100 people.

### 3. Sustainability — Energy Consumption

Processing 4K video in real time across multiple CCTV feeds requires significant and continuous GPU compute power. The energy cost of scaling this system must be considered against its commercial benefit.

### 4. Transparency — Informed Consent

Shoppers entering a mall have not consented to having their clothing choices recorded, analysed, and used to inform retailer recommendations.

Mitigation: Clear signage informing customers that AI trend analysis is in use. Anonymisation of footage, such as face blurring, before the AI processes any frame.

---

## Key Takeaways

Increasing filter depth (32→64→128) enabled the network to learn finer feature representations, which was most impactful for distinguishing visually similar classes. Replacing L2 regularisation with dropout proved more effective in the individual architecture, as it forced the network to learn generalisable features rather than relying on weight penalisation. Removing max-pooling preserved spatial resolution that was critical for fine-grained classification at the output layer. The most persistent source of misclassification across all architectures was the Shirt class, reflecting the inherent difficulty of separating visually similar flat garments at 28x28 greyscale resolution.
