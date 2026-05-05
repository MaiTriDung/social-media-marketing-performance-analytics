# Social Media Marketing Performance Analytics Project

## 1. Project Overview

This project analyzes social media marketing performance for a global IT company across multiple platforms, content formats, content categories, hashtags, publishing time slots, and geographic regions.

The main goal is to identify which factors drive content performance and provide actionable recommendations to improve reach, engagement, and click performance.

The analysis focuses on answering four key business questions:

1. Which platforms and content formats generate the strongest overall performance?
2. Which content categories and platform-format combinations are most effective?
3. What are the best posting days and hours to maximize performance?
4. Which hashtags and regions show the strongest growth potential?

---

## 2. Business Problem

The company publishes different types of content such as videos, images, text posts, carousels, and live streams across platforms including YouTube, TikTok, Instagram, X.com, LinkedIn, and Facebook.

However, content performance is not consistent across platforms, formats, time slots, hashtags, and regions.

Therefore, the project aims to transform raw social media performance data into a structured analytics system that helps marketing stakeholders answer:

> What content should we post, where should we post it, when should we post it, and which markets or hashtags should we prioritize?

---

## 3. Dataset Description

The dataset contains social media post-level performance data, including:

- Platform information: YouTube, TikTok, Instagram, X.com, LinkedIn, Facebook
- Content metadata: content type, post type, content category, hashtag
- Timing information: post date, publish hour, publish timestamp
- Geographic information: region, latitude, longitude
- Performance metrics: impressions, views, engagement, likes, comments, shares, clicks, CTR, and engagement rate

Key metric definitions:

| Metric | Description |
|---|---|
| Impressions | Number of times content was displayed |
| Views | Number of times content was viewed or watched |
| Engagement | Total interactions, including likes, comments, and shares |
| Likes | Positive reactions to content |
| Comments | User responses or discussions |
| Shares | Number of times content was shared |
| Clicks | Number of user clicks |
| CTR (Tracked) | Click-through rate calculated only for posts with valid click-tracking data |
| Click Coverage | Percentage of posts with complete click-tracking data |
| ER Median | Median engagement rate across posts |

---

## 4. Analytics Framework

The dashboard is designed around four analytical layers.

### 4.1 Overview

The Overview page provides a high-level view of the entire social media system.

It answers:

- How many posts were published?
- What are the total impressions, views, and engagement?
- Which platforms dominate reach and engagement?
- Is performance growing or declining over time?
- Is performance dependent on a small number of viral posts?

### 4.2 Platform & Content Type Performance

This page analyzes the relationship between platform, post type, and content category.

It answers:

- Which content formats work best on each platform?
- Which content categories drive scale?
- Which combinations of platform, format, and category are the strongest?
- Which combinations are underperforming and should be optimized?

### 4.3 Time Slot & Posting Schedule

This page analyzes performance by day of week and post hour.

It answers:

- What are the best posting hours?
- Are there clear “golden hours” for engagement or reach?
- Do organic and sponsored posts behave differently by time slot?
- How should the publishing schedule be optimized?

### 4.4 Region & Hashtag

This page analyzes performance by geography and hashtag strategy.

It answers:

- Which regions generate the highest impressions, views, and engagement?
- Which hashtags are global winners?
- Which hashtags are only effective in specific contexts?
- Which markets should be scaled, localized, or further tested?

---

## 5. Data Pipeline

The project follows a layered data pipeline approach:

