# Easy-to-read: Dialogue Format in Micro-stories

## Project Overview

This project focuses on the automatic conversion of dialogues in micro-stories into **Easy Reading** format using Natural Language Processing (NLP) techniques. Easy Reading is a methodology that adapts texts to make them more comprehensible for people with cognitive disabilities, learning difficulties, elderly individuals, and people with visual impairments.

## Objectives

The main objective of this Final Degree Project is to investigate the possibility of implementing a function that converts dialogues into an Easy Reading version in micro-stories. This conversion is primarily based on dialogue reorganization to facilitate comprehension.

## Background

Easy Reading methodology consists of guidelines and recommendations applied to texts to facilitate their understanding without losing information in the process. These guidelines were first published in 1997 by the European Commission in the document "Making Information Accessible to All."

The Spanish documentation used as reference is "Lectura fácil: Métodos de redacción y evaluación" (Easy Reading: Writing and Evaluation Methods), developed by the Government of Spain in 2010 and updated in 2018.

## Methodology

### Natural Language Processing Approach

The project utilizes NLP techniques, specifically using the **spaCy** library with the Spanish large model. The pipeline includes:

- Text preprocessing
- Tokenization
- Part-of-speech tagging
- Named entity recognition
- Dependency analysis

<img src="imagenes/FasesNLP.drawio.png" width="500">

### Dialogue Structure Analysis

The project identifies two main dialogue structures:

1. **Dialogues with narrative tags (incisos)**: Include narrator clarifications identifying the speaker
2. **Dialogues without narrative tags**: Lack clear speaker identification

Example of dialogue transformation:

```
BEFORE: —¡Bruno, te he dicho que subas y deshagas las maletas ahora mismo! —le ordenó la Madre.

AFTER: La Madre le ordenó:
       ¡Bruno, te he dicho que subas y deshagas las maletas ahora mismo!
```


## Implementation

### Case 1: Dialogues with Narrative Tags

**Approach:**

- Extract the speaker from the narrative tag using dependency analysis
- Identify the subject using noun chunks functionality from spaCy
- Restructure the sentence placing the speaker first, followed by the verb, and then the dialogue

<img src="imagenes/Caso 1.png" width="500">

**Process:**

1. Detect dialogues in the text using dashes (—) and hyphens (–)
2. Separate the dialogue into speech and narrative tag components
3. Extract the verb and subject from the narrative tag
4. Reconstruct the sentence in Easy Reading format

### Case 2: Dialogues without Narrative Tags

This case presents the greatest difficulty as there's no explicit speaker identification. Three approaches were implemented:

#### First-person Dialogues

- Automatically detect first-person verb forms
- Convert to "Yo" (I) or "Nosotros" (We) as speakers


#### Method 1: Name Search

- Search for proper names in the three sentences preceding the dialogue
- Select the most recent name as the likely speaker


#### Method 2: Deep Learning Approach

- Utilize GPT-3.5-turbo model to identify the omitted subject
- Provide context from previous sentences to the AI model

<img src="imagenes/Caso 2 Metodo 1.png" width="500">
<img src="imagenes/Caso 2 Metodo 2.png" width="500">


## Results and Performance

### Case 1 Performance

- **Accuracy**: 98.64% in subject detection
- **Success Rate**: 95.93% in dialogue conversion
- Total dialogues analyzed: 663 from "The Boy in the Striped Pajamas"

### Case 2 Performance

**Method 1 (Name Search):**

- Success Rate: 38.10%
- Error Rate: 61.90%

**Method 2 (Deep Learning):**

- Success Rate: 76.19%
- Error Rate: 23.81%

## Testing and Validation

The project was extensively tested using:

- "The Boy in the Striped Pajamas" (El niño con el pijama de rayas)
- Collection of 50 popular short stories
- Various micro-stories and children's literature

All results were manually verified due to the semantic nature of the transformations, ensuring accuracy in dialogue conversion quality.

## Technical Specifications

- **Programming Language**: Python
- **Main Library**: spaCy (Spanish large model)
- **AI Model**: GPT-3.5-turbo for advanced cases
- **Input Format**: Plain text (.txt files)
- **Processing**: Rule-based approach combined with machine learning


## Easy Reading Guidelines Implementation

The project follows official Easy Reading guidelines for dialogues:

- Use dashes or hyphens to initiate dialogues
- Introduce the speaker's name narratively
- Format as theatrical dialogue with speaker names in capitals
- Indent dialogue text to differentiate from narration


## Limitations and Challenges

- Complex syntactic structures may cause model confusion
- Compound verbs (perífrasis verbales) can lead to incorrect categorizations
- PDF and DOCX processing requires additional line break handling
- Manual verification needed for semantic accuracy assessment


## Future Work

1. **Extended Format Support**: Implement handling for PDF and DOCX files
2. **Complexity Scaling**: Apply to novels and journalistic articles beyond micro-stories
3. **Model Enhancement**: Utilize newer NLP models as they become available
4. **Language Expansion**: Adapt methodology to other languages
5. **Integration**: Develop web-based tools for broader accessibility

## Social Impact

This project contributes to **universal accessibility** by improving text comprehension for:

- People with intellectual and cognitive disabilities
- Elderly individuals
- Foreign language learners
- Anyone with reading difficulties

The work aligns with the UN's Sustainable Development Goals 2030, specifically promoting inclusive education and reducing inequalities.

## Acknowledgments

- Universidad Politécnica de Madrid
- Escuela Técnica Superior de Ingenieros Informáticos
- Department of Artificial Intelligence (DIA)
- Supervisors: María del Carmen Suárez de Figueroa Baonza and Isam Diab Lozano

*This project was developed as part of the research line "Applied Artificial Intelligence: Improving Cognitive Accessibility" at Universidad Politécnica de Madrid, June 2023.*

<div style="text-align: center">⁂</div>

[^1]: TFG_INF_FINAL.pdf

