
# Introduction

# Initial Questions

-   What are the significant features of classifying fake job posting
-   Which classification model is the best to classify fake job posting

# Objectives

-   To identify key features of fraudulent job postings
-   To build a model to classify real or fake job postings

# Data Cleaning and Pre-processing

## Import libraries

## Load data

``` r
df <- read.csv("https://raw.githubusercontent.com/abbylmm/fake_job_posting/main/data/fake_job_postings.csv")
```

## Summary data

``` r
df_fake_job <- df
sample_n(df_fake_job, 3)
```

    ##   job_id                                   title        location  department
    ## 1  11911                Audio-visual technician         SA, 01,             
    ## 2   6881                Subsea Pipeline Engineer US, TX, Houston Engineering
    ## 3  16453 Home-based Inbound Sales Representative          NZ, ,   Homeworker
    ##   salary_range
    ## 1  36000-54000
    ## 2             
    ## 3             
    ##                                                                                                                                                                                                                                         company_profile
    ## 1                                                                                                                                                                                                                                                      
    ## 2                                                                                                                                                                                                                                                      
    ## 3 CallCentre People Recruitment is recognised as being specialists within the CallCentre industry. Â We provide permanent, temporary, contract and management staff for a number of large national and multi-national businesses in various industries.
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     description
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   As an audio-visual technician you would install and operate multimedia equipment, such as video, TV, sound equipment and lighting at venues like conference centres ... etc
    ## 2 Â Ability to make decisions and recommendations that are recognized as authoritative and have an important impact on extensive engineering activities.Ability to initiate and maintains extensive contacts with key engineers and officials of other organizations and companies, requiring skill in persuasion and negotiation of critical issues.Demonstrable creativity, foresight, and mature engineering judgment in anticipating and solving unprecedented engineering problems, determining program objectives and requirements, organizing programs and projects, and developing standards and guides for diverse engineering activities.Periodically serves as mentor or coach to younger staff enabling them to achieve their professional goals.Occasionally involved in recruitment to meet resource requirements.Interfaces closely with Clients and works to develop INTECSEA.Plays a central role in bid preparation and resource estimating.Anticipates and resolves staffing requirements and schedule constraints.Establishes deadlines, milestones, and man-hour estimates.Works closely with Client staff to ensure alignment of approach and objectives.
    ## 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          - Work from home anywhere in New Zealand! - 25 â\200“ 30 hours a week - 7 days a week availableÂ  - Competitive hourly rate - New Year Start Your skilled approach to relationship building and problem solving will assist you in achieving your goals each and every time you are working. This is an exciting opportunity for experienced customer service and sales reps that are looking for the flexibility of working from home.
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           requirements
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           â\200¢excellent technical skills with electrical equipment and IT  â\200¢creative problem-solving ability  â\200¢organisational skills  â\200¢the ability to work well as part of a team and also on your own initiative  â\200¢the ability to work under pressure and to deadlines  â\200¢a flexible approach for dealing with varied tasks  â\200¢an awareness of electrical safety issues  â\200¢good communication and customer care skills.Â 
    ## 2 Desired Skills &amp; Experience:Ability to lead at all levels within the organization.Proven track record of exceeding performance metrics.Job RequirementsTechnical Requirements:Subsea pipeline background that involves piping stress analysis using a program like OffPipe.Ability to travel offshore during construction phase, 10% of the time maybe lessMust be able to demonstrate full project management capabilities, survey, permitting in the GOM, design, procurement, contracts, field construction, cost.Plan, schedule and conduct Engineering during; Conceptual, Pre-FEED, FEED, Detailed Design and Installation phases.Provide technical expertise to your team and our clients.Education &amp; Experience:Bachelors of Science in Mechanical Engineering or related field + 10 years relevant experience.20 years relevant experience in lieu of degree.QHSE Requirements:Learns &amp; actively promotes the INTECSEA EMS and HSE in accordance with the HSE Guideline for INTECSEA Personnel.
    ## 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          The following experience and personal qualities would be advantageous in securing this role: - Proven experience in a call centre position (required) - Excellent communication skills and rapport building skills - The confidence and the resilience to close a saleÂ  - The confidence to deal with difficult customers - A drive to exceed sales targets and proven experience of having done so - Motivated and capable of working independently - Good work ethic and time management skills - Strong computer skills
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    benefits
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       Salary Valuation3000 up to 4500 SAR
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
    ## 3 What do you require: - Landline home phone - Broadband Internet - Laptop or PC running a windows operating system - Internet Explorer version 8, 9 or 10 (11 not compatible) - Wired home phone with headset (recommended) - 13â\200\235(or larger) laptop or PC Monitor for ease of viewing (recommended) You must be able to work a minimum of 25 hours a week and meet our clients technical skill requirements.Â  We are looking for people who are available 8am to 10pm, Monday through Sunday on a rotating roster Training and ongoing coaching will be provided via webinars and e-learning. Applicants are able to be based anywhere in NZ! If this sounds like you or you want to know more get in touch with us now. Applicants for this position should have NZ residency or a valid NZ work visa.
    ##   telecommuting has_company_logo has_questions employment_type
    ## 1             0                1             0       Full-time
    ## 2             0                0             1                
    ## 3             0                1             1       Temporary
    ##   required_experience required_education                            industry
    ## 1           Associate  Bachelor's Degree Information Technology and Services
    ## 2                                                                           
    ## 3         Entry level                                      Consumer Services
    ##                function. fraudulent
    ## 1 Information Technology          0
    ## 2                                 1
    ## 3                                 0

