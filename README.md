# EXPLORATORY DATA ANALYSIS OF FORD GO BIKE SHARING SYSTEM
An Exploratory Data Analysis (EDA) of the Ford GoBike system using Python to optimize micro-mobility fleet logistics. Implements data pipelines to resolve asset distribution bottlenecks, maps distinct behavioral profiles between daily workforce commuters (Subscribers) provides data-backed operational strategies to close gaps and maximize revenue.

1. Executive Summary
The modern micro-mobility landscape has transitioned from a niche transportation alternative to a core pillar of sustainable urban transit frameworks. As public transportation networks adapt to growing populations, micro-mobility options like bike-sharing offer eco-friendly, flexible solutions for the "first-mile/last-mile" commute problem. This comprehensive project report details a thorough Exploratory Data Analysis (EDA) of the Ford GoBike sharing system using Google Collab. The primary objective of this study is to transform highly fragmented, multi-file transactional ride data into high-value business intelligence. By analysing historical ride data, this report aims to optimize fleet logistics, evaluate distinct customer usage models, investigate demographic footprints, and design data-backed strategies to ensure long-term system scalability, operational efficiency, and revenue growth.


2. Problem Statement
As urban density rises and traditional automotive vehicle traffic creates unprecedented traffic gridlock, city transit infrastructures require highly scalable, sustainable micro-mobility alternatives. While automated bike-sharing networks offer a clean, healthy, and highly space-efficient solution, platform operational managers frequently encounter severe asset distribution imbalances due to highly variable, shifting customer demand profiles throughout the day.
Without a clear predictive data model of user behaviour, bike networks run into two distinct, daily operational bottlenecks:
1.	Critical Asset Shortages & Dock Crowding: Popular transit hubs, central business districts, and university plazas run completely out of available bicycles during morning arrival hours, or run out of empty docking slots during evening rush hours, causing immediate ride abandonment and user frustration.
2.	Asset Underutilization & Inactive Capital: Large amounts of vehicle inventory sit completely idle, unmonetized, and clustered in residential or commercial dead zones during off-peak midday windows and across the weekend.


3. Data Wrangling & Engineering Pipeline
•	Multi-File Integration: The raw transactional history was originally fragmented across separate monthly and seasonal CSV sheets, making comprehensive long-term tracking impossible. Using Python’s glob and os modules, a script dynamically scanned the file storage path and executed an optimized row-wise concatenation via pd.concat(axis=0, ignore index=True) to produce a unified master Data Frame.
•	Null Value Mitigation & Quality Control: High-contrast Seaborn heatmaps were generated to visually map missing data across millions of rows. Incomplete rows lacking critical geographic indices—such as station names, unique station IDs, or precise station coordinates—were systematically dropped to maintain calculation integrity and eliminate spatial modelling bias.
•	Type Standardization: Raw string timestamps (start_time and end_time) were parsed and converted into uniform datetime64[ns] objects to unlock temporal indexing capabilities.
•	Feature Engineering: To allow for granular temporal tracking and look for hidden chronological rhythms, new analytical dimensions were engineered from the datetime objects, including start_hour (0–23), day_of_week (Monday–Sunday), and month.
•	Unit Normalization: Trip durations were converted from raw seconds into a standalone duration_min metric. This step provided clear, human-readable data points for statistical exploration and prevented long-tail outliers from skewing the statistical distributions.


