---
layout: post
title:      "Struggle of Building Model Relationships"
date:       2020-08-24 02:59:47 +0000
permalink:  struggle_of_building_model_relationships
---


Coming into the rails project, I was very excited on what kind of project I could make with all the rails resources at my disposal. After thinking through a couple ideas, I commited to building an investment portfolio tracker. Essentially with the idea of being similar to tracking investments in excel table. The first models I thought about were just simply, a user, a stock, and then a portfolio. I initially had the relationship setup as a stock belongs to a portfolio and a portfolio belongs to a user. Where a user has many stocks through portfolios.  As I began to try to connect all them together, I was getting stuck on how the relationships were becoming and the way they would work in the app and routes I would need. These connections and relationship wasn't quite correct or fit how I needed to build the project. So I thought of changing the models up a bit. I was testing with a broker class and simply a user_stock class to replace the portfolio. But these were also not quite working out for the project or the really that interesting or useful to what I wanted. I finally settled on creating a category class with a join table for stocks and categories. Stocks would also belong to a user. This helped in creating the nested routes that would be functional and look right in relation to how I wanted to set everything up. 

Struggling through the right model classes and building the connections was not the best of times in working on this project, but it was also a good learning experience for me. I would constantly be looking at the rails guide for associations a learned a two tips that would be useful in future projects. 

Firstly, I forgot about the foreign key in my tables. This is important to add the forgein key to the class that belongs to another. For instance, because a stock belongs to a user, I included a user_id key within the stock table. This also applies when having a join table. For my stocks and categories, I created the stocks_categories class. And within that join table, I added the stock_id and the category_id, because stocks_categories belonged to both classes.

Secondly, associations are built around catching. So when testing associations, calling on a method that queries from the database, will then be used when calling on the next method. And to reset the association for a new test, you will call the reload method on the association. For example, when I was testing my associations, I called `user.stocks` to set the association I wanted to check. I then would call another method like, `user.stocks.count` to see how many stocks the user had. However I would be stuck on the current user I tested if I call `user.stocks.empty?` if I wanted to see another users stocks. I would have to call `user.stocks.reload.empty?` to see the proper result.

Constantly changing how my relationships were connected with each other, and how they would interact within the app was a great challenge. Although I still think theres plenty to learn about associations in general and building them to make sense. I built a better foundation that I could recall on as I progress through the course and in my career. 


