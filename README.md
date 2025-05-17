# RTA-Riyadh-Transport-Authority-dashboards
This project offers valuable insights into public transportation dynamics, unveiling essential information about how the transportation is covering  Riyadh city. From bus operations to Metro Dynamics, we've got you covered!


This analysis is based on a rich dataset that encompasses various aspects of public transportation, including:
Bus operations and Stops
Metro Lines and Stations

Key Insights Covered in this Report :
1. Total Number of Buses: Understand the overall volume of Buses and the the bus stops and routes where they function.
2. Total Number of Metrolines: Understand the Distrubtion of Metrolines and the Metro Stations.
3. Performance Analysis between Buses and MetroS mapping and Distrubtions: Identify Most performing Stations and Bus stops and proption between these main transportations to optimize operations.

   <img width="497" alt="1" src="https://github.com/user-attachments/assets/04d64360-74a0-446f-9305-eca723df3e37" />

   In this Dashboard you can Navigate the Analysis get grasp of the following pages.

   
<img width="493" alt="2" src="https://github.com/user-attachments/assets/4c049973-84b4-4abc-a31c-306f361d2929" />

All bus informations been suggested in this dashboard where u can see where each stops is located, the count of the buses, the sheltered used in the stops, and Top 10 buses where they covers many stops and bottom 10.

Dax used:

1)Bus Caption = 
if (
    SELECTEDVALUE('Dynamic TopN'[Dynamic TopN Order])=0,
    "Top-10 BusLines with the Most Stops",
    "Bottom-10 BusLines with the Most Stops"
)

2)Total Stops per bus = 
COUNTROWS (
    FILTER (
        'Bus line',
        'Bus line'[Bus line code] = SELECTEDVALUE('Bus line'[Bus line code])
    )
)

3)TopN = 
    VAR _Ranking = 
    RANKX(
        ALL('Bus line'[Bus line code]),[Total Stops per bus],,DESC
    )
    RETURN 
    IF(_Ranking <= 10,[Total Stops per bus])

    4)Bottom N = 
    VAR _Ranking = 
    RANKX(
        ALL('Bus line'[Bus line code]),[Total Stops per bus],,ASC
    )
    RETURN 
    IF(_Ranking <= 10,[Total Stops per bus])

    5)Dynamic TopN = {
    ("Top Buses", NAMEOF('_Measure'[TopN]), 0),
    ("Bottom Buses", NAMEOF('_Measure'[Bottom N]), 1)
}

______________________________________



<img width="496" alt="3" src="https://github.com/user-attachments/assets/e39545c4-2208-435b-a8ff-ab56c54e9c26" />


All Metro informations been suggested in this dashboard where u can see where each station is located, the count of the Metrolines, station types and their count u, and Top metrolines where they covers many stations and bottom ones.


Dax used:

1)Metro Caption = 
if (
    SELECTEDVALUE('Dynamic Metro'[Dynamic Metro Order])=0,
    "Top 2 MetroLines with the Most Station",
    "Bottom 2 MetroLines with the Most Station"
)

2)Metro topN = 
    VAR _Ranking = 
    RANKX(
        ALL('Metro Routes'[Metro line number]),[Total Stations per Metro],,DESC
    )
    RETURN 
    IF(_Ranking <= 1,[Total Stations per Metro])

    3)Metro BottomN = 
    VAR _Ranking = 
    RANKX(
        ALL('Metro line'[Metro line number]),[Total Stations per Metro],,ASC
    )
    RETURN 
    IF(_Ranking <= 2, [Total Stations per Metro] )
    
    4)Total Stations per Metro = 
COUNTROWS (
    FILTER (
        'Metro line',
        'Metro line'[Metro line number] = SELECTEDVALUE('Metro line'[Metro line number])
    )
)
5)Dynamic Metro = {
    ("topN", NAMEOF('_Measure'[Metro topN]), 0),
    ("BottomN", NAMEOF('_Measure'[Metro BottomN]), 1)
}

_______________________
<img width="404" alt="4" src="https://github.com/user-attachments/assets/101ad064-e8da-4954-b883-43d1b4464188" />

This Dashboard offers a track of each bus-line or Metro-line and  overall mapping of the entire transport