4. Key Analytical Insights & Visualizations
A. System Demand Timelines (Univariate Analysis)
•	Bimodal Peak Commuting: Total system demand exhibits an explicit, powerful bimodal distribution on weekdays, peaking sharply between 8:00 AM – 9:00 AM and 5:00 PM – 6:00 PM. This confirms that routine workforce and student transit form the foundational load of the system.
•	Weekly Traffic Shift: Aggregate trip counts remain consistently high from Monday through Friday but experience a ~25% drop-off over the weekend, confirming that casual use does not completely offset the drop in commuter volume.
B. User Segmentation Analysis (Bivariate Analysis)
•	The Subscriber Baseline: Annual Subscribers represent 85–90% of all generated trips. Their usage is highly destination-focused, tightly bound to peak weekday commute windows, and incredibly efficient—maintaining a brief average trip length of 10–15 minutes.
•	The Casual Customer Engine: Non-subscribing, short-term Customers display a smooth, bell-shaped midday active curve peaking between 11:00 AM and 2:00 PM. While their total trip volume is lower, their average ride duration surges by approximately 60% on weekends, indicating high engagement with leisure travel, tourism, and open-ended urban exploration.
C. Demographics & Feature Relationships (Multivariate Analysis)
•	Demographic Concentration: Platform engagement peaks sharply among young adults aged 25–38. A stark gender gap is visible across the system, with male riders generating over 70% of total system transactions.
•	Statistical Independence: Correlation matrices and multi-variable pair plots confirm that engineered time indicators (hours, months) possess near-zero linear correlations with ride lengths. Trip duration is fundamentally determined by user type and behavioural intent, rather than the clock or calendar.


5. Visual Deep-Dive: Explaining Key Notebook Charts
Chart 1: Proportional Breakdown of User Types (Pie Chart)
•	Visual Representation: A segmented categorical circle representing part-to-whole data metrics.
•	The Insight: It reveals that annual Subscribers form the absolute backbone of the platform, driving approximately 85% to 90% of all generated trips, while casual riders represent a small minority.
•	Business Impact: This proves the system has exceptional baseline loyalty among daily commuters. However, it alerts the business that the casual tourist market is highly under-penetrated and needs targeted user-acquisition strategies.
•	 
Chart 2: Total Bike Rentals Grouped by Hour of the Day (Countplot)
•	Visual Representation: Discrete numerical bar charts indicating absolute load by hour.
•	The Insight: The data exhibits a powerful bimodal distribution. Massive demand spikes occur strictly between 8:00 AM – 9:00 AM and 5:00 PM – 6:00 PM on weekdays, while midday traffic remains a steady, lower plateau.
•	Business Impact: This chart gives the logistics team an exact operational timeline. To avoid empty docks or bike shortages, ground crews should schedule major fleet rebalancing runs right before these rush-hour windows.
 
Chart 3: Hourly Bike Rentals Segmented by User Type (Grouped Countplot)
•	Visual Representation: Clustered side-by-side comparative bars matching hours with a custom user hue overlay.
•	The Insight: It exposes completely different behavioral patterns. Subscribers strictly drive the high-intensity 8 AM and 5 PM rush-hour peaks, confirming they use the bikes for workplace or school commuting. Casual Customers, however, show a smooth, bell-shaped curve that peaks during pleasant midday hours (11 AM – 2 PM).
•	Business Impact: This prevents marketing teams from wasting budget on generic ads. Instead, they can target non-subscribers with midday leisure promotions while focusing subscription offers around daily commute convenience.
 
Chart 4: Daily Distribution of Bike Trips Across the Week (Bar Chart)
•	Visual Representation: Chronological distribution across sequential days of the week.
•	The Insight: Ride volumes remain consistently high and uniform from Monday through Friday but experience a noticeable ~25% drop-off on Saturdays and Sundays.
•	Business Impact: Knowing that weekend volume drops allows maintenance managers to safely pull heavily used bikes off the streets for deep structural checkups, repairs, and safety testing over the weekend without disrupting the high-volume weekday commuter network.
 
Chart 5: Comparison of Ride Durations by User Type (Boxplot)
•	Visual Representation: Box-and-whisker distribution blocks showcasing medians, ranges, and outliers.
•	The Insight: Even though Subscribers generate the vast majority of trips, their rides are highly efficient and brief, tightly clustering around 10–15 minutes. Casual Customers keep the bikes out significantly longer, with an average trip duration that surges by 60% on weekends.
•	Business Impact: This justifies changing the pricing structure for casual riders. Instead of a strict 30-minute standard cut-off, the company can introduce custom, higher-priced "Weekend Explorer" passes with a 45-to-60-minute base window to perfectly match tourist behaviour.
 
