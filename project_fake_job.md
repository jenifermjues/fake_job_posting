
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

    ##   job_id                                title         location  department
    ## 1  13749    Embedded and Application Engineer NZ, N, Auckland  Engineering
    ## 2  15149 Community Manager & Customer Support US, NY, New York            
    ## 3  12808         Business Development Manager        AU, VIC,             
    ##   salary_range
    ## 1             
    ## 2  55000-70000
    ## 3             
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  company_profile
    ## 1 Want to be part of a NZ success story thatâ\200\231s going places?Want to have a hand in developing products that youâ\200\231ll be proud of?We are a driven and ambitious technology business with a Vision to deliver revolutionary transactional and self service products that make people wonder how they ever lived without them.Designed in New Zealand and exported across the world, our products have an enviable history of delivering smart and robust technology solutions to the oil and gas retail sector. We have developed many first-in-world products and we are embarking on our next strategic horizon - so we have exciting and challenging times ahead!Types of roles we recruit for;Embedded and Application EngineersMechanical, Hardware and Production EngineersSoftware Developers (particularly Java Devâ\200\231s with payments experience)Product ArchitectsQA &amp; Compliance (including Test Analysts / Test Engineers)Project Managers (software and hardware)Solutions Consultants (Business Analysts)Plus much much moreWe believe in the importance of living and breathing our Company Values; weâ\200\231re Passionate, we do What We Say, weâ\200\231re Straight Up, weâ\200\231re Creative, weâ\200\231re Team players, weâ\200\231re all about Quality, we make it Win-Win and People Matter to us.
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             BoweryÂ is an easier way to set up your development environment.Â 
    ## 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      We are experts in enterprise systems management for the desktop, mobility, datacentre + cloud. We are a young and dynamic workplace, with a strong culture of technical brilliance, sharing, learning, and well, having fun at the same time. Our team is based in Melbourne, Australia. If you have awesome skills in virtualisation and management, and you want to part of the Olikka team, apply now.
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     description
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 We are a driven and ambitious technology business with a Vision to deliver revolutionary transactional and self service products that make people wonder how they ever lived without them.Designed in New Zealand and exported across the world, our products have an enviable history of delivering smart and robust technology solutions. We have developed many first-in-world products and have a long history of innovative site automation solutions. We are embarking on our next strategic horizon - implementing cloud and mobile strategies to retain our leadership and recognised innovation, so we have exciting and challenging times ahead.In thisÂ key role, the Embedded and Application Engineer will play a vital role in building and maintaining embedded software solutions. You will be responsible for embedded product maintenance, completing the development of new functionality and modifications to existing functionality on embedded devices, updating regression/unit test suites, software documentation and the creation of developer test plans. This role will give you exposure to a new platform and enable you provide expert input into development.
    ## 2 Bowery is an easier way to set up your development environment. We're venture-backed and looking for a self-driven and excited customer-experience lead to engage our community and make users happy.And why would you want to work here?Work on something that matters. You're not the type of person who wants to work on another image sharing app or social network for dogs. You want to create tools that developers around the world love and share. Build a dev tool that you love using and everyone else will love it too.Work with a smart team who cares.Â The average age of our team is 21.75. We've worked at companies like Medium, Poptip, and Jawbone, and we enjoy working with people who care about the work they do.Be judged on the work you do, not where or when you do it.Â There's no bureaucracy or approved holiday time. We're all measured by metrics and the work we do, not what time you get into the office. That's the advantage of hiring the smartest engineers we know.As part of this position, you will:Formalize and manage all aspects of customer experienceAnswer customer support questions and comments over email and live chatEstablish process to measure customer service performance and continuously drive strategies to improve itOwn social media presence and actively engage community to build loyalty on Twitter, Github, etc.Manage company blog, write original content, and find others in the developer community who can write guest posts and contribute contentConceptualize new marketing strategies and promotional plans (both offline and online)Help our engineering and design teams prioritize new features and bug fixes based on customer feedback
    ## 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  An Olikka New Business/Account Manager is considered an integral part to the sales team function, and will form a crucial role in taking Olikka to the next level and the success of the business. The New Business/Account Manager is a motivated individual with enthusiasm and confidence to lead sales and not only achieve but exceed targets and KPIs set by the business.The Olikka New Business/Account Manager will have demonstrated experience within the IT industry, selling solutions and products and have a willingness to learn and adapt to new technologies as they emerge. An understanding of both Microsoft and Citrix technologies will be a valuable asset.In addition, the Olikka New Business/Account Manager will have experience in developing sales strategies and building new business relationships. They will also be a strong communicator and are adept at communicating business value of our solutions in a way that is extremely easy for our customers to understand.
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 requirements
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        As an expert in Embedded DevelopmentÂ you will have the following experience:Strong working knowledge of C/C++ and Assembler languagesExcellent understanding of electronics, with the ability to interpret electronic schematicsAwareness of the fundamentals of digital designExperience in RTOS or embedded OSesEmbedded Linux x86/ARMIt goes without saying that you are a confident team player with the ability to interact with internal and external clients alike. Your open personality, outstanding decision making skills and communicative approach will see you succeed in this role.
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    You're familiar with codingâ\200”maybe you've taken a class in school, or watched some videos online. The more familiarity with web development, the better.Strong writing and interpersonal skillsAbility to troubleshoot customer problems, sometimes under pressureSelf-starter who is comfortable working independently in unstructured environmentsExperience with helping customersNYC-based a plus, but not necessaryPrevious experience in customer support a plus
    ## 3 The Olikka New Business/Account Manager will be responsible but not limited to the following:Continually look to identify and establish new business relationships with key influencersUse existing networks and industry contacts to generate new businessAct promptly on leads provided by Partners (Citrix and Microsoft)Plan, design and conduct a defined sales strategy to ensure sales targets set by management are metSustain a good understanding of current and upcoming technologies, services and productsRecognise the sales process to proactively and accurately engage with customers about next purchase decisionsMaintain up to date information in the CRM database for management of the sales cycle, pipeline and sales targetsPrepare and provide sales proposals in a timely mannerCoordinate with Consultants and Technical Specialists where necessary to meet customer and business needs and expectationsParticipate in sales, marketing and networking events designed to assist Olikka in gaining exposure and a greater market shareSupport and implement marketing initiatives as required
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                benefits
    ## 1 We are in an exciting growth phase, if you would like the opportunity to work for an organisation where your skills and performance will be recognised, an organisation that believes in investing in your learning and development, then we would like to hear from you!City fringe location - based in PonsonbyEmployee Wellbeing ProgrammeActive Social ClubPerformance based pay, training and development opportunities, challenging work, flexible work hours, paid birthday leave, discounted medical insurance, discounted Gym membership, Cafe discounts and access to EAP services.We believe in the importance of living our Company Values; weâ\200\231re Passionate, we do What We Say, weâ\200\231re Straight Up, weâ\200\231re Creative, weâ\200\231re Team players, weâ\200\231re all about Quality, we make it Win-Win and People Matter to us.If this sounds like you and you want to work with a passionate group of people who work hard to get projects across the line; do what needs to be done to deliver successfully and have fun while doing it, then apply today!#URL_5986f170772b5bd01bbbe5dcef6d24f90be00a45753fa426e2c4ec5453248cd6#
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Happy.Â Work with a fast-growing team to build a product with thousands of users.Healthy.Â Full health and dental coverageâ\200”we want you to be healthy.Productive.Â Your workstation of choiceâ\200”use the tools that make you most efficient at your job. And we work out ofÂ Work-bench, an awesome co-working space in the heart of New York City that has the coolest espresso machine ever.Wherever.Â Relocation supportâ\200”if you want to move NYC, we'll help you out.
    ## 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      
    ##   telecommuting has_company_logo has_questions employment_type
    ## 1             0                1             1       Full-time
    ## 2             0                1             1       Full-time
    ## 3             0                1             0                
    ##   required_experience required_education                            industry
    ## 1           Associate  Bachelor's Degree Information Technology and Services
    ## 2         Entry level        Unspecified                   Computer Software
    ## 3                                                                           
    ##          function. fraudulent
    ## 1      Engineering          0
    ## 2 Customer Service          0
    ## 3                           0

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
    ## 1  17417             0                1             1          0
    ## 2  12755             0                0             0          0
    ## 3   4597             0                1             1          0
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   full_text
    ## 1 Senior Web Developer (Back End/Infrastructure) GR Web Development competitive salary and option pool schemepaid vacation according to greek law, plus public holidaysaccess to free books and resources for professional and personal developmentopportunities to attend conferences, internal and external trainings, workshops, etc.vibrant company culture, weekly team events and more! competitive salary and option pool schemepaid vacation according to greek law, plus public holidaysaccess to free books and resources for professional and personal developmentopportunities to attend conferences, internal and external trainings, workshops, etc.vibrant company culture, weekly team events and more! competitive salary and option pool schemepaid vacation according to greek law, plus public holidaysaccess to free books and resources for professional and personal developmentopportunities to attend conferences, internal and external trainings, workshops, etc.vibrant company culture, weekly team events and more! competitive salary and option pool schemepaid vacation according to greek law, plus public holidaysaccess to free books and resources for professional and personal developmentopportunities to attend conferences, internal and external trainings, workshops, etc.vibrant company culture, weekly team events and more! Full-time Not Applicable Unspecified Information Technology and Services Information Technology
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Mechanical Engineer US NA NA NA NA NA Full-time NA NA Mechanical or Industrial Engineering NA
    ## 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       English Teacher Abroad  US NA see job description see job description see job description see job description Contract NA Bachelor's Degree Education Management NA

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
        cex.names=0.7, 
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
