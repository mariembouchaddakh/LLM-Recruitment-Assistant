# RecrutAI : Système d'Intelligence Artificielle pour le Filtrage et l'Évaluation de Candidatures

## Contexte du Projet (Recherche & Application Entreprise)
Le recrutement moderne fait face à un volume massif de candidatures (CVs), rendant le tri manuel chronophage et sujet aux biais cognitifs.
- **Aspect Recherche (NLP & LLM)** : Ce projet explore l'hybridation de techniques classiques d'extraction d'information (TF-IDF) avec des modèles de plongement sémantique denses (Sentence-BERT). Il intègre également une phase d'évaluation conversationnelle automatisée pilotée par un Large Language Model (LLaMA 3.3 70B) agissant comme un agent recruteur adaptatif.
- **Aspect Entreprise (HR Tech)** : Outil B2B conçu pour les départements Ressources Humaines (RH) et les cabinets de recrutement. Il automatise la phase de présélection (Screening) avec un haut degré de précision, réduisant le Time-to-Hire tout en augmentant la qualité des profils retenus via un score composite (Sémantique CV + Entretien Chatbot).

## Architecture et Stack Technologique
L'architecture est optimisée pour une faible latence et une évolutivité Cloud :
- **Vectorisation Lexicale** : `scikit-learn` (TF-IDF) pour la correspondance stricte de mots-clés.
- **Plongement Sémantique Denses** : `sentence-transformers` (`paraphrase-multilingual-MiniLM-L12-v2`) pour capturer le contexte et les analogies métiers (ex: "développeur" ≈ "ingénieur logiciel").
- **Agent Conversationnel (LLM)** : LLaMA 3.3 70B orchestré via l'API Groq (inférence ultra-rapide), permettant de générer des questions d'entretien adaptées dynamiquement au profil.
- **Interface Utilisateur (UI)** : Développée en Python via **Streamlit**, offrant des tableaux de bord interactifs et des analyses comparatives (Matplotlib).

## Flux d'Évaluation et Métriques
Le système calcule un score d'affinité composite robuste :
`Score Final = 0.4 * Score_SBERT_CV + 0.6 * Score_Entretien_LLM`

1. **Filtrage Sémantique** : Les CVs franchissant un seuil de similarité cosinus avec la fiche de poste sont retenus.
2. **Entretien Automatisé** : Le chatbot évalue la pertinence des réponses du candidat et attribue une note automatisée sur 10.

## Instructions d'Installation et d'Inférence

### Prérequis
- Python 3.10+
- Un compte Groq (API gratuite)

### Déploiement Local

1. **Cloner le dépôt** :
   ```bash
   git clone https://github.com/mariembouchaddakh/projetNLP.git
   cd projetNLP
   ```

2. **Installer les dépendances** :
   ```bash
   pip install -r requirements.txt
   ```

3. **Configuration de l'Agent LLM** :
   Dans le fichier `src/chatbot.py`, configurez votre clé API Groq via une variable d'environnement ou directement dans l'instanciation du client (à ne pas commiter).

4. **Lancer l'application Web** :
   ```bash
   streamlit run app.py
   ```
   L'interface de scoring et le chatbot seront accessibles sur `http://localhost:8501`.

### Tests en ligne de commande
Pour valider le pipeline NLP sans l'interface :
```bash
python test.py
```