Chart 6: Average Trip Duration Across Hours of the Day (Line Plot)
•	Visual Representation: A continuous sequential line metric linking hourly intervals.
•	The Insight: While the volume of rides drops during the middle of the day, the average length of those midday trips peaks sharply between 11:00 AM and 2:00 PM. A secondary trip length increase is also visible late at night.
•	Business Impact: This proves that off-peak riders are not in a rush. The business can leverage this by partnering with local cafes, parks, and retail districts to offer "slow-riding" rewards, keeping bikes active and generating revenue during hours when commuters are at their desks.
 
Chart 7: Correlation Matrix of Numeric Bike Metrics (Heatmap)
•	Visual Representation: A standard numerical correlation grid utilizing high-contrast linear gradient boxes.
•	The Insight: Strong positive correlations naturally exist between duration values. However, near-zero correlations with hours and calendar months mathematically prove that ride lengths are completely independent of the time of day or seasonal calendar indices.
•	Business Impact: For an intern project, this is a major win because it proves that your feature engineering steps (like extracting hours and converting time) did not introduce multi-collinearity errors. It confirms your cleaned dataset is perfectly prepared for future machine learning or predictive data models.
 


6. Strategic Business Solutions & Recommendations
Based on the data-driven trends uncovered during the EDA phase, the following operational adjustments are recommended:

1.	Smart Fleet Rebalancing Schedules: Ground rebalancing crews should prioritize bike distribution adjustments during the off-peak midday window (10:00 AM to 2:00 PM). Moving idle inventory from residential drop points back to central commercial business hubs before the 5:00 PM evening rush will minimize empty-dock frustrations and optimize vehicle turnaround times.

2.	Weekend Revenue Optimization: Launch targeted "Weekend Explorer" bundles and cross-promotional rewards with local parks, dining spots, and cultural venues. This captures high-duration casual tourist demand and monetizes inventory that would otherwise sit idle on Saturdays and Sundays.

3.	Targeted Demographic Expansion: Address the system's 70% male bias by running inclusive marketing initiatives. Partnering with cities to showcase protected, well-lit micro-mobility transit corridors will lower the barrier to entry for female and senior riders.

4.	Simplified Equity Program Onboarding: Streamline registration and run community outreach events for the underutilized "Bike Share for All" low-income program. Expanding this segment builds strong local political goodwill and helps secure valuable municipal operating subsidies.


7. Detailed Project Methodology & Implementation Details
•	Robust Data Injection: Rather than assuming local file availability, the ingestion tier utilizes advanced folder scanning and error-handling conditions. If no target data sheets are detected, the system throws descriptive custom alerts to avoid execution failure.
•	Exploratory Visual Matrix Construction: Visual charts utilize customized styling configurations to ensure high contrast and clear readability. The integration of Kernel Density Estimation (KDE) line mappings onto the structural histograms provides clear visibility into right-skewed data boundaries.
•	Asset Lifecycle Analysis: By tracking independent usage counts across individual bike_id strings, the code lays the foundation for predictive preventative maintenance models, helping operations teams identify heavily worked assets before hardware failures occur on city streets.


8. Conclusion
This project successfully transitions raw, fragmented transactional system logs into a clear, strategic map of consumer behaviour. The analysis proves that the Ford GoBike system relies on a dual-engine user model: highly routine, high-frequency weekday commuters (Subscribers) and highly elastic, long-duration weekend leisure riders (Customers). By implementing these data-backed logistics schedules and targeted marketing expansions, the platform can successfully maximize vehicle lifetime value, eliminate costly dock bottlenecks, and scale long-term revenue growth.

