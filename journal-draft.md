# (Not-so) Naive Way to Analyse Competitor using Orange Data Mining Toolkit

- tldr : You can get lost easily in twitter data mining, so you have to be VERY SPECIFIC on what you trying to find out before you even begin diving. Here, we use tweets from 4 big retail players in indonesia, input them 'orange data mining' toolkit, and output wordcloud (common keywords & hashtags they used to make them stands out), 10 topics in general from those tweets (sentence version of wordcloud, to learn what are they talking about), and sentiment analysis on those tweets (we can see their customers positive & negative feedbacks, and how can we learn from them).
- scenario
  Following up from my previous journal (https://dwihdyn.github.io/3-wordcloud-twitter.html), i've digging around ways on how can we properly mine twitter data, and this is when i discovered 'Orange Data Mining'. Watched few videos on data analysis https://www.youtube.com/watch?v=HDkI6G4slzQ & sentiment analysis https://www.youtube.com/watch?v=7Fnli0wc11g, looks fun. but that one beautiful word that hook me up for good. **_open-source_**. i'm sold.
- prerequisite :
  just like cooking, you need to get the ingredients & the proper cooking tools before we start, hence below the ingredients you must get & tools you must download: - python3 https://www.python.org/downloads/ (or just get whole anaconda) - twitter API token https://developer.twitter.com/en/docs/authentication/oauth-2-0/bearer-tokens#:~:text=Login%20to%20your%20Twitter%20account,Generate%22%20next%20to%20Bearer%20Token. - orange data miner (duh) https://orangedatamining.com/download, + setting up the twitter features (which you can follow here)https://drmarketing.expert/2018/04/09/6-steps-to-link-orange-3-and-twitter-api/

now we have all ingredients, lets cook some data with our usual OSEMN step-by-step cookbook!

- obtain
  - open 'twitter' widget and enter the twitter API & users you wanna get the data. here we getting 4 big retail players in indonesia
  - insert pic1
  - once you got it, open 'corpus viewer' to see the overview of the data. press ctrl + a, and click 'content' in 'display feature' to see the clean content of the tweets you just obtained.
  - insert pic2
- scrub
  - 'insert widget' from twitter to make sure we get the data from what we obtained, and open 'preprocess text' widget and follow the setup in the image below. (and for indonesian stopword, you can copy/paste here (https://raw.githubusercontent.com/dwihdyn/ds-exploration/main/p3/data/stopwords-indo.txt) and paste it in your empty .txt file and load it inside orange
  - insert pic
- explore
  - 'insert widget' from 'preprocess text' and open 'wordcloud', and you will get this output. (pull the 'words tilt' to max and come back zero to get all data)
  - inser pic1
  - i know, just like i mentioned in previous article that breaking down tweet into words are just return word with no meaning.
  - since twitter was the father of hashtags, we will look into interesting hashtags. here, lets look at #ppkm (lockdown in indonesian). and we can further analyse it by click at #ppkm, and open 'corpus viewer' widget.
  - inser pic2
  - turns out, we can see that only acehardware uses this hashtag, and promotes on ice cream walls, massage machine, and upselling their delivery service due to lockdown
- model
  - we have 2 kinds of modelling. topic modelling & sentiment score
  - in layman term, topic modelling is when we take all of these many words and try to group them together. here we group it to 10 different topics in general, which we can see result below
  - for techies & interested readers, we will be using 'Latent Dirichlet allocation' model
  - insert pic1
  - we can see each of those 10 topics of the orignial tweets by using heatmap, and group it together by topics, result below
  - insert pic2
  - click particular root, and see each tweets in 'corpus viewer'
  - insert pic3
    <br/>
- Next is sentiment score of each tweets. layman term, is to convert the tweets to numerical between -1 to +1, where -1 is negative tweet (eg : 'this place is sucks') and vise versa (+1 for tweets 'this place is wonderful'). You can follow the setting below
- for techies & interested readers, we will be using 'Vader' model
- insert pic4
- for begineers, you can start with 'Data Table' widget to display the data, scroll to the end, and click 'compound' column to sort the score. (compound is the overall sentiment of each given tweets)
- insert pic5
- for advances, you use heatmap (same as topic modelling), group it together by topics, result below
- insert pic6
- and click particular root, and see each tweets in 'corpus viewer'
- insert pic7

- interpret

  - we can draw conclusions from all 'heatmaps' (or data tables) & 'corpus viewers'. and let us show you how our 'tree' look like & parts they play in OSEMN.
  - insert pic1
  - Wordcloud :
    - all users leverage hashtag on either current event hapening (#ppkm lockdown & merdeka independence day), their collab (tokopedia with bts), or their own corporate hashtag (acesemangataktivitassetiaphari, keluargatransmart, belisemuadishopee)
    - #ppkm : we can see that only acehardware uses this hashtag, and promotes on ice cream walls, massage machine, and upselling their delivery service due to lockdown
    - we can explore in-depth too on #merdeka and each of the corporate hashtag
    - other than that, the tweets are very 'conversational', might consider update more stopwords, but if update it result to 90% data gone, we might need to get tweets by 'context' lookup, rather than 'user' lookup

- For Topic modelling & Sentiment Score. you really need to know exactly what are you trying to find out.

- final words from dwi

  - in twitter data mining, you REALLY need to be very specific on what exacly are we trying to find out. As there is SO MUCH data, which we can get lost easily

  - For beginners to really abe to digest the usefulness of 'topic modelling', find english topics that is easy to interpreted in 'topic modelling' (eg : #machinelearning give out pretty clean results)

  - Of course, you can download the analysis I made here (https://github.com/dwihdyn/ds-exploration/blob/main/p5/indoretail-comp-analysis.ows) and open it in your orange. You will see an error message from the heatplot part. so please take a breath, dont panic, and read the error message slowly, and google what you want to fix
