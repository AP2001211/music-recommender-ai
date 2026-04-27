# 🎧 Explainable & Reliable Music Recommender

## 🔹 Summary
This project extends the **Music Recommender Simulation (Module 3)** into a full **end-to-end AI system** that generates personalized music recommendations with **explanations, confidence scores, and reliability checks**.

The system retrieves relevant songs from a large Spotify dataset, ranks them using interpretable audio-feature scoring, and applies guardrails to ensure trustworthy outputs.

Unlike black-box recommenders, every recommendation is **traceable and explainable**.

---

## 🔹 Original Project (Module 3)
The original project implemented a basic music recommendation system that:
- Took a user “taste profile”
- Compared it to song features
- Returned top recommendations

However, it lacked:
- structured retrieval
- explanation of decisions
- reliability checks
- evaluation framework

This project extends it into a **complete applied AI system**.

---

## ⚙️ Core Components

### Retriever
- Filters songs by genre, energy, mood, and explicit content
- Reduces large dataset into relevant candidates

### Ranker
Scores songs using:
- genre match
- mood match
- energy similarity
- valence similarity
- danceability similarity
- acoustic preference
- favorite artist bonus

### Recommender
- Orchestrates pipeline
- Applies diversity constraint (max 2 per genre)
- Generates explanations and confidence scores

### Guardrails
Detects:
- low-confidence recommendations
- lack of diversity  
Provides warnings to the user

---

## 📊 Dataset
- ~89,740 songs (Spotify dataset)
- 31k+ unique artists
- 14 genre groups (from 114 raw genres)
- 7 derived moods based on valence + energy

---

## 🚀 Setup Instructions

### 1. Install dependencies
```
pip install pandas streamlit pytest
```

### 2. Run CLI Demo
```
python -m src.main
```

### 3. Run Unit Tests
```
pytest
```

### 4. Run Evaluation Script
```
python evaluation/evaluate_profiles.py
```

---

## 💡 Sample Interactions

### Example 1: Pop Energetic User

**Input**
```
Genre: pop
Mood: happy
Energy: 0.8
```

**Output**
- High-confidence recommendations (~85%)
- All songs match genre + mood
- Guardrail warning: low diversity (expected for focused taste)

---

### Example 2: Sparse Input User

**Input**
```
No genre or mood preference
```

**Output**
- Diverse recommendations across multiple genres
- Lower confidence (~30%)
- No guardrail warnings

---

## 🧪 Testing & Evaluation

### Unit Testing
34 pytest tests covering:
- genre mapping
- mood derivation
- retrieval logic
- scoring correctness
- guardrails

### Evaluation Script

We implemented an evaluation harness (`evaluation/evaluate_profiles.py`) to simulate real users.

**It measures:**
- average confidence
- genre diversity
- duplicate detection
- guardrail behavior

### Results
- 4/5 profiles passed  
- The exploration-focused profile failed due to limited diversity in retrieval  

---

## 📈 Design Decisions

### Two-stage pipeline (retrieve → rank)
Improves scalability and performance for large datasets.

### Interpretable scoring (not black-box ML)
Chosen for:
- transparency  
- explainability  
- easier debugging  

### Diversity constraint
Prevents repetitive recommendations and improves user experience.

### Confidence scoring
Helps users understand how reliable each recommendation is.

---

## ⚠️ Limitations & Biases

- Strong genre filtering can reduce diversity  
- Discovery preference affects ranking but not retrieval strongly enough  
- No real user feedback loop  
- Dataset bias toward popular genres (pop, electronic)  

---

## 🔐 Responsible AI Considerations

### Safeguards
- Explicit content filtering  
- Transparent explanations  
- Confidence scores to indicate uncertainty  

### Potential Misuse
- Over-reliance on automated recommendations  

### Mitigation
- Provide explanations and guardrail warnings  

---

## 🤖 Reflection

### What surprised me
Even with a discovery boost in ranking, recommendations remained narrow because retrieval filtered too aggressively. This showed that pipeline design impacts results more than scoring logic alone.

### AI Collaboration
- Helpful: AI suggested modularizing the system into retriever, ranker, and recommender components  
- Flawed: AI initially suggested overly strict evaluation criteria, causing valid outputs to fail  

---

## 🔮 Future Improvements

### High-impact improvements
- Improve retrieval for high-discovery users  
- Add feedback loop (thumbs up/down)  
- Add conversational input (“something chill but upbeat”)  

### Advanced extensions
- Add RAG (e.g., artist metadata or lyrics)  
- Add LLM-based explanation refinement  
- Add adaptive learning of user preferences  

---

## 🎥 Demo

Loom walkthrough: *(add your link here)*

---

## 💼 Portfolio Reflection

This project demonstrates my ability to:
- design modular AI systems  
- implement retrieval + ranking pipelines  
- build explainable and reliable AI outputs  
- evaluate system behavior with structured testing  

It reflects my interest in building trustworthy AI systems, not just functional ones.
