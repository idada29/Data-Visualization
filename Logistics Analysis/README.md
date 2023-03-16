The data source for the following analysis is in: https://www.kaggle.com/datasets/jolenechen/datacosupplychaindataset

The analysis process covered the following process:


    1. Data Preparation
       - Removing irrelevant data - "Product Status", "Product Price", "Product Name", "Product Image", "Product Description", "Product Category Id", "Product  Card Id"
       - Removed duplicates: This was needed to create unique keys to merge tables on.
       - Handled missing data - replaced nulls and empty cells
       - Data type conversions.
       - Validate data quality to check for completeness of the data.
       - Standardize data in "Order Country" to make naming convention useful for shape maps.
       
    2. Data Modelling: In this model I used star method as it best suits the data, having a single fact table and multiple dimension tables around it.
       I joined the tables based on primary keys and secondary keys.
    
    
![BI model](https://user-images.githubusercontent.com/22597020/225587953-693ac4ac-fd77-4f5d-abcb-654e676b3b92.jpg)
    
    
    

    3. Dashboard UI/UX design: I used most Powerpoint to create SVG backgrounds to increase the efficiency of the dashboard and reduce redundant images or shapes not in use for any analytics purpose rather than just designs.
    
    4. Generated business questions and made chooses on the visual selection to properly answer these questions










Excited to share the results of my latest project - a logistics dashboard for a retail firm handling an average of $11M in orders a year from its customers.

The findings gave me a clear picture of the payment preferences of customers, which will be a game-changer for the business's future strategies.

📌 Debit card dominates the spending landscape with a whopping 12.6 million dollars!

📌 Transfer follows closely with $9.2 million, proving to be a popular payment option.

📌 High number of pending and cancelled orders should be addressed to improve overall processing efficiency.

📌 To reduce pending orders, the firm should focus on streamlining card payment process and enhancing fraud detection measures.

📌 To reduce cancelled transactions, the firm should consider conducting customer satisfaction surveys and improving the ordering and delivery experience for customers.


I tried out the light and dark theme background, which do you prefer??


![DataCoSupply1024_1](https://user-images.githubusercontent.com/22597020/218254716-8cfeb1b6-a338-4755-8eeb-c1145381ec81.jpg)



![DataCoSupply1024_2](https://user-images.githubusercontent.com/22597020/218254724-f09a0201-59d4-4883-ba7e-bcc90496ce47.jpg)
