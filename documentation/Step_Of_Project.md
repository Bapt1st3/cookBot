# Recipe Chatbot Development Plan

## 1. Data Preparation and Cleaning
Since your dataset already includes information like `title`, `ingredients`, `directions`, `link`, `source`, and `NER` (list of ingredients), the first step is ensuring the data is clean and organized for querying. You’ll need to:

- **Parse ingredients**: Ensure the `ingredients` and `NER` fields are normalized so that ingredients are comparable (e.g., handle cases like "tomato" vs. "tomatoes").
- **Categorize diets/allergies**: Create categories or tags for common dietary preferences (e.g., vegan, vegetarian, gluten-free) and allergies (e.g., nut-free, dairy-free).
- **Taste preferences**: If the dataset doesn’t have explicit taste tags (spicy, sweet, savory), you can manually assign these based on the recipe's ingredients or look into using a machine learning model to predict them.

## 2. Core Features of the Chatbot

### Ingredient-based Recipe Suggestions
Users input the ingredients they have, and the chatbot suggests recipes that use these ingredients.
- Use a simple **search/match algorithm** that compares user input with the `ingredients` field in the dataset to suggest matching recipes.
- If some ingredients are missing from the user's input but are required by a recipe, the bot could mention those and suggest substitutions.

### Allergy and Dietary Restrictions
Users specify their dietary needs (e.g., vegan, gluten-free) or allergies (e.g., nut-free), and the chatbot ensures that the recommended recipes comply.
- You’ll need to build a filter that checks for these conditions against the `NER` or `ingredients` fields.
- Create a mapping of common ingredients that are allergens (nuts, gluten-containing grains, dairy) and ensure recipes containing them are excluded based on user preferences.

### Taste Preference Matching
Users input their taste preferences (e.g., sweet, spicy), and the chatbot suggests suitable recipes.
- Add tags for taste categories to your dataset (either manually or using natural language processing techniques) or use ingredients (e.g., chili peppers for spicy, honey for sweet) as a proxy for taste preferences.

## 3. Workflow of the Chatbot

1. **User Interaction**: Users input their preferences, such as ingredients on hand, dietary restrictions, allergies, and taste preferences.
2. **Querying the Dataset**:
   - **Ingredients Matching**: Query the dataset for recipes that match the user's ingredients list.
   - **Filter by Preferences**: Ensure that the recipes align with user preferences, such as vegan, gluten-free, or nut-free.
   - **Taste Matching**: Use a simple rule-based matching for taste preferences or leverage a more complex classification model if needed.
3. **Recipe Recommendation**: Suggest a list of recipes that match user input. Return the title, ingredients, directions, and link if available.

## 4. Tech Stack and Development Plan

### Backend:
- **Python & Pandas**: For managing and querying the recipes dataset.
- **FastAPI / Flask**: For creating the backend API to serve chatbot responses.
- **Scikit-learn (optional)**: To build simple classifiers or use NLP-based approaches for categorizing recipes by taste, ingredients, or diet.

### Frontend:
- **Rasa / Botpress / Microsoft Bot Framework**: Use one of these chatbot frameworks to create the interactive part of the bot.
- **Natural Language Processing (NLP)**: Use NLP libraries like `spaCy` or `Transformers` (from HuggingFace) to better understand user queries related to dietary restrictions or taste preferences.

### Database:
- **SQLite / PostgreSQL**: Store the recipe dataset, especially if you plan on extending this dataset with more user-generated data.

### Steps:
1. **Data Preparation**: Clean and tag the recipe dataset.
2. **Querying Recipes**: Write functions that query the dataset based on user input.
3. **Allergy & Diet Filters**: Build filtering logic to exclude recipes that don't fit user preferences.
4. **Taste Matching**: Add a feature to match taste preferences to recipes.
5. **Frontend Development**: Use a chatbot framework (e.g., Rasa) to build the user interface.
6. **Integrate the API**: Connect the recipe querying backend to the chatbot.

## 5. Example Code for Ingredient Matching

Here’s a basic idea of how you could implement the core recipe search based on ingredients:

```python
import pandas as pd

# Load your dataset (assuming it's already cleaned)
df = pd.read_csv("recipes.csv")

def find_recipes_by_ingredients(available_ingredients, diet=None, allergies=None):
    """
    Find recipes that match the user's available ingredients, diet, and allergies.
    """
    def matches_ingredients(recipe_ingredients, user_ingredients):
        recipe_ingredients_set = set(recipe_ingredients.split(','))
        user_ingredients_set = set(user_ingredients)
        return user_ingredients_set.issubset(recipe_ingredients_set)

    # Filter by diet if specified
    if diet:
        df_filtered = df[df['diet'] == diet]
    else:
        df_filtered = df

    # Filter by allergies
    if allergies:
        for allergy in allergies:
            df_filtered = df_filtered[~df_filtered['ingredients'].str.contains(allergy, case=False)]

    # Find recipes that match the available ingredients
    matched_recipes = df_filtered[df_filtered['ingredients'].apply(lambda x: matches_ingredients(x, available_ingredients))]
    
    return matched_recipes[['title', 'ingredients', 'directions', 'link']]

# Example usage
available_ingredients = ['tomato', 'onion', 'garlic']
diet = 'vegan'
allergies = ['nuts']

recipes = find_recipes_by_ingredients(available_ingredients, diet, allergies)
print(recipes)
