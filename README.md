# Food-Recommendation

## Dataset Generation
First, a simulated dataset of 100,000 food orders is generated using the Faker library. Each order includes a customer ID, order date, a main food item from categories like Pizza, Burger, or Pasta, and a random quantity. The total price is calculated based on a price range for each food category and the quantity.

The script then randomly adds complementary items—a drink, side, starter, or dessert—based on a set probability for each category:

Drink: 60% chance of being added.

Side: 50% chance of being added.

Starter: 40% chance of being added.

Dessert: 30% chance of being added.

After generating the orders, the data is structured into a pandas DataFrame. Additional features are then created to enrich the dataset:

Time-based features: The hour of the day, day of the week, and whether the order was placed on a weekend are extracted from the OrderDate.

Customer-level features: The number of past orders and the average spending for each customer are calculated.

## Recommendation Models
The document explores three different methods for generating recommendations:

1. Item-Based Collaborative Filtering (Item-CF) 
This method finds relationships between items by analyzing what people typically buy together. The process is as follows:

Transaction Matrix: A binary matrix is created where each row represents a transaction (an order), and each column represents an item (e.g., 'Pepperoni Pizza,' 'Coke,' 'Fries'). A "1" indicates the item was in the order, and a "0" indicates it was not.

Cosine Similarity: The similarity between every pair of items is calculated using cosine similarity. This measures how often items appear together in the same orders.


Recommendations: To recommend items for a main item (e.g., 'Margherita' pizza), the model finds the items with the highest similarity scores and suggests them as complementary items.



Example: The model recommends 'Orange Juice,' 'Garlic Bread,' 'Spring Rolls,' 'Brownie,' 'Fries,' and 'Coke' for a Margherita pizza.

## 2. Random Forest Classifier 
This approach uses a machine learning model to predict which complementary items a customer is likely to purchase.


Features: The model is trained on features like the MainItem, Hour, DayOfWeek, and IsWeekend. These features are one-hot encoded to be used by the model.


Target: The target variable is the set of complementary items in each order. Since multiple items can be present, a 

MultiLabelBinarizer is used to handle this.


Model: A MultiOutputClassifier with a RandomForestClassifier is used, which is suitable for predicting multiple target labels at once.


Training and Prediction: The model is trained on a portion of the data (X_train, Y_train). When a new 


main_item is given, the model predicts the probability of each complementary item being chosen.

Example: The model recommends 'Lemonade,' 'Fries,' 'Coke,' 'Pepsi,' 'Garlic Bread,' and 'Water' for a Margherita pizza.

## 3. XGBoost Classifier (Optional) 
This section introduces an alternative to the Random Forest model using XGBoost, a powerful gradient-boosting algorithm.


Setup: The process is similar to the Random Forest model, using a MultiOutputClassifier with an XGBClassifier.


Training and Prediction: The model is trained on the same features and target variables as the Random Forest model. It then predicts the probability of each complementary item for a given main item.


Example: The model recommends 'Water,' 'Coke,' 'Pepsi,' 'Onion Rings,' 'Garlic Bread,' and 'Orange Juice' for a Margherita pizza.

All three models provide different, but valid, recommendations, demonstrating various approaches to solving the same problem.
