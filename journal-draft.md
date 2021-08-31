# mrkt bskt prediction + exploration best practices in retail

- TLDR :

- Scenario :

- Result :

  - Obtain
    - Data is given & shown sneak-peek in 'Scenario' section
  - Scrub

    - Since we want to know two things (which depts are the best pairs, and which products are the best pairs), we just need to prepare two dataframes such that it is suitable for our 'Association Rule' derivation (which is order_id and item_id). Below are the sneak-peek of each of the dataframes.

  - Explore
    - We've skipped entirely this part, as deriving 'Association Rule' on 3 million+ rows dataset is computationally expensive (nearly consumed 16GB or RAM)
  - Model

    - This is the part where we implement the Association Rules function. You can check out the full code in my kaggle (https://www.kaggle.com/dwihdyn/mkt-bskt-analysis), but oversimplifying it:

  - iNterpret
    - From department table, we can put these 5 top dept side by side, as coincidentally, it circes back (other, alcohol, pets, household, personal care)

- call-to-action :

  - Merchendise team can re-arrange these 5 dept to be placed side-by-side (other, alcohol, pets, household, personal care)

- final word from dwi :

  - About the "Explore" part that we skipped, we'll cover how to explore data as this to get insight in our next article!