```text
Raw Dataset
    ↓
Power Query Preprocessing
    ↓
Python Data Cleaning & QA
    ↓
Staging Deduplicated Table
    ↓
BigQuery Data Modeling
    ↓
Power BI Dashboard
### 5.1 Power Query Preprocessing

Power Query was used as the first preprocessing layer before the Python pipeline.

The main purpose of this step was to create a composite business key called `Post_key`, which uniquely identifies each social media post across platforms.

`Post_key` was created by combining:

- Platform
- Post ID
- Published timestamp or cleaned post date

This was necessary because the raw `Post_ID` alone may not be sufficiently reliable for deduplication across multiple platforms.

```text
Post_key = Platform + Post_ID + Post_Published_At
```

This key is later used in Python for:

- duplicate detection
- staging-level deduplication
- data quality validation
- post-level analytics

---

### 5.2 Python Cleaning Layer

Python was used to clean, standardize, and validate the raw dataset before building the dashboard.

The cleaning process includes:

- converting numeric columns into proper numeric types
- standardizing `Engagement_Rate` into numeric decimal format
- identifying posts with valid click-tracking data
- creating `Traffic_scope` to separate tracked and non-tracked posts
- preparing the dataset for downstream analytics

Main output:

```text
RAW_clean.csv
```

This layer keeps the data close to the original structure while making it safer and more consistent for analysis.

---

### 5.3 Deduplication Layer

The staging layer removes duplicated posts based on `Post_key`.

The goal of deduplication is to ensure that each post is represented by only one reliable record in the analytics-ready dataset.

Instead of randomly removing duplicates, the pipeline uses a priority-based logic. When multiple records share the same `Post_key`, the pipeline keeps the record with:

1. valid click-tracking data
2. higher impressions
3. higher engagement
4. higher views
5. higher clicks

This approach ensures that the staging table keeps the most complete and informative version of each duplicated post.

Main output:

```text
STG_dedup.csv
```

This table is used as the main input for data modeling and dashboard development.

---

### 5.4 QA Outputs

Quality Assurance (QA) outputs were generated to validate data quality before building the dashboard.

These outputs help detect potential issues such as duplicate records, missing values, and incomplete click-tracking data.

| QA Output | Purpose |
|---|---|
| `QA_overview.csv` | Checks row counts, duplicate counts, and click data coverage |
| `QA_missingness_stg.csv` | Checks missing values by column in the staging table |
| `QA_missing_by_platform_stg.csv` | Checks Clicks and CTR missingness by platform |
| `QA_duplicate_post_key_sample_raw.csv` | Provides duplicate `Post_key` samples for manual validation |

These QA outputs help ensure that the dashboard is based on reliable and validated data.

---

## 6. Data Model

The project uses a star-schema-inspired data model to support scalable analytics and dashboard reporting.

The main tables include:

| Table | Description |
|---|---|
| `FactPostPerformance` | Main fact table containing post-level performance metrics |
| `DimPlatform` | Platform dimension table |
| `DimContent` | Content type, post type, and content category dimension |
| `DimGeo` | Geographic dimension table |
| `DimDate` | Date dimension table |

The fact table contains foreign keys such as:

- `platform_id`
- `content_id`
- `date_id`
- `geo_id`

This structure improves dashboard performance and makes the model easier to analyze across multiple dimensions such as platform, content, time, and geography.

---

## 7. Dashboard Design

The Power BI dashboard is organized into four main pages. Each page answers a different layer of the business question.

---

### 7.1 Performance Overview

The Overview page provides a high-level view of overall social media performance.

It helps stakeholders quickly understand:

- total impressions, views, engagement, and clicks
- overall engagement rate and CTR
- top-performing platforms
- performance trends over time
- the difference between scale and efficiency

Key visuals include:

- KPI cards
- platform performance comparison
- efficiency vs scale analysis
- trend over time
- funnel-style performance logic from impressions to views, engagement, and clicks

---

### 7.2 Platform & Content Type Performance

This page analyzes how content performance differs by platform, post type, and content category.

It answers:

- which platforms generate the strongest reach
- which content formats perform best on each platform
- which content categories drive scale and engagement
- which platform-content-format combinations should be scaled or optimized

Key visuals include:

- category performance by platform
- share vs performance bubble chart
- top platform-content-format combinations
- post type performance matrix

---

### 7.3 Time Slot & Posting Schedule

This page analyzes publishing time performance.

It answers:

- which hours generate the highest views and engagement
- whether there are clear golden hours
- how performance differs between organic and sponsored posts
- whether posting schedules should be adjusted by platform or content type

Key visuals include:

- performance by hour
- heatmap by day and hour
- time slot comparison
- organic vs sponsored timing analysis

---

### 7.4 Region & Hashtag

This page analyzes geographic performance and hashtag effectiveness.

It answers:

- which regions generate the highest reach and engagement
- which hashtags act as global performance drivers
- which hashtags work only in specific contexts
- whether content strategy should be localized by region

Key visuals include:

- top hashtag cards
- hashtag performance table
- regional performance scatter plot
- performance map by region
- region-platform-content comparison

---

## 8. Key Insights

### 8.1 Overview Insight

The system has strong overall scale, but performance quality differs significantly across platforms and content categories.

High total engagement does not always mean high engagement efficiency. Some categories generate large total numbers because they receive more reach, while others perform better on a per-post or engagement-rate basis.

---

### 8.2 Content Insight

Video is the main growth engine across the system, especially on YouTube, TikTok, and X.com.

However, per-post analysis shows that smaller formats such as articles, carousels, and selected image posts can also deliver strong efficiency in specific contexts.

This suggests that the content strategy should not rely only on total volume, but should also consider per-post productivity.

---

### 8.3 Timing Insight

Performance is concentrated around two main attention windows:

- late morning
- late afternoon

Organic posts are more sensitive to timing, while sponsored posts work best when they amplify strong organic time windows rather than replacing them.

This suggests that timing should be treated as a strategic lever, not only as an operational scheduling task.

---

### 8.4 Hashtag Insight

Hashtags such as `#ProductDemo` and `#CustomerStory` act as core performance drivers.

Some hashtags, such as `#WebinarReplay`, are not global scale drivers but perform strongly in specific contexts. These should be treated as contextual winners rather than general-purpose hashtags.

---

### 8.5 Region Insight

The same global content formula does not perform equally across all regions.

Some regions act as scale markets, while others require more localized platform, content, or hashtag strategies.

This suggests that the company should apply a global core strategy while allowing regional optimization.

---

## 9. Recommendations

### 9.1 Content Strategy

The company should keep video as the core scale engine, especially for Product Promotion, Educational, and Entertainment content.

At the same time, it should test and selectively scale high-efficiency formats such as:

- articles
- carousels
- selected image formats
- customer story formats

