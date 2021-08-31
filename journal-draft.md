# mba-retail

- TLDR : Input each customer orders that contains the products & from which departments, Output are 2 things, pair of products (and their departments) that happen to be bought together more often than random, hence we can recommend management to re-arrange these departments side-by-side & the product pair side-by-side too to unconsciously trigger customer impulsive buying.

That is the formal definition of "Social Engineering", in this context, what we are trying to achieve is to place our products such that,

- Scenario

  - Have you ever thought of going to supermarket, knowing that you JUST WANT TO BUY WHAT IN YOUR LIST, but ended up buying half of the supermarket?
  - Yeah, welcome to Social Engineering 101 in retail, that has been implemented by the retail Data Scientist team in order to maximise the unconscious impulsive buying.
    - insert scenario1
  - We are working in a supermarket retail industry, and management hand us 3 datasets. Below the sneak-peek of the data
    - insert 6-mba-retail-scenario2
  - First is "orders_prod_prior", contains previous order contents for all customers.
  - Second is "products", contain each of the product details that the company has
  - Third is "departments", contains all the departments that the company has
  - With given data above, we can answer these two important question in order to implement the social engineering:

    - Given all past orders, which dept that always come together ?
    - Once the dept known, which products to be specific on each od these dept are always bought together ?

  - With those two questions answered, business can reorganize the store layout & run promotional campaign to bundle these item together.

- Result

  - Translating from those two business requirements to technical requirements, we can answer this question by using "Market Basket Analysis - Association Rule". (https://towardsdatascience.com/a-gentle-introduction-on-market-basket-analysis-association-rules-fa4b986a40ce)
  - Oversimplifying it, what it does is that, with each order data that contains products that has been purchased, we can see the occurences of particular item A & B happen on every order. If its happen very often, we can conclude that these two products are come in pairs, and what management can do to encourage this to happen more is to put these two item side-by-side.
  - Below is the simulation with the smaller dataset in order to understand "Associate Rules" intuitively

    - insert 6-mba-retail-result1
    - With this example, we can put apple & egg side-by-side in order to trigger the customer impulsive buying. you can read in-depth analysis here (https://www.kaggle.com/datatheque/association-rules-mining-market-basket-analysis)

  - With that being said, let's solve this problem with our favourite OSEMN framework!
  - Obtain
    - Data is given & shown sneak-peek in 'Scenario' section
  - Scrub
    - Since we want to know two things (which depts are the best pairs, and which products are the best pairs), we just need to prepare two dataframes such that it is suitable for our 'Association Rule' derivation (which is order_id and item_id). Below are the sneak-peek of each of the dataframes.
    - which depts are the best pairs
      - insert result2
    - which products are the best pairs
      - insert result3
    - note that since to make things simple, we've created function to get Association Rule derivation, we rename both targeted column to item_id. (no more product_id or dept_id)
  - Explore
    - We've skipped entirely this part, as deriving 'Association Rule' on 3 million+ rows dataset is computationally expensive (nearly consumed 16GB or RAM)
  - Model
    - This is the part where we implement the Association Rules function. You can check out the code in my kaggle (https://www.kaggle.com/dwihdyn/mkt-bskt-analysis), but oversimplifying it:
      - What we want is to calculate each pair of items relationships (lift value). say we have item A & B.
        - if lift > 1, A & B occur together more often than random
        - if lift = 1, A & B occur together only by chance (random)
        - if lift < 1, A & B occur together less often than random
      - calculate lift(A,B) = Pr(A & B bought together) / (Pr(A bought) \* Pr(B bought))
        - where Pr(A bought) : Probability item A is bought
    - Below is the result of best pair & the lift value for each department
      - insert result4
    - And for each product
      - insert result5
  - iNterpret
    - From department table, we can put these 5 top dept side by side, as coincidentally, it circes back (other, alcohol, pets, household, personal care)
    - From Product table
      - Top association characterics were, with one flavor of an item being purchased with another flavor from the SAME ITEM FAMILY
        - Strawberry chia COTTAGE CHEESE & Blueberry acai COTTAGE CHEESE
        - Chicken CAT FOOD & Turkey CAT FOOD
      - This can be implemented in "Recommended system" backend. (eg if cust buy chicken cat food, recommend them turkey cat food too)
    - General solution that we can give to management ?
      - Get lift > 1 dept, and put dept rows side-by-side
      - For each items in dept, Get lift > 1 products, and put it together accordingly (and share these pairings to marketing team to create 'pair discount'

- call-to-action

      - Merchendise team can re-arrange these 5 dept to be placed side-by-side (other, alcohol, pets, household, personal care)
      - Since almost all products that comes in pair are in the same departments, for each departments, put those pair products side-by-side (+ We can share these product pairs to the marketing team to promote 'Bundle sales' for all these pairs that has top10 highest lift-value)

- final word from dwi
  - As mentioned in Explore section, we'll cover how to explore data as this to get insight in our next article!
  - It's too much to digest this topic in one article, hence for interested reader that want to fully digest this knowledge, head over to my code in my kaggle notebook (https://www.kaggle.com/dwihdyn/mkt-bskt-analysis) and leave a like on the notebook!