``` r
summary(df_fake_job)
```

    ##      job_id         title             location          department       
    ##  Min.   :    1   Length:17880       Length:17880       Length:17880      
    ##  1st Qu.: 4471   Class :character   Class :character   Class :character  
    ##  Median : 8940   Mode  :character   Mode  :character   Mode  :character  
    ##  Mean   : 8940                                                           
    ##  3rd Qu.:13410                                                           
    ##  Max.   :17880                                                           
    ##  salary_range       company_profile    description        requirements      
    ##  Length:17880       Length:17880       Length:17880       Length:17880      
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##    benefits         telecommuting    has_company_logo has_questions   
    ##  Length:17880       Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  Class :character   1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:0.0000  
    ##  Mode  :character   Median :0.0000   Median :1.0000   Median :0.0000  
    ##                     Mean   :0.0429   Mean   :0.7953   Mean   :0.4917  
    ##                     3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:1.0000  
    ##                     Max.   :1.0000   Max.   :1.0000   Max.   :1.0000  
    ##  employment_type    required_experience required_education   industry        
    ##  Length:17880       Length:17880        Length:17880       Length:17880      
    ##  Class :character   Class :character    Class :character   Class :character  
    ##  Mode  :character   Mode  :character    Mode  :character   Mode  :character  
    ##                                                                              
    ##                                                                              
    ##                                                                              
    ##   function.           fraudulent     
    ##  Length:17880       Min.   :0.00000  
    ##  Class :character   1st Qu.:0.00000  
    ##  Mode  :character   Median :0.00000  
    ##                     Mean   :0.04843  
    ##                     3rd Qu.:0.00000  
    ##                     Max.   :1.00000

## Check all the missing values - ‘empty’

``` r
skim(df_fake_job)
```

|                                                  |             |
|:-------------------------------------------------|:------------|
| Name                                             | df_fake_job |
| Number of rows                                   | 17880       |
| Number of columns                                | 18          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |             |
| Column type frequency:                           |             |
| character                                        | 13          |
| numeric                                          | 5           |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |             |
| Group variables                                  | None        |

Data summary

**Variable type: character**

| skim_variable       | n_missing | complete_rate | min |   max | empty | n_unique | whitespace |
|:--------------------|----------:|--------------:|----:|------:|------:|---------:|-----------:|
| title               |         0 |             1 |   3 |   142 |     0 |    11231 |          0 |
| location            |         0 |             1 |   0 |   161 |   346 |     3106 |          0 |
| department          |         0 |             1 |   0 |   255 | 11547 |     1338 |          6 |
| salary_range        |         0 |             1 |   0 |    20 | 15012 |      875 |          0 |
| company_profile     |         0 |             1 |   0 |  6230 |  3308 |     1710 |          0 |
| description         |         0 |             1 |   3 | 22722 |     0 |    14802 |          0 |
| requirements        |         0 |             1 |   0 | 10921 |  2694 |    11970 |          0 |
| benefits            |         2 |             1 |   0 |  4489 |  7206 |     6207 |          0 |
| employment_type     |         0 |             1 |   0 |     9 |  3471 |        6 |          0 |
| required_experience |         0 |             1 |   0 |    16 |  7050 |        8 |          0 |
| required_education  |         0 |             1 |   0 |    33 |  8105 |       14 |          0 |
| industry            |         0 |             1 |   0 |    36 |  4903 |      132 |          0 |
| function.           |         0 |             1 |   0 |    22 |  6455 |       38 |          0 |

