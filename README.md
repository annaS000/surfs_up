# **Surfs up: Weather Analysis**

## **Overview** 
> This project provides a weather analysis for Oahu, Hawaii. In hopes of opening a surf/ice cream shop, we must supply a potential investor, W. Avy, with the information he needs to feel confident in supporting our business. Since the success of our shop relies heavily on the weather, we have been asked to collect data on the temperatures in June and December. To acquire quality results we will be querying data from a [SQLite database](https://github.com/annaS000/surfs_up/blob/main/hawaii.sqlite) and then using Python, specifically the Pandas library, SQLAlchemy, and Matplotlib tp perform our analysis. Once the information has been organized into dataframes, we must use this information to find trends and create a write up for W. Avy.

---

## **Results**
###### Click here to view my [Challenge code](https://github.com/annaS000/surfs_up/blob/main/SurfsUp_Challenge.ipynb)

This section will review the results of the analysis for the weather during the months of June and December.

---

1. Overall, the temperatures in June were consistently warm. 
    * Averaging about 75°F with little variability and 50% of our data is within the range of 64°F-77°F, this is perfect weather for people to go have ice cream which is beneficial to our shop.
2. The month of June does not see much precipitation. 
    * The maximum score was a little over 4 but, in comparison to the rest of the summary, this does not seem to happen often and could even be a possible outlier.

    <br/>

    #### **Summary for Temperature and Precipitation in June:**
    <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/junetemp.png?raw=true" width="200" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/juneprcp.png?raw=true" width="200" height="300" >
    > Here we have two charts of summary statistics in Oahu for Temperature and Precipitation in June

    <br/>

3. In December, the temperature has a slighly lower average but is still in good standing with our shop. 
    * December continues to see warmer days with 50% of our data being between 69°F-74°F which means the ice cream shop would still attain business even throughout the winter.
4. Precipitation in December has a higher maximum precipitation score.
    * This may also be an outlier because when compared to the rest of the chart, majority of data shows very low scores.

    <br/>

    #### **Summary for Temperature and Precipitation in December:**
    <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/dectemp.png?raw=true" width="200" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/decprcp.png?raw=true" width="200" height="300" >
    >Here we have two charts of summary statistics in Oahu for Temperature and Precipitation in December

---

## **Summary**
After analyzing the data gathered for the temperatures in June and December, we can see that Oahu is a a favorable choice for our surf shop. In order to have consistent business throughout the year for a surf and ice cream shop, there must be warm temperatures year-round. So far, we have seen satisfactory numbers for the Summer and Winter using our samples from June and December. To provide further reassure for these findings, it is of value to observe temperatures for the "Spring" and "Fall" as well. For example:

<img src="https://github.com/annaS000/surfs_up/blob/main/pictures/marchtemps.png?raw=true" width="200" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/septemps.png?raw=true" width="200" height="300" >
>These charts show summary statistics for March and September to confirm that the weather remains an appropriate temperature for the shop to be profitable. These numbers are fairly uniform to our data from June and December, therefore 

Overall, as expected of an island with a tropical climate, Oahu experiences mostly high temperatures. In fact, according to the [National Weather Service](https://www.weather.gov/hfo/climate_summary), "for most of Hawaii, there are only two seasons: "summer," between May and October, and "winter," between October and April" which explains why there are not many disparities in temperatures between months throughout the year. This is great news for our surf shop and it can be concluded that we can have confidence in the opening of our surf shop in Oahu.

### **Additional Queries:**
If W. Avy was interested in studying the weather trends from specific places in Oahu we can create new queries from temperature and precipitation data that is grouped by station. With this data we can then create visualizations such as bar charts to display these findings.
1. June Temperature and Precipitation by Station

        #high low and avg for june temps by station
        juneStats = session.query(Measurement.station,func.min(Measurement.tobs), 
                    func.max(Measurement.tobs), func.avg(Measurement.tobs)).\
                    group_by(Measurement.station).\
                    filter(func.strftime("%m", Measurement.date) == '06').all()

        #dataframes for june temps by station
        junedf = pd.DataFrame(juneStats,columns=['station','min temp','max temp','avg temp'])
        junedf.set_index('station', inplace=True)

        #high low and avg for june precipitation by station
        juneStats2 = session.query(Measurement.station,func.min(Measurement.prcp), 
                    func.max(Measurement.prcp), func.avg(Measurement.prcp)).\
                    group_by(Measurement.station).filter(func.strftime("%m", 
                    Measurement.date) == '06').all()

        #dataframes for june temps by station
        junedf2 = pd.DataFrame(juneStats2, columns=['station','min','max','avg'])
        junedf2.set_index('station', inplace=True)


    #### **Temperature and Precipitation in June by Station:**
    <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Jun%20Temps%20Station.png?raw=true" width="500" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Jun%20Precip%20Station.png?raw=true" width="500" height="300" >  
    > With the information from the additional queries, we can create these two bar charts of the min, max, and average temperatures and precipitation by station in Oahu for the month of June.


    2. December Temperatur and Precipitation by Station

            #high low and avg for december temps by station
            decStats = session.query(Measurement.station,func.min(Measurement.tobs), 
                        func.max(Measurement.tobs), func.avg(Measurement.tobs)).\
                        group_by(Measurement.station).\
                        filter(func.strftime("%m", Measurement.date) == '12').all()

            #dataframes for december temps by station
            decdf = pd.DataFrame(decStats, columns=['station', 'min temp', 'max temp', 'avg temp'])
            decdf.set_index('station', inplace=True)

            #high low and avg for december precipitation by station
            decStats2 = session.query(Measurement.station,func.min(Measurement.prcp), 
                        func.max(Measurement.prcp), func.avg(Measurement.prcp)).\
                        group_by(Measurement.station).filter(func.strftime("%m", 
                        Measurement.date) == '12').all()

            #dataframes for december temps by station
            decdf2 = pd.DataFrame(decStats2, columns=['station','min','max','avg'])
            decdf2.set_index('station', inplace=True)


        #### **Temperature and Precipitation in December by Station:**
        <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Dec%20Temps%20Station.png?raw=true" width="500" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Dec%20Precip%20Station.png?raw=true" width="500" height="300" > 
        > From the data collected by the additional queries, we can create these two bar charts of the min, max, and average temperatures and precipitation by station in Oahu for the month of December. 

        These bar charts that display information for each station in Oahu are helpful when deciding an exact location on the island. While it is good to see overall statistics, having data on specific areas narrow down the options for where in Oahu our shop will open and depending on how well the store does we can possibly open multiple locations.

## **Citation**
Click here for [reference]()