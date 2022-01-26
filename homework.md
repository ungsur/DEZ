## Week 1 Homework

In this homework we'll prepare the environment 
and practice with terraform and SQL

## Question 1. Google Cloud SDK

Install Google Cloud SDK. What's the version you have? 

To get the version, run `gcloud --version`

## Google Cloud account 

Create an account in Google Cloud and create a project.


## Question 2. Terraform 

Now install terraform and go to the terraform directory (`week_1_basics_n_setup/1_terraform_gcp/terraform`)

After that, run

* `terraform init`
* `terraform plan`
* `terraform apply` 

Apply the plan and copy the output to the form

## Prepare Postgres 

Run Postgres and load data as shown in the videos

We'll use the yellow taxi trips from January 2021:

```bash
wget https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2021-01.csv
```

Download this data and put it to Postgres

## Question 3. Count records 

How many taxi trips were there on January 15?
select count(*)
from yellow_taxi_trips where cast(tpep_pickup_datetime as date) = '2021-01-15'
53024

## Question 4. Average
average tip: 159.05
with maxtable as(select max(tip_amount) baller,cast(tpep_pickup_datetime as date) dt 
	  from yellow_taxi_trips group by dt) 
	  select avg(baller) from maxtable

Find the largest tip for each day. 
On which day it was the largest tip in January?
1140.44 2021-1-20
select max(tip_amount) baller,cast(tpep_pickup_datetime as date) dt 
	  from yellow_taxi_trips group by dt order by baller desc
(note: it's not a typo, it's "tip", not "trip")

## Question 5. Most popular destination

What was the most popular destination for passengers picked up 
in central park on January 14?
elect count("DOLocationID") DOL,"DOLocationID" from yellow_taxi_trips  
where "PULocationID" = 43 and
CAST(tpep_pickup_datetime as date) = '2021-1-14' 
group by "DOLocationID" order by DOL Desc limit 1
Enter the district name (not id)
237,"Manhattan","Upper East Side South","Yellow Zone"

## Question 6. 

What's the pickup-dropoff pair with the largest 
average price for a ride (calculated based on `total_amount`)?
4 - 265 $2292.4
4,"Manhattan","Alphabet City","Yellow Zone" - 
265,"Unknown","NA","N/A"

234-39 262.85
234,"Manhattan","Union Sq","Yellow Zone"
39,"Brooklyn","Canarsie","Boro Zone"
262.85

select "PULocationID","DOLocationID", avg(total_amount)
from yellow_taxi_trips 
where "DOLocationID" != 265 and "DOLocationID" != 264
group by ("PULocationID","DOLocationID") 
order by  avg(total_amount) desc





## Submitting the solutions

Form for sumitting (TBA)

Deadline: 24 January, 17:00 CET