**Variable type: numeric**

| skim_variable    | n_missing | complete_rate |    mean |      sd |  p0 |     p25 |    p50 |      p75 |  p100 | hist  |
|:-----------------|----------:|--------------:|--------:|--------:|----:|--------:|-------:|---------:|------:|:------|
| job_id           |         0 |             1 | 8940.50 | 5161.66 |   1 | 4470.75 | 8940.5 | 13410.25 | 17880 | ▇▇▇▇▇ |
| telecommuting    |         0 |             1 |    0.04 |    0.20 |   0 |    0.00 |    0.0 |     0.00 |     1 | ▇▁▁▁▁ |
| has_company_logo |         0 |             1 |    0.80 |    0.40 |   0 |    1.00 |    1.0 |     1.00 |     1 | ▂▁▁▁▇ |
| has_questions    |         0 |             1 |    0.49 |    0.50 |   0 |    0.00 |    0.0 |     1.00 |     1 | ▇▁▁▁▇ |
| fraudulent       |         0 |             1 |    0.05 |    0.21 |   0 |    0.00 |    0.0 |     0.00 |     1 | ▇▁▁▁▁ |

## Split location to country, state, city and fill empty with NA

``` r
df_fake_job[c("country", "state", "city")] <- str_split_fixed(df_fake_job$location, ", ", 3)
df_fake_job[c("country", "state", "city")][df_fake_job[c("country", "state", "city")] == ""] <- NA
```

## Split salary_range to min_salary, max_salary and fill empty with NA

``` r
df_fake_job[c("min_salary", "max_salary")] <- str_split_fixed(df_fake_job$salary_range, "-", 2)
df_fake_job[c("min_salary", "max_salary")][df_fake_job[c("min_salary", "max_salary")] == ""] <- NA
```

## Drop location and salary_range

``` r
df_fake_job <- select(df_fake_job, -c(location, salary_range))
```

## Convert to lowercase string

``` r
cols <- c("company_profile", "description", "requirements", "benefits")
for (x in df_fake_job[cols]) {
  df_fake_job[cols] <- tolower(x)
}
```

## View the structure of data

``` r
glimpse(df_fake_job)
```

    ## Rows: 17,880
    ## Columns: 21
    ## $ job_id              <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15,~
    ## $ title               <chr> "Marketing Intern", "Customer Service - Cloud Vide~
    ## $ department          <chr> "Marketing", "Success", "", "Sales", "", "", "ANDR~
    ## $ company_profile     <chr> "", "what you will get from usthrough being part o~
    ## $ description         <chr> "", "what you will get from usthrough being part o~
    ## $ requirements        <chr> "", "what you will get from usthrough being part o~
    ## $ benefits            <chr> "", "what you will get from usthrough being part o~
    ## $ telecommuting       <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ has_company_logo    <int> 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1,~
    ## $ has_questions       <int> 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 0,~
    ## $ employment_type     <chr> "Other", "Full-time", "", "Full-time", "Full-time"~
    ## $ required_experience <chr> "Internship", "Not Applicable", "", "Mid-Senior le~
    ## $ required_education  <chr> "", "", "", "Bachelor's Degree", "Bachelor's Degre~
    ## $ industry            <chr> "", "Marketing and Advertising", "", "Computer Sof~
    ## $ function.           <chr> "Marketing", "Customer Service", "", "Sales", "Hea~
    ## $ fraudulent          <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ country             <chr> "US", "NZ", "US", "US", "US", "US", "DE", "US", "U~
    ## $ state               <chr> "NY", NA, "IA", "DC", "FL", "MD", "BE", "CA", "FL"~
    ## $ city                <chr> "New York", "Auckland", "Wever", "Washington", "Fo~
    ## $ min_salary          <chr> NA, NA, NA, NA, NA, NA, "20000", NA, NA, NA, "1000~
    ## $ max_salary          <chr> NA, NA, NA, NA, NA, NA, "28000", NA, NA, NA, "1200~

``` r
class(df_fake_job)
```

    ## [1] "data.frame"

## View column names

