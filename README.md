# Themis – Sentiment Score Prediction Model (TRACE++ Architecture)

This repository contains **Sentiment Analysis 1.0**, the first version of the AI model used to predict employee sentiment inside the Themis HR system.

This version combines **structured behavioral data** and **textual feedback** to produce a sentiment class from 0 to 4. It is the core emotional intelligence layer that influences other downstream models like attrition risk, performance prediction, and role fitting.

>  **Note:** A future version (**Sentiment Analysis 2.0**) is planned, which will integrate real-time action images to enhance emotional recognition and improve prediction precision and usability in live enterprise environments.

---

##  Model Overview

The model is built on a dual-branch architecture known as **TRACE++**, an evolved version of the TRACE framework. It combines:

- A **Transformer + Autoencoder branch** for structured simulated behavior
- An **LSTM branch** for analyzing employee-written comments
- A **Fusion MLP** that joins both latent representations and outputs a softmax score

---

## Structured Branch (Transformer + Autoencoder)

Processes features like:
- Attendance behavior
- Hours present
- Interaction frequency
- Conflict counts
- Movement type and sitting posture
- Break and wandering time
- Collaboration and stress scores (derived)

### Why Transformer?
To learn complex interdependencies between behavioral signals without relying on manual weighting.

### Why Autoencoder?
To compress and denoise the attention-encoded feature space before classification, improving generalization.

---

##  Textual Branch (LSTM)

Processes written comments, complaints, feedback, or praises from employees.

### Why LSTM?
It understands the sequential and contextual structure of text, capturing tone, intent, and sentiment over time.

---

##  Fusion and Classification

The latent vectors from both branches are concatenated and passed through:

- Dense(64) → ReLU  
- Dropout(0.3)  
- Dense(32) → ReLU  
- Output: **Softmax over 5 sentiment classes** (0–4)

---

##  Output

The model outputs a single value:
- `0`: Extremely Negative  
- `4`: Extremely Positive

This score is used in:
-  Attrition Risk Prediction  
-  Performance Scoring  
-  Role Fit Recommendation (TBU)



## FEATURES

A. Structured (Transformer Branch)
base_salary	Current salary
num_raise_requests	Raise requests submitted
num_appraisals	Evaluations received
num_benefits	Assigned benefits
num_penalties	Penalties on record
past_performance_score	Output from performance model
skills	Number of verified skills
cost_of_training	Financial cost of training
has_training	Whether training exists (bool)
attrition_risk	Predicted risk score (0–3)
age, marital_status	Demographic features (one-hot encoded)

🔹 B. Simulated Behavior Metrics
hours_present_per_day, workstation_time	Time tracking
meetings_attended, break_time	Engagement indicators
stress_level	Derived from attrition and penalties
movement_type, sitting_posture	Workplace behavior patterns
total_num_of_interactions	Comment count, feedback frequency
num_conflicts_involved	Disciplinary records
collaboration_score	Computed from task completion & group work
negative_body_language_signal_score	Simulated metric
positive_body_language_signal_score	Simulated metric



🔹 C. Textual (LSTM Branch)
comments Free-form employee-written text (collected from the platform)

1. Output Format:
{
  "sentiment_score": 3
}
•	Integer between 0 and 4 indicating overall sentiment class


---

##  Roadmap

> **Sentiment Analysis 2.0** will introduce:
- Real-time live action image input
- Emotion recognition from video/posture
- Multimodal fusion for enhanced workplace insight

---

##  Credits

Developed by **ME** as part of the **Themis AI Engine**, fusing behavioral intelligence with emotion-aware prediction to drive smarter HR decisions.

