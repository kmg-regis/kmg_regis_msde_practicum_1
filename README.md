# Kate Gallagher | Regis University | MSDE Practicum I
## Project Goal
In the modern digital age, online consumer reviews are generally important to the decision-making process about anything we spend money on in our society. These reviews are written by consumers for other consumers to read, which makes them rich in information, but disorganized and difficult to quantify at a higher level. 

My goal is to create a process by which reviews can be analyzed en masse, in order to gain valuable insights into the front-end user experience.

## Why Video Games?
The video game industry has been steadily increasing in popularity for years. Modern games are usually delivered on digital platforms, meaning there is no physical disc or cartridge anymore. The digital delivery method means that developers can release patches, bug fixes, content updates, etc. to consumers after they have already purchased the game. 


 
This ease of delivery has created a de facto ongoing contract between game developer and game consumer. Consumers expect developers to fix their bugs, update their games, and even publish new content for that game, after they have given the developer money for that game. 

This means that reviews are particularly important for games because the developer can fix things for those consumers - unlike buying a vacuum, for instance, where the consumer can leave a review about aspects of the vacuum they dislike, but they're still stuck with that specific vacuum. 

Developers can and should also use feedback from reviews to shape their next steps – for example, do they have the resources to shift focus to their next game, or do they need to work on a patch for their current one? 

## Why Steam?
Steam is the largest PC gaming platform in the world, with 75% of the global market share, with annual revenues over $35 billion.  

Steam also has structure around reviews that make the data reliable and useful for this project:

•	Accounts must have purchased the game in order to leave a review. This makes it much less likely that reviews are fake. 

•	No star or number ratings – players may only mark a game as “recommended” or “not recommended”. Thus in order to express their full opinion, they must write it out, making it a great source for sentiment analysis.

•	Other users may interact with reviews, including voting on whether it was helpful, whether it was funny, and leaving comments. This creates a natural filter by which off-topic or useless reviews are generally voted down and hidden from view. 

•	Game developers can leave responses to reviews of their game. Not every developer does this, but when they do it gives insight into the impact of fan engagement.

## ETL Process
The script I wrote extracts the html review data from Steampowered.com for a particular game, cleans and processes it, applies the Vader Sentiment Intensity Analyzer, and exports the groomed data to a CSV. The CSV can then be connected to Tableau for use in the dashboard I created. The script also saves the dataset to MongoDB for future usage. 

It is possible to connect Tableau directly to the data in MongoDB through an Atlas cluster, but I found the connection to be slow and unreliable. The dashboard performs much better when backed by a CSV. 

The pipeline will work on any game with a Steam identifier number, or “game app ID”. This can be found in the URL of the game’s Steam webpage. See screenshot below for an example.

![url_screenshot](https://github.com/kmg-regis/kmg_regis_msde_practicum_1/blob/main/images/url_screenshot.png)

 ## Limitations
Steam throttles its call rates, meaning that it takes some time to pull large amounts of reviews. It took me about 10-15 minutes per batch of 1000 to do the extraction.

The standard access level also limits users to data from the past year.

## Dataset
In order to demonstrate the pipeline and dashboard, I chose the following three games:

![stardew_image](https://github.com/kmg-regis/kmg_regis_msde_practicum_1/blob/main/images/stardew_image.png)
Stardew Valley is an indie game that was released in 2016. It is considered highly beloved, and serves as a control case for a game that has long-term popularity. The developer still occasionally releases free content and patches, even 8 years after release. 

![cyberpunk_image](https://github.com/kmg-regis/kmg_regis_msde_practicum_1/blob/main/images/cyberpunk_image.png)
Cyberpunk 2077 is a game from a major developer (CD Projekt Red). Its original release in 2020 was considered catastrophic: the game was highly hyped in the media, but upon release players found it buggy, unfinished, and boring. 

Over the last 3 years the studio has continued working on the game, taking in feedback from reviews and releasing patches and fixes. It is now highly popular and considered a very good game. 

![starfield_image](https://github.com/kmg-regis/kmg_regis_msde_practicum_1/blob/main/images/starfield_image.png)
Starfield is another big-name game, released by Bethesda last fall. The game was teased and hyped to fans in excess for years, but since release it has not lived up to the expectations. Fans think the game is boring and disappointing. 

The developer began replying to critical reviews on Steam, and the reviews with replies drew massive attention and fan engagement. However, the responses themselves were argumentative about fan reactions, rather than accepting of the feedback. A similar issue happened in December, when a studio director made a defensive post on Twitter that went viral. 

There is still time to change the story of this game, given the trajectory that Cyberpunk 2077 had – but Bethesda needs to be much more open to fan feedback if they are hoping to do so.

## Dashboard
[Link to Tableau Public](https://public.tableau.com/app/profile/katherine.gallagher3483/viz/VGR_final_KG/Dashboard1?publish=yes)

The underlying dataset for this dashboard contains the top 1000 reviews for each game in the last year, as determined by user votes. 

The ETL script also includes further examples of queries that might be useful to a game developer, such as the difference in engagement between negative and positive reviews. 

## Future Possibilities
This pipeline and dashboard could be paired with internal sales and cost data from a developer in order to model out how review sentiments impact revenues. 

Developers have special API access on Steam, which allows them to pull review data older than 1 year. Expanding the time range would allow more extensive study on review statistics over time. 

## Resources
I adapted the review extraction function from [Andrew Muller](https://andrew-muller.medium.com/scraping-steam-user-reviews-9a43f9e38c92). 
 
All data is owned by [Steampowered.com](https://store.steampowered.com/). 
