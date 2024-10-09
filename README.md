# Recipe Chatbot using RecipeNLG Dataset

This is a personal Python project that utilizes the RecipeNLG dataset from Kaggle to create an intelligent recipe recommendation chatbot. The chatbot can assist users by suggesting recipes based on their preferences, allergies, dietary restrictions, and available ingredients.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Dataset](#dataset)
3. [Features](#features)
4. [Technologies](#technologies)
5. [Installation](#installation)
6. [Usage](#usage)
7. [Contributing](#contributing)
8. [License](#license)

## Project Overview

The goal of this project is to build a conversational AI that helps users find recipes based on various inputs such as:
- Taste preferences
- Allergies (e.g., nut-free, gluten-free)
- Dietary restrictions (e.g., vegetarian, vegan, keto)
- List of available ingredients

This project will leverage machine learning models to understand user inputs, recommend relevant recipes, and ensure the chatbot can interact naturally through text.

## Dataset

We are using the [RecipeNLG](https://www.kaggle.com/datasets/paultimothymooney/recipenlg) dataset from Kaggle. This dataset contains a large number of cooking recipes with structured ingredients, cooking methods, and detailed instructions.

- **Source**: Kaggle
- **Link**: [RecipeNLG](https://www.kaggle.com/datasets/paultimothymooney/recipenlg)
- **Dataset Description**: RecipeNLG is a high-quality dataset with over 2 million recipes designed for Natural Language Generation tasks but is also highly useful for recommendation systems and conversational AI.

## Features

- **Recipe Recommendation**: Suggests recipes based on the user's dietary preferences, allergies, or specific cuisine types.
- **Ingredient-Based Search**: Users can input the ingredients they have, and the chatbot will return recipes that can be made using those ingredients.
- **Allergy and Diet Awareness**: Ensures that recipes recommended adhere to specified allergies (e.g., nut-free) or diets (e.g., vegan).
- **Taste Profile**: Users can input taste preferences (e.g., spicy, sweet), and the chatbot will recommend suitable recipes.

## Technologies

Here is a list of technologies that will be used in the project:

- **Python**: The core programming language for the chatbot and data processing.
- **Natural Language Processing (NLP)**: For understanding user inputs and generating relevant responses.

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/recipe-chatbot.git
   cd recipe-chatbot

   libraries to install 
   keras
   tensorflow
   pandas
   seaborn
   scikit-learn