``` r
names(df_fake_job)
```

    ##  [1] "job_id"              "title"               "department"         
    ##  [4] "company_profile"     "description"         "requirements"       
    ##  [7] "benefits"            "telecommuting"       "has_company_logo"   
    ## [10] "has_questions"       "employment_type"     "required_experience"
    ## [13] "required_education"  "industry"            "function."          
    ## [16] "fraudulent"          "country"             "state"              
    ## [19] "city"                "min_salary"          "max_salary"

## Check if any duplication id

``` r
table(duplicated(df_fake_job$job_id))
```

    ## 
    ## FALSE 
    ## 17880

``` r
### there is no duplication id
```

## Check for total missing values for each feature

``` r
colSums(is.na(df_fake_job))
```

    ##              job_id               title          department     company_profile 
    ##                   0                   0                   0                   2 
    ##         description        requirements            benefits       telecommuting 
    ##                   2                   2                   2                   0 
    ##    has_company_logo       has_questions     employment_type required_experience 
    ##                   0                   0                   0                   0 
    ##  required_education            industry           function.          fraudulent 
    ##                   0                   0                   0                   0 
    ##             country               state                city          min_salary 
    ##                 346                2580                2067               15012 
    ##          max_salary 
    ##               15013

``` r
### there are two missing values in 'benefits' column
```

## Populate missing rates for each feature

``` r
colSums(is.na(df_fake_job)/length(df_fake_job)*100)
```

    ##              job_id               title          department     company_profile 
    ##             0.00000             0.00000             0.00000             9.52381 
    ##         description        requirements            benefits       telecommuting 
    ##             9.52381             9.52381             9.52381             0.00000 
    ##    has_company_logo       has_questions     employment_type required_experience 
    ##             0.00000             0.00000             0.00000             0.00000 
    ##  required_education            industry           function.          fraudulent 
    ##             0.00000             0.00000             0.00000             0.00000 
    ##             country               state                city          min_salary 
    ##          1647.61905         12285.71429          9842.85714         71485.71429 
    ##          max_salary 
    ##         71490.47619

## List rows with missing values

``` r
missingdf <- df_fake_job[!complete.cases(df_fake_job), ]
```

## Visualize missing values

``` r
gg_miss_var(df_fake_job, show_pct = TRUE) + labs(y = "% Missing")
```

    ## Warning: It is deprecated to specify `guide = FALSE` to remove a guide. Please
    ## use `guide = "none"` instead.

