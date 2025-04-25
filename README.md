# 🎧 Mood-Driven User Behavior Analysis in a Music Streaming App

This project analyzes the listening patterns and behaviors of users in a music streaming app, focusing on identifying **factors that distinguish churned users from upgraded users**. The dataset initially consisted of over **26 million records** and was around **12GB** in size.

---

## 🧠 Project Objective

The main goal was to explore whether **music mood preferences** can provide insight into **user retention and upgrade behavior**. By analyzing user activity logs and the emotional tone of songs, we aimed to discover patterns that might predict:

- Who is more likely to **churn** (downgrade from paid to free)
- Who is more likely to **upgrade** (free to paid)

---

## ⚙️ Methods & Process

1. **Data Cleaning & Reduction**
   - Removed a user with corrupted registration data (~778K rows).
   - Filtered unnecessary rows and columns to reduce size for processing.

2. **Mood Extraction (Multiple Strategies)**
   - Used **Spotify API** to fetch track audio features (limited success).
   - Explored lyric-based sentiment using **VADER** on `spotify_millsongdata`.
   - Integrated song metadata from large sources like **Wasabi** and **Spotify 1M**.
   - Cleaned and matched titles using regex, casing, and keyword filtering.
   - Where APIs and lyrics failed, we leveraged **GPT** to manually classify batches of songs (~80k unmatched entries split into files).

3. **User Mood Profiling**
   - Aggregated mood counts per user (happy, sad, neutral).
   - Users were grouped as **churned** or **upgraded** based on subscription level changes and confirmation via page clicks.

4. **Normalization and Labeling**
   - Developed a custom heuristic: if mood differences were under 6%, assign "neutral", otherwise assign dominant mood.
   - This step was controversial but allowed categorization in ambiguous cases.

---

## 📊 Final Insights

After normalization and visualization:
- **Neutral** was the dominant category in most user profiles.
- While the idea was promising, **mood alone wasn’t a strong enough differentiator** between churn and upgrade behavior.
- However, the process highlighted the **potential and limits** of music-based emotional profiling.

---

## 🧩 Challenges

- **API Limitations**: Spotify’s API imposed strict rate limits; Gemini API failed on large batches.
- **Dataset Size**: The Wasabi dataset was **4.4GB**, making it difficult to load and filter.
- **Noisy Data**: Title variations (remixes, live versions, etc.) made matching difficult.
- **Manual Work**: GPT had to be used manually for many mood classifications.

---

## 📂 Datasets Used

- 🎧 **User Logs Dataset**:  
  [Customer Churn Dataset – Kaggle](https://www.kaggle.com/datasets/joy11117/customer-churn-dataset)

- 📝 **Lyric-Based Mood Dataset**:  
  [Spotify Million Song Dataset – Kaggle](https://www.kaggle.com/datasets/notshrirang/spotify-million-song-dataset?select=spotify_millsongdata.csv)

- 🎼 **Spotify Audio Features Dataset**:  
  [Spotify 1M Tracks – Kaggle](https://www.kaggle.com/datasets/amitanshjoshi/spotify-1million-tracks)

- 📁 **Large Metadata Dataset**:  
  [Wasabi Dataset – GitHub](https://github.com/micbuffa/WasabiDataset)

---

## 💡 Future Work

- Integrate **user demographics** and **time-based patterns** for richer modeling.
- Use **machine learning** to correlate mood profiles with upgrade probability.
- Explore **sequence modeling** of song moods and transition patterns.

---

## 📬 Feedback & Contributions

This project was built as a solo analytical deep-dive. I'm open to ideas, improvements, or extensions — feel free to fork or message with suggestions!

