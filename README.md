Data Analysis of NYSE stock exchange data using Hive and Tableau 

Step1: Download NYSE stck exchange data from http://eoddata.com/. 
Step2: Upload data into HDFS using

 hdfs dfs -put /home/shwetatanwar13/nyse /user/shwetatanwar13/
 hdfs dfs -put /home/shwetatanwar13/nyse/companylist.csv /user/shwetatanwar13/nyse/

Step3: Create tables in Hive on top of the data.

 create table company_list(
Symbol string,
Name string,
LastSale float,
MarketCap float,
ADR_TSO string,
IPOyear string,
Sector string,
Industry string,
Summary string,
Quote string)
row format delimited fields terminated by '|'
tblproperties ("skip.header.line.count"="1");

load data inpath '/user/shwetatanwar13/nyse/companylist.csv' into table company_list;

create external table stock_eod(
stockticker string,
transactiondate string,
openprice float,
highprice float,
lowprice float,
closeprice float,
volume bigint
)
row format delimited fields terminated by ',';

load data inpath '/user/shwetatanwar13/nyse/NYSE_2019-18.csv' into table stock_eod;

Step4: Calculate Mothly total Volume by Sector and Company_Name for year 2019 and insert into table stock_volume_per_month.

Step5: Download data to local to analyse in tableau

   hdfs dfs -get /apps/hive/warehouse/nyse_sh.db/stock_volume_per_month /home/shwetatanwar13/nyse
   
Step6:Visualize the data in tableau.

