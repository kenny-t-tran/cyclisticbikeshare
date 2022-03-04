<a name="top"></a>
# [Cyclistic Case Study](#top)
This data analysis was completed as part of the [Google Data Analytics Professional Certificate capstone course.](https://www.coursera.org/learn/google-data-analytics-capstone?specialization) 

The objective of this analysis is to discover how the use of Cyclistic's bike-sharing service differ between annual members and casual customers. I used the insights I gathered to develop a marketing strategy aimed at converting casual customers into annual members. 

Analyzed using Power BI. Visualized using both Power BI and Tableau Public. 
## Scenario
I am a junior data analyst working in the marketing analyst team at Cyclistic, a (fictional) bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, my team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, my team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve my recommendations, so they must be backed up with compelling data insights and professional data visualizations.

**About Cyclistic**

Cyclistic is a fictional bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.

> *To make the case study more realistic and place it into context, later I'm going to supplement some of the case information with information from [Divvy](https://ride.divvybikes.com/), the bike-share company that the case is based on.*

**The Goals**
 - Design a marketing strategy aimed at converting casual riders into annual members
 - Identify trends to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect Cyclistic's marketing tactics

**Deliverables**

 - A clear statement of the business task
 - A description of all data sources used
 - Documentation of any cleaning or manipulation of data
 - A summary of the analysis
 - Supporting visualizations and key findings
 - My top three recommentations based on my analysis
 
 <br>
 
**Let's Get Started.**  
## Phases
 **1.** [Ask](#ask)
 <br>
 **2.** [Prepare](#prepare) 
 <br>
 **3.** [Process](#process) 
 <br>
 **4.** [Analyze](#analyze)
 <br>
 **5.** [Share ](#share)
 <br>
 **6.** [Act](#act)

<a name="ask"></a>
## Ask

> **Guiding Questions**
> 
>  - What is the problem you are trying to solve?
>  - How can your insights drive business decisions?  
>  
> **Key Tasks**
>  1. Identify the business task.
>  2. Consider key stakeholders.
> 
> **Deliverable**
> 
>  - [X] A clear statement of the business task

##
**Business Task:** Discover how annual members and casual riders use Cyclistic/Divvy bikes differently and provide insight towards a marketing strategy that will convert casual riders to annual members.

**Scope of Work**: [Available here.](https://drive.google.com/file/d/1sIwqQKxrmJ--_LlZ2HrnXsmP9D3QbhCb/view?usp=sharing)

<a name="prepare"></a>
## Prepare

> **Guiding Questions**
> 
>  - Where is your data located?
>  - How is the data organized?
>  - Are there issues with bias or credibility in this data?
>  - How are you addressing licensing, privacy, security, and accessibility?
>  - How did you verify the data's integrity?
>  - How does it help you answer your question?
>  - Are there any problems with the data?  
>
> **Key Tasks**
>  1. Download the data and store it appropriately.
>  2. Identify how it's organized.
>  3. Sort and filter the data.
>  4. Determine credibility of the data.
> 
> **Deliverable**
> 
>  - [X] A description of all data sources used

##
I will be using 2021's historical trip data, organized by month in 12 separate .csv files, to analyze and identify trends. The data is obtained from [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

> *Note: The public dataset has been made available by Motivate International Inc. under [this license](https://ride.divvybikes.com/data-license-agreement). Due to data-privacy issues, the data does not contain personally identifiable information.*

Because the data is not tied to individual customers, I won't be able to identify Cyclistic's/Divvy's frequent customers and analyze their usage trends.

<a name="process"></a>
## Process

> **Guiding Questions**
> 
>  - What tools are you choosing and why?
>  - Have you ensured your data's integrity?
>  - What steps have you taken to ensure that your data is clean?
>  - How can you verify that your data is clean and ready to analze?
>  - Have you documented your cleaning process so you can review and share those results?
>
> **Key Tasks**
>  1. Check the data for errors.
>  2. Choose your tools.
>  3. Transform the data so you can work witth it effectively.
> 4. Document the cleaning process.
>
> **Deliverable**
> 
>  - [X] Documentation of any cleaning or manipulation of data

##
I will be using Power BI throughout this analysis. Though the Google Data Analytics course does not cover Power BI, I wanted to challenge myself to learn and get familiar with it. 

> *Note to future students: I would not recommed using Power BI due to the long processing times from the large amount of data. With over 5 million rows, you are much better off using SQL or R to complete this case study.*

**First Steps:**

 - **Merge** all 12 months of data into a single Power BI project file named ***tripdata_csv.pbix***. (5,595,063 rows of data = number of trips taken in 2021).
 
 - **Create columns** to help with analysis:
 
	- **ride_length**
		- In Power Query, create a new column with ***Duration.TotalSeconds***([ended_at]-[started_at]) to see the difference between start and end times in seconds. Label this column *ride_length_seconds*. 
		- In Power BI's Data view, add a column labeled *ride_length_minutes* using ***[ride_length_seconds]/60*** (will be used for a visualization).
		- In Power BI's Data view, create a new column labled *duration* that converts *ride_length_seconds* into hh:mm:ss format. [See here for the formula](https://community.powerbi.com/t5/Community-Blog/Aggregating-Duration-Time/ba-p/22486) *(Credit to Greg Deckler and konstantinos)!*
		
	- **distance**
		- Follow [this guide](http://www.girlswithpowertools.com/2014/05/distance/) to convert lattitude and longitude into miles. Label the final column *distance*.
		
		> *Since we have data for lattitude and longitude, I thought it would be interesting to calculate the distance of each  trip. I then realized that this column would be useless, as it only tells us where the bikes started and then ended up, not the total distance the bike traveled, so you can **skip this one.***
	- **day_of_week**
		- In Power Query, create a column labeled *day_of_week* using ***Date.DateofWeekName([started_at])***
			
	- **hour_of_day**
	  -  In Power Query, create a new column labled *hour_of_day* with ***DateTime.ToText([started_at], "h tt")*** to extract the hour of the day from the *started_at* column in AM/PM format.
			
**Cleaning the Data:**
 - **Blanks:** starting and ending latitude and longitude must not be blank, as that would indicate that the trip never completed. It is okay to have blanks in the station names, as not all bikes are parked at stations. We will fill blank station names with "No Station".
 
 - **Negative/Erroneous values:**
	 - 146 rows have a negative *duration*, which doesn't make sense. Looking at these rows, we can see that their date for *ended_at* began before their *started_at* date. This must mean that their dates were either swapped or incorrectly inputted. In any case, ***we must remove these rows.***
	> *Next is where I supplement the case information with information from Divvy. For this analysis, **I will assume all customers are financially responsible.** Long tangent ahead...*
- **Outliers -- Upper Limit:**
	- Sorting the *duration* column by descending, there are quite a few rows with rides lasting extremely long. The longest being 932 hours and 24 minutes, that's **38 days**! Could there be a mistake in the data (obviously), or could there actually be a customer out there that biked for  38 days and spent over $8,208 on a bike rental? 
	- We will use Divvy's pricing model to determine a reasonable ride duration and narrow down our data and get a better sense of how a typical, financially reasonable customer would use Cyclistic's/Divvy's bike-share service.
	- Divvy's pricing model works as follows: 
		1. **Single Rides**: $3.30 for 30 minutes. 
		2. **Day Pass**: $15 for a 24-hour period of unlimited  3-hour rides. 
		3. **Annual Memberships**: $9/month ($108 upfront) for unlimited 45-minute rides. 
		4. Rides that surpass the time limit incur a $0.15/minute fee. 
		5. There is a $2 fee for bikes not returned and docked at one of Divvy's [842 docking stations](https://data.cityofchicago.org/Transportation/Divvy-Bicycle-Stations-All-Map/bk89-9dk7) in Chigaco.
	
	- Based on these fees, it *does not* make financial sense for a casual rider to rent a bike out for longer than **52 minutes**, or to spend $7.80 on a single ride, as it would be more cost-effective to pay the potential $2 docking fee and start a second ride once they reach the 30-minute mark for at most $6.60. Not only would they save money, they would also get an additional 8 minutes of ride time. For annual members with free rides up to 45 minutes, it *would not* make financial sense for them to rent a bike out for longer than **59 minutes**, as they would pay a bigger fee for being over their timelimit than the $2 fee for not parking their bike at a Divvy dock (if they were not in range or didn't feel like pedaling to one).
	- ***One big problem:*** we don't know whether or not a casual customer's ride was purchased with a day pass. Though, if we did, we could set a conservative upper limit of **60 minutes** on the *duration* for those who did not utilize a day pass.
	-  	However, what we *can* do is assume that all rides were purchased with a day pass, and set an upper limit that starts at 3 hours, the maximum amount of time a day pass customer can rent a bike out at a time without paying a fee.
	- That upper limit is 3 hours and 14 minutes, or **11,640 seconds**. Because going 14 minutes over the 3 hour time limit is equivalent to the $2 parking fee, it would be more cost-effective to start another ride for free.

- **Outliers -- Lower limit:**
	- What is the minimum *duration* a ride would resonably last?
	
	- There are 506 rides that last 0 seconds. That means a customer unlocked a bike, paid for it, and docked it back instantaneously, which is imposssible. Filtering for rows with a *duration* of 1 second results in 873 rows. Again, this seems unreasonable. We will start with removing these rows.
	- To further clean up the rows, I'm going to assume that a ride should not last less than **30 seconds**. I am considering the fact that, in a span of 30 seconds, a customer would have to check out the bike, ride it, and park it. And then spend $3.30 doing so ($5.30 if it's not returned to a dock). It would be cheaper and faster to walk or run to get where they're going. So, ***we will remove rides that last less than 30 seconds.***
- Finally, after all of the cleaning is done, we are left with **5,515,894 rows** to work with.

<a name="analyze"></a>
## Analyze

> **Guiding Questions**
> 
>  - How should you organize your data to perform analysis on it?
>  - Has your data been properly formatted?
>  - What surprises did you discover in the data?
>  - What trends or relationships did you find in the data?
>  - How will these insights help answer your business questions?
>
> **Key Tasks**
>  1. Aggregate your data so it's useful and accessible.
>  2. Organize and format your data.
>  3. Perform calculations.
>  4. Identify trends and relationships.
>
> **Deliverable**
> 
>  - [X] A summary of your analysis

##

**Create measures** in the Report view that calculate the following:

- Mean of *duration*:

 `=FORMAT(AVERAGEA(tripdata_csv[duration]),"hh:mm:ss")`



	 
 - Mode of *ride_length_minutes*:
	 
`= 
VAR myTable = SUMMARIZE(tripdata_csv,tripdata_csv[ride_length_minutes],"Count",COUNT(tripdata_csv[ride_length_minutes])) 
VAR myTable2 = FILTER(myTable,[Count]=MAXX(myTable,[Count])) 
VAR Mode1 = MAXX(LASTNONBLANK(myTable2,tripdata_csv[ride_length_minutes]),tripdata_csv[ride_length_minutes]) 
RETURN  Mode1` 
	 
 - Mode of *day_of_week*:
 
 `= VAR myTable = SUMMARIZE(tripdata_csv,tripdata_csv[day_of_week],"Count",COUNT(tripdata_csv[day_of_week])) 
 VAR  myTable2 = FILTER(myTable,[Count]=MAXX(myTable,[Count])) 
 VAR  Mode1 = MAXX(LASTNONBLANK(myTable2,tripdata_csv[day_of_week]),tripdata_csv[day_of_week] 
 RETURN  Mode1`

**Analysis:**

 - Annual members preferred weekdays (40.44% vs. 26.59%), with Wednesday being the most popular day (471.71k rides).

 - Casual customers preferred weekends (18.50% vs. 14.47%), with Saturday being the most popular day (584.3k rides).

- The number of rides from casual customers on their second most popular day, Sunday (472k rides), was greater than the most popular day of annual members.
 
 - Ridership accross both customer types dipped in Fall and Winter, but increased rapidly throughout Spring and Summer, dipping as low as 48k rides in February and peaking at 810k rides in July.

 - During the 3rd Quarter (July, August, September) casual customer ridership surpassed annual member ridership by 49k or 4.1%.
 
- Both customer types preferred classic bikes (likely due to cost and availability).

- For annual members, most trips started between 7 AM and 8 AM. The number of trips steadily declined up until 3 PM where it started increasing until it peaked at 5 PM, and then declined again.

- Most popular ride times for casual customers were in the afternoon (3 PM to 6 PM).

- Rides for both customer types peaked at 5 PM, and dipped to their lowest between 3 AM and 4 AM. Ridership among casual customers surpassed rides of annual members between 9 PM and 4 AM.

- Annual members had shorter average ride durations on the weekends compared to casual customers.

- The majority of rides by annual members lasted around 5 minutes, whereas the majority of rides by casual customers lasted around 9 minutes.

- For both customer types, the most popular starting point was at a non station.

- The most popular starting and ending station for casual customers was Streeter Dr. and Grand Ave. For annual members, it was Clark St. and Elm St.

<a name="share"></a>
## Share

> **Guiding Questions**
> 
>  - Were you able to answer the question of how annual members and casual riders use Cyclistic bikes differently?
>  - What story does your data tell?
>  - How do your findings relate to your original question?
>  - Who is your audience? What is the best way to communicate with them?
>  - Can data visualization help you share your findings?
>  - Is your presentation accessible to your audience?
>
> **Key Tasks**
>  1. Determine the best way to share your findings.
>  2. Create effective data visualizations.
>  3. Present your findings.
>  4. Ensure your work is accessible.
>
> **Deliverable**
> 
>  - [X] Supporting visualizations and key findings

##

You can find a PDF of my Power BI visualizations [here](https://drive.google.com/file/d/1SuoxajAfL7KFiUz_lYKLR14yWSCvH0sG/view?usp=sharing).

Because I don't have a premium Power BI account, I can't publish my dashboard. So, I exported the data from my ***2021_tripdata.pbix*** file to a .csv using DAX Studio and recreated my visualizations in Tableau Public which is available [here](https://public.tableau.com/views/CyclsticCaseStudy/RidesbyDay?:language=en-US&:display_count=n&:origin=viz_share_link).

Lastly, [here](https://drive.google.com/file/d/1lFkpNz6Ruyihtl83jqsOLvvxCEbE1JUQ/view?usp=sharing) is the final Google Slides presentation of my analysis.

As for my report, well, you are reading it right now 🙂.

<a name="act"></a>
## Act

> **Guiding Questions**
> 
>  - What is your final conclusion based on your analysis?
>  - How could your team and business apply your insights?
>  - What next steps would you or your stkaeholders take based on your findings?
>  - Is there any additional data you could use to expand on your findings?
>
> **Key Tasks**
>  1. Create your portfolio.
>  2. Add your case study.
>  3. Practice presenting your case study to a friend or family member.
>
> **Deliverable**
> 
>  - [X] Your top three recommendations based on your analysis

##

**Conclusion:**

Recalling the business task of this analysis: 

> **Discover how annual members and casual riders use Cyclistic/Divvy bikes differently and provide insight towards a marketing strategy that will convert casual riders to annual members.**

Casual customers are individuals who leisurely use Cyclistic's bike-share service to get around the city. It is likely that this group of customers includes a large portion of tourists. They may visit Chicago often in their free time, but don't feel it is worth it to purchase an annual membership. These customers prefer longer rides that take place particularly in the afternoon and during the weekends. Their favorite place to rent bikes is at Streeter Dr. and Grand Ave., a docking station located at Jane Addams Memorial Park.

Annual members are individuals who use Cyclistic's bike-share service to commute to and from work. They prefer shorter rides that take place early in the morning and in the afternoon after work hours. Their favorite place to rent bikes is at Clark St. and Elm St., a docking station surrounded by apartments and businesses. Annual members are likely to be individuals that live in Chicago and lack other means of transportation.

**My Recommendations:**
1. **Create advertisements around casual customers' most popular stations** aimed at converting them into annual members.
	- Ideally, these advertisements would be displayed during Spring and Summer, and showcase how much casual customers would save by becoming an annual member.
	 
2. **Introduce a points-based rewards system that lets annual members earn points for taking rides and referring others** to purchase a membership. Members can use these points to redeem rewards such as:
	- A free ride they can give out to friends and family
	- Cyclistic/Divvy merchandise
	- Coupons and Discounts at retail stores and restaurants partnering with Cyclistic/Divvy
	- Day passes
	- Time limit extension credits
		- i.e.: If a ride lasts 48 minutes and a member has 3 minutes worth of extensions, they can apply all of or a portion of their credits to avoid the $0.15/minute fee.
	- Waived monthly payments
3. **Offer a discounted annual membership** targeting tourists and individuals who live outside of Chicago. 
	- This will encourage tourism in the city and increase ridership at the same time.

**Further Analysis:**

I would like to see additional data that:
- Ties rides to customer profiles
- Lists whether a ride was purchased with a day pass
- Shows minute-by-minute GPS tracking of bikes
##

This is the end of my case study. Thank you so much for taking the time to read though it. If you're also taking the Google Data Analytics certificate, I hope my take on this case study helped you out.

If you have any questions or feedback, please reach out to me through my [LinkedIn](https://www.linkedin.com/in/ktt/).

Thank you!

-- Kenny Tran

##

[Return to top](#top)
