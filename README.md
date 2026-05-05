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