![](project_fake_job_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

## Merge columns and create a new ‘full_text’ column

``` r
viz_df <- select(df_fake_job, -c(max_salary, min_salary, state, city))
viz_df[viz_df == ""] <- NA
viz_df$full_text <- 
  paste(viz_df$title, 
        viz_df$country, 
        viz_df$department, 
        viz_df$company_profile, 
        viz_df$description, 
        viz_df$requirements, 
        viz_df$benefits, 
        viz_df$employment_type, 
        viz_df$required_experience, 
        viz_df$required_education, 
        viz_df$industry, 
        viz_df$function.)
# sample(viz_df, 3)
# write.csv(viz_df, "C:/Users/munmu/Documents/GitHub/fake_job_posting\\viz_df.csv", row.names = FALSE)
```

## Visualize missing profile for each feature

``` r
plot_missing(viz_df)
```

![](project_fake_job_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

## Drop columns

``` r
model_df <- select(viz_df, 
                   -c(title, 
                      country, 
                      department, 
                      company_profile, 
                      description, 
                      requirements, 
                      benefits, 
                      employment_type, 
                      required_experience, 
                      required_education, 
                      industry, 
                      function.))
sample_n(model_df, 3)
```

    ##   job_id telecommuting has_company_logo has_questions fraudulent
    ## 1   8889             0                1             0          0
    ## 2    193             0                0             0          0
    ## 3    777             0                1             1          0
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   full_text
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        SAP BI Consultant US NA NA NA NA NA NA NA NA NA NA
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    Manager, Network Engineering  US NA comprehensive benefits package available. comprehensive benefits package available. comprehensive benefits package available. comprehensive benefits package available. Full-time Mid-Senior level Bachelor's Degree Hospital & Health Care Information Technology
    ## 3 Construction Management - West/Northwest Chicagoland US Sales what we offer for your hard work:an excellent compensation package, with secured and guaranteed high earnings, vacations, bonuses.serious income to start 50k plus percentage of profit, plus percentage of your teams profit. (high potential)year round full time work, no seasonal work here!weekly compensation payout after the first two weeks of employment. direct deposit available.excellent new manager training by your co managers and sales director.need a pickup truck, no problem! we offer truck rental/lease assistance program.develop territory which leads to a path of branch management.â relaxed and comfortable work environment with casual business dress.dedicated support team that ensures you have everything you need to be successful. what we offer for your hard work:an excellent compensation package, with secured and guaranteed high earnings, vacations, bonuses.serious income to start 50k plus percentage of profit, plus percentage of your teams profit. (high potential)year round full time work, no seasonal work here!weekly compensation payout after the first two weeks of employment. direct deposit available.excellent new manager training by your co managers and sales director.need a pickup truck, no problem! we offer truck rental/lease assistance program.develop territory which leads to a path of branch management.â relaxed and comfortable work environment with casual business dress.dedicated support team that ensures you have everything you need to be successful. what we offer for your hard work:an excellent compensation package, with secured and guaranteed high earnings, vacations, bonuses.serious income to start 50k plus percentage of profit, plus percentage of your teams profit. (high potential)year round full time work, no seasonal work here!weekly compensation payout after the first two weeks of employment. direct deposit available.excellent new manager training by your co managers and sales director.need a pickup truck, no problem! we offer truck rental/lease assistance program.develop territory which leads to a path of branch management.â relaxed and comfortable work environment with casual business dress.dedicated support team that ensures you have everything you need to be successful. what we offer for your hard work:an excellent compensation package, with secured and guaranteed high earnings, vacations, bonuses.serious income to start 50k plus percentage of profit, plus percentage of your teams profit. (high potential)year round full time work, no seasonal work here!weekly compensation payout after the first two weeks of employment. direct deposit available.excellent new manager training by your co managers and sales director.need a pickup truck, no problem! we offer truck rental/lease assistance program.develop territory which leads to a path of branch management.â relaxed and comfortable work environment with casual business dress.dedicated support team that ensures you have everything you need to be successful. Full-time Mid-Senior level High School or equivalent Construction Sales

``` r
# write.csv(model_df, "C:/Users/munmu/Documents/GitHub/fake_job_posting\\model_df.csv", row.names = FALSE)
```

## Check NA or missing values

``` r
sum(is.na(model_df))
```

    ## [1] 0

``` r
sum(model_df == "")
```

    ## [1] 0

## Visualize missing values

``` r
vis_miss(model_df)
```

    ## Warning: `gather_()` was deprecated in tidyr 1.2.0.
    ## Please use `gather()` instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was generated.

![](project_fake_job_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
vis_dat(model_df)
```

![](project_fake_job_files/figure-gfm/unnamed-chunk-18-2.png)<!-- -->

# Exploratory Data Analysis (EDA)

## Visualize Fraud and Real

``` r
viz_df$fraudulent[viz_df$fraudulent == 1] <- "Yes"
viz_df$fraudulent[viz_df$fraudulent == 0] <- "No"
count <- table(viz_df$fraudulent)
barplot(count, 
        main="Real and Fraudulent", 
        xlab="fraudulent", 
        ylab="count", 
        col="#69b3a2")
```

![](project_fake_job_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

## Visualize Country-wise Job Posting

``` r
temp <- na.omit(subset(viz_df, select = c(country, job_id))) %>% 
  group_by(country) %>% 
  summarize(n = n()) %>% 
  arrange(desc(n)) %>% 
  slice(1:10)

barplot(height=temp$n, 
        main="Top 10 Country-wise Job Posting", 
        ylab="count", 
        col=brewer.pal(10, "Set2"), 
        names.arg=c("United States",
                    "United Kingdom",
                    "Greece",
                    "Canada",
                    "Germany",
                    "New Zealand",
                    "India",
                    "Australia",
                    "Philippines",
                    "Netherlands"), 
        cex.names=0.8, 
        las=2
)
```

    ## Warning in brewer.pal(10, "Set2"): n too large, allowed maximum for palette Set2 is 8
    ## Returning the palette you asked for with that many colors

![](project_fake_job_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

## Visualize the required experiences in the jobs

``` r
temp <- na.omit(subset(viz_df, select = c(required_experience, job_id))) %>% 
  group_by(required_experience) %>% 
  summarize(n = n()) %>% 
  arrange(desc(n))

barplot(height=temp$n, 
        names=temp$required_experience, 
        main="No. of jobs with different experience levels", 
        ylab="count", 
        col=brewer.pal(7, "Set2"), 
        cex.names=0.6, 
        las=2
)
```

![](project_fake_job_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

# Modeling

## Classification

## Regression

# Data Prediction

# Evaluation
