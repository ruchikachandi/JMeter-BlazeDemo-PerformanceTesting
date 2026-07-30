# JMeter-BlazeDemo-PerformanceTesting
Performance Testing  of flight booking application using JMeter 

## About this project
This is my first performance testing project using Apache JMeter. I tested blazedemo.com which is a demo flight booking website made for testing practice.

I wanted to see how the site behaves when multiple users are using it at the same time — 50, 100 and 200 users.

## Tools used
- Apache JMeter 5.6.3
- CSV Data Set Config for test data
- JMeter HTML Dashboard Report

## What I tested
I simulated a complete flight booking journey that a real user would do:

| Step | Action | URL |
|------|--------|-----|
| 1 | Visit homepage | blazedemo.com/ |
| 2 | Search for flights | /reserve.php |
| 3 | Choose a flight | /purchase.php |
| 4 | Complete purchase | /confirmation.php |

To make it realistic, I used a CSV file with 7 different city pairs so each virtual user searches a different route instead of all users searching the same thing.

## Test results

| Users | Avg Response | Min | Max  | 90th pct | Throughput | Error % |
|-------|-------------|-----|------|----------|------------|---------|
| 50    | 704ms       | 338 | 3478 | 1812ms   | 9.10/sec   | 0.00%   |
| 100   | 583ms       | 331 | 4191 | 777ms    | 22.38/sec  | 0.00%   |
| 200   | 614ms       | 336 | 3937 | 897ms    | 43.23/sec  | 0.00%   |

## What I noticed in the results
- All 3 tests completed with 0% error rate which means the site handled all users without failing
- Throughput increased significantly from 9/sec at 50 users to 43/sec at 200 users — the server was processing more requests as load increased
- Interestingly average response time at 100 users (583ms) was actually better than at 50 users (704ms) — this can happen on demo servers where performance varies between runs
- 90th percentile at 100 users was 777ms meaning 90% of users got a response under 1 second which is a good result
- Find Flights page was consistently the slowest step across all 3 tests — this makes sense as it does a search query

## How to run this test
1. Download and install Apache JMeter
2. Open test-plan/BlazeDemoProject.jmx in JMeter
3. Update the CSV file path in CSV Data Set Config 
   to point to test-data/flightData.csv on your machine
4. Set number of threads in Thread Group
5. Click Play button to run
6. To generate HTML report after test completes: jmeter -g results.csv -o report-folder
