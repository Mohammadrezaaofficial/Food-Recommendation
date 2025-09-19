# Food-Recommendation

This document describes the creation of a food recommendation system using a synthetic dataset and three different machine learning models. The system aims to recommend complementary food items (like drinks or sides) based on a main food item, while also considering contextual factors.

## Dataset Generation 📝
First, a synthetic dataset of 100,000 orders is created using the Faker library. Each order includes a MainItem (e.g., Pizza, Burger, Pasta) along with a randomized selection of complementary items such as a drink, side, starter, or dessert, which are added based on a set probability. The dataset also includes a CustomerID, OrderDate, quantity, and total_price.

To make the recommendations more context-aware, new features are added:

Time features: The hour of the day, day of the week, and whether the order was on a weekend (IsWeekend) are extracted from the OrderDate.

Customer features: The number of past orders and the average spending for each customer are calculated to provide insights into their purchasing behavior.

## Recommendation Models 🧠
The project uses three models to generate recommendations:

## 1. Item-Based Collaborative Filtering (Item-CF) 
This is the most straightforward approach. It identifies relationships between items by creating a matrix that shows how often items are purchased together. The similarity between items is then calculated using cosine similarity. To recommend a complementary item for a main_item, the model finds other items with the highest similarity scores and suggests them.


For 'Margherita' pizza, the recommendations are: 'Water', 'Fries', 'Soup', 'Pudding', 'Fanta', 'Orange Juice'.

For 'Veg Kebab', the recommendations are: 'Lemonade', 'Mashed Potatoes', 'Garlic Mushrooms', 'Cake', 'Garlic Bread', 'Orange Juice'.

For 'Fettuccine Alfredo', the recommendations are: 'Orange Juice', 'Salad', 'Garlic Mushrooms', 'Brownie', 'Lemonade', 'Mashed Potatoes'.

## 2. Random Forest Classifier (Context-Aware) 
This model goes beyond simple item pairings by incorporating contextual features. It is trained to predict the probability of a customer ordering a complementary item based on the MainItem, Hour, DayOfWeek, IsWeekend, PastOrders, and AvgSpend. A MultiOutputClassifier is used, as it can predict multiple complementary items at once.

With specific context (hour=18, dayofweek=5, is_weekend=1, past_orders=10, avg_spend=20), the recommendations 

For 'Margherita' are: 'Mashed Potatoes', 'Pepsi', 'Orange Juice', 'Fanta', 'Coke', 'Garlic Bread'.

For 'Pepperoni Calzone' under the same context, the recommendations are: 'Orange Juice', 'Coke', 'Pepsi', 'Salad', 'Mashed Potatoes', 'Garlic Bread'.

## 3. XGBoost Classifier (Context-Aware) 
Similar to the Random Forest model, XGBoost is a powerful, context-aware algorithm used to make predictions. It is trained on the same features to predict the probability of complementary items.

Under the same context as the Random Forest example, the recommendations 

For 'Margherita' are: 'Orange Juice', 'Chicken Wings', 'Pepsi', 'Garlic Bread', 'Onion Rings', 'Garlic Mushrooms'.

For 'Vegan Fish & Chips', the recommendations are: 'Ice Cream', 'Coke', 'Water', 'Fries', 'Onion Rings', 'Pepsi'.

## Conclusion
The project successfully demonstrates three distinct approaches to building a food recommendation system: a simple, association-based model (Item-CF) and two more advanced, context-aware machine learning models (Random Forest and XGBoost). Each model produces a different set of recommendations, highlighting the fact that including contextual features such as time and customer behavior can significantly alter the results. This makes the recommendations more personalized and potentially more accurate.



contextual features such as time and customer behavior can significantly alter the results. This makes the recommendations more personalized and potentially more accurate.
