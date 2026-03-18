#DAX Measures

##DQ Distinct Countries 

DQ Distinct Countries = DISTINCTCOUNT(population_by_country_2020[Country])

##DQ Duplicate Countries

DQ Duplicate Countries = 
[DQ Total Rows] - [DQ Distinct Countries]

##DQ Missing Fertility

DQ Missing Fertility = 
VAR c =
    COUNTROWS(
        FILTER(
            population_by_country_2020,
            ISBLANK(population_by_country_2020[Fert. Rate])
        )
    )
RETURN COALESCE(c, 0)

##DQ Missing Key Fields

DQ Missing Key Fields = 
VAR c =
    COUNTROWS(
        FILTER(
            population_by_country_2020,
            ISBLANK(population_by_country_2020[Country])
                || ISBLANK(population_by_country_2020[Population_2020])
        )
    )
RETURN COALESCE(c, 0)

##DQ Missing Median Age

DQ Missing Median Age = 
VAR c =
    COUNTROWS(
        FILTER(
            population_by_country_2020,
            ISBLANK(population_by_country_2020[Med. Age])
        )
    )
RETURN COALESCE(c, 0)

##DQ Missing Migrants

DQ Missing Migrants = 
COUNTROWS(
    FILTER(
        population_by_country_2020,
        ISBLANK(population_by_country_2020[Migrants (net)])
    )
)

##DQ Total Rows

DQ Total Rows = COUNTROWS(population_by_country_2020)

##Population (M)

Population (M) = DIVIDE(SUM(population_by_country_2020[Population_2020]), 1000000)
