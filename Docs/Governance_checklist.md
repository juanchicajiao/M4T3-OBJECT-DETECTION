# AI Governance Checklist

## 1. Privacy and Consent

The dataset used in this project does not contain personal or sensitive data.  
Images correspond to construction environments and objects relevant to the detection task.

If publicly sourced data were used, they were obtained from datasets with open access licenses.

---

## 2. Data Minimization

Only the data strictly necessary for the object detection task were used.

The dataset contains:
- annotated images of construction elements
- bounding boxes for the objects of interest

No personal identifiers or unnecessary metadata were included.

---

## 3. Model Limitations

This model may perform poorly in the following situations:

- low lighting conditions
- unusual camera angles
- objects partially occluded
- environments not represented in the training dataset

The model should therefore not be used as the sole decision-making system in safety-critical scenarios.

---

## 4. Risk Considerations (False Negatives vs False Positives)

Two types of errors may occur:

False Negative (FN)  
The model fails to detect an object that is present.

False Positive (FP)  
The model detects an object that is not present.

In construction safety scenarios, false negatives may represent a higher risk since hazards could remain undetected.

---

## 5. Project License

This project is released under the MIT License.

The code can be reused, modified and distributed under the terms of the MIT license.

---

## 6. Dataset Rights

Dataset origin: [Specify here]

Options:
- Public dataset
- Proprietary dataset created for this project
- Licensed dataset

All dataset usage complies with the respective licensing terms.
