# Community-Engagement
This notebook has the code for the solution of the problem to find the community engagement of a user given various input paramerters. The final result is stored in the submission.csv file. It contains the user_id and the respective engagement score.
Step-by-step walkthrough of how I arrived at the solution from the problem statement.
1. All the json files were present in different folders under a subfolder. Therefore, the first step was to merge all the scattered json files in to a single json file.
2. After that, came the part to actually play around with the data. It was a json file. All the columns in the dataframe were containng information in the form pyhton dictionaries because it was in json format. 
3. Going through all the key, value pairs and determining what information was necessary was the next task, since there were quite a few paramters in the data. Finally, I zeroed down on the following parametrs-
  * a. user_id: Id of each user.
  * b. total_texts: The number of messages sent by each user.
  * c. reaction_count: Total count of the reactions to the message sent by the user.
  * d. mentions: The number of times the user has mentioned someone in the message.
  * e. count_of_active_weeks: The number of weeks the user has been active. (This was found by checking how many weeks has he messaged in)
  * f. count_of replies: The number of times the user has replied to a message ,in a thread, or individually.
  * g. forwarded: The number of times the message has been forwarded.
4. I separated all the above factors by using the groupby method. Gropuing the dataframe with user_id and then selecting the specified columns.
5. Now an interesting thing mentioned in the problem statement was to find user engagement on a weekly basis as well. The reason behind this was that the more number of weeks a user is active and is sending messages, the better should be his community engagement score. 
6. To tackle this, I decided to create the variable avg_texts_per_week. So basically, I multiplied the total_texts variable with the count_of_active_weeks variable and then divided it by the total range of weeks in the dataframe which was 23. This weighted function ensured that the person having a greater number of texts but was active only for 1 week was given a lesser score than a person who has sent a few texts but consistantly over a longer time frame.
7. After this was done, I normalised all the values using the MinMax Scaler concept on the relevant cloumns.
8. Now this was the important part which would generate the engagement score. It had to be a weighted function for the fators mentioned above (excpet user_id,total_texts and count_of_active_weeks). So, the final variables remaining along with the weights which I decided to give them were-
  * a. reaction_count, 0.1
  * b. mentions, 0.2
  * c. avg_texts_per_week, 0.25
  * d. count_of_replies, 0.25
  * e. forwarded, 0.2
9. While coming up with parameters to measure community engagement, it should be kept in mind that those factors which provide a scope for further engagement between other users should be given a greater importance. Therefore, least weights were given to reactions because they leave no further scope of engagement as compared to mentions and forwards.
10. mentioning another user might show that the one who has messaged is pretty confident and a coherent memeber of the community. Usually, the people who are not involved in a community rarely mentions other in the messages. 
11. forwards create greater opportunities for engaging the community. Consider Twittter for example. Retweets are considered to be more important than likes. So following this principle, forwarded (retweets) should rank higher than reactions (likes)
12. The very base of an engaging conversation is when there is involvement from both sides. This is why replies are given a higher weightage. Replies help in keeping the ocnversation going. Like in Reddit, there are long threads which get higher user engagement.
13. Finally, the  avg_texts_per_week measures the activeness of user in a community. Hence this has a high weightage, equal to the weight of replies.
