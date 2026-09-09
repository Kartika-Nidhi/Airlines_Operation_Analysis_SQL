# INTRODUCTION

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">The commercial aviation industry operates within high-volume, low-margin environments where operational efficiency, aircraft utilization, and scheduling precision directly dictate profitability. Managing flight networks requires real-time monitoring of delay propagation, seat occupancy rates, fleet route allocation, and customer booking behaviors.

This project delivers an end-to-end SQL analytical framework built on a multi-table relational airline database. By leveraging advanced SQL capabilities—including Common Table Expressions (CTEs), multi-level window functions, conditional aggregations, and subquery optimizations—this analysis transforms raw operational logs into actionable business intelligence. The dataset captures key dimensional entities such as flights, aircraft models, airports, bookings, and ticket itineraries, providing a comprehensive view of operational performance and revenue realization.

The project addresses core business challenges, including identifying high-delay corridors, optimizing seat load factors, evaluating fleet efficiency, and uncovering customer booking lifecycle trends.

# OBJECTIVES:

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
<ul>
<li>Flight Delays & Reliability: Identify routes and airports with the highest delay rates and bottleneck patterns.

<li>Fleet Utilization & Load Factor: Measure passenger capacity utilization across aircraft types and flight routes.

<li>Revenue Yield & Pricing Trends: Analyze total revenue generated across fare classes, routes, and booking lead times.

<li>Route & Passenger Demand: Rank origin-destination corridors by total passenger volume and traffic density.

<li>Ground Turnaround Efficiency: Track aircraft idle times between landing and next departure to evaluate fleet optimization.
</ul>

## Database Schema

# 1. Getting Ready with Data

<div>

# 2. Individual Table Inspection

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">Extracted English strings from JSON objects. 

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">Extracted airport_name and city from JSON objects.

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">No null or duplicates.

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">Nearly 50% flights, acutal departure and actual arrival time are missing.

<div
>

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">ticket_flights table is intermediate table to link bookings, tickets and flights.

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">There can be more than one flight for one ticket. In ticket_flights ticket_no is unique linked t ticket_no in tickets, but flight_id can be many. 

<div>

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">Considering Airlines as Business client, here are top questions.

# 3. Operational Efficiency and Groud Performance

## 3.1 Which flight routes and origin/destination airports generate the highest frequency and duration of departure and arrival delays?



<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
<ul>
<li>Out of ~33.1K total flight records, only 16,773 (~50.7%) contain tracked actual departure/arrival timestamps. The remaining 49.3% reflect unrecorded or cancelled operations, highlighting a data collection issue at ground stations.

<li>A total of 248 routes exhibit a 100% delay frequency, while an additional 618 routes experience delays on at least 50% of scheduled operations.

<li>Origin airports maintaining a 100% delay rate across the majority of their destination connections point to systemic hub-level bottlenecks (e.g., gate congestion, fueling bottlenecks, or restrictive departure slots) rather than isolated flight-specific issues.
</ul>

<div>

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
Reported To: Chief Operating Officer (COO) and Director of Integrated Operations Control Center (IOCC).

<div>

## 3.2 What is the average daily operational flight time and ground turnaround window per aircraft tail between consecutive scheduled flights?


<div>

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
Reported To: VP of Technical Operations & Maintenance (MRO) and Head of Airport Ground Handling & Ramp Operations.

<div>

# 4. Commercial Strategy & Revenue Optimization

## 4.1 Which route corridors and fare conditions generate the highest total revenue yield ?



<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
<ul>
<li>The DME-->KHV (Moscow Domodedovo to Khabarovsk) round-trip corridor is the network's largest revenue generator, producing 753.48M and 733.80M respectively (over 1.48B combined across both directions).
<li>Fare Class Contribution: Economy class contributes the majority of revenue (~65–70%) across all top routes, but Business class accounts for a significant premium contribution (~30%), particularly on long-haul routes like DME -> KHV and KHV -> LED.
<li>Comfort class seating is restricted to specific corridors (primarily routes connecting OVB - Novosibirsk) where it contributes ~16% of total route yield.

<div>

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
Reported To: Chief Commercial Officer (CCO) and VP of Revenue Management & Pricing.

<div>

## 4.2 How does passenger booking lead time correlate with ticket prices and fare class selection?


<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
<ul>
<li>Early-bird bookings (31+ days) secure significant cash flow upfront, driven by high Economy volume and premium yield in Business class.
<li>
The presence of high maximum prices in early windows shows that revenue management algorithms begin surge pricing early on high-demand routes rather than holding flat base rates until closer to departure.


<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
Reported To: Head of Revenue Management & Pricing and Director of Demand Generation & Marketing.

<div>

# 5. Network Planning & Customer Intelligence

## 5.1 What is the average seat load factor across different aircraft models and individual flight legs?


<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
<ul>

<li>The Boeing 777-300 leads the fleet with the highest average load factor at 65.87% across 308 operations, indicating strong demand concentration on its long-haul configuration (402 total seats, averaging 264.8 passengers per flight).
<li>
The Cessna 208 Caravan exhibits a severely depressed load factor of 14.42% (averaging only 1.7 passengers per flight against 12 total seats), despite operating a high frequency of 4,697 flights. This highlights an over-allocated rural feeder model that requires immediate capacity rightsizing or frequency adjustments.
<li>
 Workhorses like the Boeing 737-300 and Sukhoi Superjet-100 maintain stable utilization rates around 56.41% and 48.13% respectively, balancing high-density short-to-medium regional demand.
</ul>
</div>

<div>

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
Reported To: VP of Network Planning & Fleet Strategy and  Chief Financial Officer (CFO).

<div>

## 5.2 What is the distribution of repeat bookings per individual passenger, and what proportion of total revenue comes from frequent flyers?



<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
<ul>
<li>
Repeat customers account for 78.49% (187,470 passengers) of the total traveler base, indicating strong brand stickiness across the airline's network.

<li>While repeat buyers make up ~78% of volume, they generate 93.83% of total revenue. Conversely, one-time customers represent 21.51% of passengers but contribute only 6.17% to top-line earnings.

<li>The high revenue concentration among repeat flyers underlines the critical importance of retention programs, loyalty rewards, and personalized cross-selling targeted at frequent flyers to protect the airline's core financial stream.
</ul>
</div>

<div style = "background-color:lightblue; color:green; font-size:20px; text-align:justify">
Reported To: VP of Customer Experience & Loyalty Programs and Chief Marketing Officer (CMO).

<div>

<div>

# 6. Recommendations and Suggestions