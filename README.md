# **Surfs up: Weather Analysis**

## **Overview** 
> This project 

---

## **Results**
###### Click here to view my [Challenge code](https://github.com/annaS000/surfs_up/blob/main/SurfsUp_Challenge.ipynb)

This section will review the results of the analysis for the weather during the months of June and December.

---

1. Overall, the temperatures in June were consistently warm, averaging about 75° with little variability
2. June precipitation
    #### **Summary for Temperature and Precipitation in June:**
    <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/junetemp.png?raw=true" width="200" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/juneprcp.png?raw=true" width="200" height="300" >
    > Here we have two charts of summary statistics in Oahu for Temperature and Precipitation in June


3. In December, we can see that the temperature 
4. Precipitation in dec
    #### **Summary for Temperature and Precipitation in December:**
    <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/dectemp.png?raw=true" width="200" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/decprcp.png?raw=true" width="200" height="300" >
    >Here we have two charts of summary statistics in Oahu for Temperature and Precipitation in December

    * 

---

## **Summary**

### **Additional Queries:**
If W.Avy wanted to look at the weather from specific places in Oahu we can create new quesries from temperature and precipitation data that is grouped by station. With this data we can then create 
1. June Temperatur and Precipitation by Station

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
<img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Jun%20Temps%20by%20Station.png?raw=true" width="500" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Jun%20Precip%20by%20Station.png?raw=true" width="500" height="300" >  
> With the information from the additional queries, we can create these two line charts of the min, max, and average temperatures and precipitation by station in Oahu for the month of June.


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
<img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Dec%20Temps%20by%20Station.png?raw=true" width="500" height="300" >  <img src="https://github.com/annaS000/surfs_up/blob/main/pictures/Dec%20Precip%20by%20Station.png?raw=true" width="500" height="300" > 
 > From the data collected by the additional queries, we can create these two line charts of the min, max, and average temperatures and precipitation by station in Oahu for the month of December.