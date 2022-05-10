# hipaa_app_data
 
This HIPAA app is a reporter's toolkit that enables:
  * daily downloads of the current HIPAA disclosures and resolutions
  * a merge of disclosures and resolutions into a single data set
  * a daily diff from the prior day's data 
  * a labeled / transformed full data set
  * output of datestamped csv's for each of the above (daily)
  * a list of links to known state data breach databases for easy access

The date-stamped csv's create an ongoing record of daily snapshots that can be considered a historical archive. 

The labeled data set (based on the combined disclosures & settlements) covers some basic transforms that coerce date columns to the date types and add
  * a boolean to indicate ransomware
  * T/F duplicated column to indicate entities that appear more than once (aka repeat offenders) - kind of a boolean, kind of not
  * booleans to flag breaches where the number of people affected is >10k, >100k, and 1m+ 

The labeled columns are designed to make it easy for a reporter to put their hands on the news without running the same queries repeatedly, as is the separate 'new and updated' file.

My submission will also include a link to the datasette version of this project, which I effectively abandoned. The workflow to grab data and generate the csv's, then port the data into datasette, would have required dropping and rebuilding the tables, the db views, and the full text search daily. That's not impossible, but I didn't have a compelling use case. There's nothing one could do in datasette that couldn't be accomplished in R.

The current state of this project reflects the point where my efforts came to the proverbial fork in the road, which could take it in various directions.

In investigated the possibility of trying to link ransomware breaches with actual data breach material living in the wild. I think there's potential here, but it needs some pretty deep investigation into bitcoin tracking and dark web resources. Not impossible, but more than I could take on at the end of this project. (I'll come back to this. Stay tuned.)

What you'll see instead in the app is a curated list of state breach notification websites. There's potentially more context and narrative to be gleaned from the state level, but this depends almost wholly on the amount of background information that the breached organization includes in a letter to anyone whose data has been compromised. In other words, no promises. State material also requires a HIPAA-specific reporter to sift health information out of all reported data breaches. 

The states list contemplates at least a dozen separate scraping and pdf-pulling projects, as every state has its own system. (Because of course they do.) This is the point where the use case would need to be made for putting in that amount of work. Possible reporting reasons to do so might include:
  * expanding the HIPAA scope to the Everything Scope, using state data to try to get some kind of handle on just how much private data's been compromised and by what methods and from some sources -- I think some kind of really global story or project could justify the huge lift for all that scraping
  * HIPAA as a beat -- if I needed this information every day, I'd want an automated process and some kind of archive 
  * comparing the kind of data breached in other settings to health data
  * it would be interesting to do a Theoretical Person profile of all the data that could be out there due to breaches from various aspects of a person's life
  * there's potential to feed all the consumer letters into a machine learning / text mining process and maybe come out with some interesting angles (who gets blamed? how do the actors describe the underlying issues? how do these letter try to soften the blow?)

Setting the states aside, another logical step would be to fire these scripts automagically using GitHub. This gets to the question of deployment. There's no reason this system couldn't just live on someone's harddrive. Or, it could be automated and 'deployed' on some kind of internally accessed site. 

Since most of the sample Github Actions projects use python scripts, and I don't have any python here, I started down this path but didn't feel like I had enough time to make something work. (Somehow I missed the Github Actions moment that everyone else seemed to have jumped on board. I don't really have anything to show for my research. Greg later gave me permission to steal his methodology.)

In the end, I think this app does a great job inside a limited scope. I learned a lot from the datasette builds even though I dropped that line of work. In retrospect, if I wanted something more deployable, maybe flask would have made sense? I didn't really understand how the datasette json feed turns into an API -- I'll be looking over your shoulder this summer to see how that works. (That was a frustrating moment. I just didn't get it.)

On the other hand, this whole project was a great lesson on building my own reporting/work tools -- the stuff I do repeatedly that could be more automated or standardized. The creation of the date -stamped csv's alone would make this worth doing if I covered this area daily. I count getting selenium to work as a victory! It also helped a lot to run this project for a couple weeks. HIPAA data changes more than is obvious by glancing on the public 'wall of shame.'

Back to ransomware. There's making an app to learn how to make an app. But, then there's also news. IMHO, ransomware is the news here, and in retrospect I wish I had spent a lot of my time pondering slackbots and datasette methodologies on figuring out how to expand on or pull in more ransomware data. That said, even having the basic data in hand means the ransomware angle could now be measured, tracked over time and traced back to the affected hospitals for further reporting. 