The goal is to build a balanced content portfolio instead of relying only on video-led scale.

---

### 9.2 Platform Strategy

Different platforms should have different strategic roles.

Recommended platform roles:

| Platform Type | Strategic Role |
|---|---|
| YouTube / TikTok / X.com | Scale and awareness engine |
| Instagram | Visual engagement and per-post efficiency |
| LinkedIn | Professional, article, and thought-leadership content |
| Facebook | Traffic and selected engagement use cases |

The company should avoid using the same content strategy across all platforms.

---

### 9.3 Timing Strategy

The publishing schedule should prioritize high-performing time windows.

Recommended actions:

- increase posting during late morning and late afternoon
- reduce posting in low-attention time slots
- use sponsored distribution to amplify strong organic posts
- test platform-specific posting schedules

The goal is to improve performance without necessarily increasing content volume.

---

### 9.4 Hashtag Strategy

Hashtags should be managed as a structured portfolio.

Recommended hashtag groups:

| Hashtag Type | Role |
|---|---|
| Core drivers | Hashtags that consistently drive scale |
| Engagement drivers | Hashtags that support deeper interaction |
| Contextual winners | Hashtags that work in specific platforms, regions, or campaigns |
| Experimental hashtags | Hashtags that require further testing |
| Low-priority hashtags | Hashtags with weak performance and limited strategic value |

This helps avoid over-investing in hashtags that only appear strong in small data slices.

---

### 9.5 Regional Strategy

The company should move from a one-size-fits-all global strategy to a global-core, local-optimization model.

Recommended actions:

- keep global content pillars consistent
- adjust platform weighting by region
- localize hashtag framing where needed
- build regional playbooks for different market types

This allows the company to preserve global scale while improving local relevance.

---

## 10. Tools & Technologies

| Tool | Purpose |
|---|---|
| Python | Data cleaning, deduplication, QA output generation |
| Pandas | Data transformation and profiling |
| NumPy | Missing value and numeric handling |
| Power Query | Initial preprocessing and composite key creation |
| Google BigQuery | Data warehouse and SQL modeling |
| SQL | Fact table and dimension modeling |
| Power BI | Dashboard development and business reporting |

---

## 11. Project Structure

```text
social-media-performance-analytics/
│
├── data/
│   ├── raw/
│   │   └── Social_Media_Content_Performance_Dataset_RAW.xlsx
│   │
│   ├── processed/
│   │   ├── RAW_clean.csv
│   │   ├── STG_dedup.csv
│   │   ├── FactPostPerformance.csv
│   │   ├── DimPlatform.csv
│   │   ├── DimContent.csv
│   │   └── DimGeo.csv
│
├── notebooks/
│   └── social_media_pipeline_portfolio.ipynb
│
├── scripts/
│   ├── social_media_raw_audit.py
│   └── social_media_pipeline.py
│
├── sql/
│   └── create_fact_post_performance.sql
│
├── powerbi/
│   └── social_media_performance_dashboard.pbix
│
├── docs/
│   ├── Data_Dictionary.xlsx
│   └── dashboard_screenshots/
│
└── README.md
```

---

## 12. How to Run the Project

### Step 1: Prepare the raw data

Place the raw dataset in the `data/raw/` folder.

### Step 2: Run the Python pipeline

```bash
python scripts/social_media_pipeline.py
```

This generates cleaned and staging-level output files.

### Step 3: Upload staging data to BigQuery

Upload `STG_dedup.csv` to BigQuery as the staging table.

### Step 4: Run SQL transformation

Run the SQL script to create the fact table and dimension-ready fields.

### Step 5: Connect Power BI

Connect Power BI to the processed tables and refresh the dashboard.

---

## 13. Auto-Refresh Design

The recommended production workflow is:

```text
Python Pipeline → BigQuery → Power BI Service → Scheduled Refresh
```

Power BI Service can be configured to refresh the dashboard daily after the data pipeline updates the warehouse table.

This turns the dashboard from a static report into an automated reporting system.

---

## 14. Business Value

This project helps marketing teams:

- identify winning platforms, formats, and content categories
- optimize posting schedules
- improve paid vs organic distribution strategy
- detect high-potential regions and hashtags
- reduce decision-making based on intuition
- build a repeatable reporting system for social media performance monitoring

---

## 15. Limitations

- Click-related metrics are only reliable for posts with valid tracking data.
- Hashtag performance may be affected by sample size.
- Regional analysis should be interpreted carefully if some markets have fewer posts.
- Dashboard insights are based on historical performance and should be validated through future A/B testing.
- The latest time period should be checked for data completeness before interpreting trend drops.

---

## 16. Future Improvements

Potential improvements include:

- automated pipeline scheduling
- incremental refresh in Power BI
- anomaly detection for sudden performance drops
- predictive modeling for post performance
- campaign-level ROI analysis
- recommendation logic for platform-content-time combinations
- A/B testing framework for content and posting time experiments

---

## 17. Author

Created by: [Your Name]  
Role: Data Analyst / Business Analytics Student  
Project Type: Data Analytics Portfolio Project

