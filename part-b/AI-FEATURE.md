# AI Feature Proposal — Waitlist Confirmation Predictor

## Problem It Solves

Users booking waitlisted tickets do not know whether their tickets are likely to get confirmed.

---

# Model Choice

Model:

* XGBoost Classifier

Why:

* Works efficiently on structured/tabular railway booking data
* Fast prediction speed
* Lower infrastructure cost compared to deep learning models

---

# Training Data

Required Data:

* Historical waitlist bookings
* Route popularity
* Seasonal booking patterns
* Train class
* Final confirmation status

Data Sources:

* Historical IRCTC booking records
* Railway reservation datasets

---

# User Output

After booking a WL ticket:

“Your WL 14 ticket has a 78% chance of confirmation based on historical data.”

The system also provides:

* Updated predictions
* SMS notifications
* Alternative train suggestions

---

# Fallback Strategy

If prediction confidence is low:

* Show:
  “Insufficient historical data available for accurate prediction.”

Fallback:

* Standard PNR tracking continues normally.

---

# Benefits

* Reduces user anxiety
* Reduces repeated PNR checks
* Improves booking confidence
* Better travel planning experience
