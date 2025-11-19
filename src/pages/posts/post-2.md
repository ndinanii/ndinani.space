---
layout: ../../components/MarkdownPost.astro
title: "TechCo Account Console: Optimizing Workflow Efficiency"
author: 
  name: "NDINANI"
  url: "https://images.pexels.com/photos/935743/pexels-photo-935743.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2"
image:
  url: "https://images.pexels.com/photos/590022/pexels-photo-590022.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2"
  alt: "Salesforce Dashboard"
tags: ["Salesforce", "LWC", "Apex", "Visualforce"]
pubDate: 'Nov 19, 2025'
likes: '0'
comments: '0'
---

## Project Overview

Account Managers at TechCo were struggling with inefficient workflows, spending significant time navigating between multiple screens to gather critical decision-making data. This project focused on creating a "Single Pane of Glass" solution to eliminate context switching and improve productivity.

[**View Project on GitHub →**](https://github.com/ndinanii/salesforce-techco-account-console)

## The Business Challenge

The core problem was information architecture, not a lack of data. Account Managers had to navigate through a repetitive cycle of:

1.  Opening Account records
2.  Navigating to Related Opportunities
3.  Switching to Reports
4.  Returning to the Account list

This "swivel-chairing" resulted in approximately 15-20 minutes wasted daily per user, leading to frustration and delayed response times.

## Strategic Solution

The goal was to eliminate navigation while preserving data context. The solution was a **Hybrid Architecture** combining modern and legacy technologies where they fit best.

### Architecture Decisions

*   **Real-time Dashboard (LWC):** Chosen for performance and reactivity.
*   **Account Listing (Visualforce):** Utilized for specific assessment requirements and custom styling needs.
*   **Data Visualization (Pure CSS):** Selected to avoid external library dependencies and ensure instant loading.
*   **Data Layer (Apex):** Implemented with `@AuraEnabled(cacheable=true)` for Lightning Data Service caching.

## Technical Implementation

### 1. Dashboard Component (LWC)

To eliminate screen navigation, I built a responsive dashboard using LWC. It uses `@wire` adapters for reactive data binding and CSS Grid for layout.

```javascript
@wire(getAccountsWithOpportunities)
accounts; // Automatic reactivity

@wire(getOpportunitiesByStage)
wiredOpportunities({ error, data }) {
    if (data) {
        this.prepareChartData(); // Transform for visualization
    }
}
```

### 2. Efficient Data Retrieval (Apex)

To handle data without hitting governor limits, I used aggregate queries and wrapper classes.

```java
@AuraEnabled(cacheable=true)
public static List<OpportunityStageWrapper> getOpportunitiesByStage() {
    // Aggregate query - efficient GROUP BY
    List<AggregateResult> results = [
        SELECT StageName, COUNT(Id)
        FROM Opportunity
        WHERE IsDeleted = false
        GROUP BY StageName
    ];
    // Transform to wrapper class
}
```

### 3. Visual Data Representation

I implemented a pure CSS bar chart to visualize opportunity stages without heavy charting libraries.

```javascript
prepareChartData() {
    const total = this.opportunitiesData.reduce((sum, item) => sum + item.count, 0);
    this.chartLegendData = this.opportunitiesData.map((item, index) => ({
        stage: item.stage,
        count: item.count,
        percentage: ((item.count / total) * 100).toFixed(1),
        widthStyle: `width: ${(item.count / total) * 100}%;`
    }));
}
```

## Results & Impact

The implementation of the Account Console delivered immediate measurable benefits:

*   **Zero Navigation:** Routine decisions can now be made from a single screen.
*   **Time Savings:** Estimated 17 minutes saved per day per user.
*   **ROI:** For 50 users, this translates to approximately 3,692 hours saved annually.

## Reflection

This project demonstrated that effective Salesforce development isn't just about writing code—it's about understanding the business workflow. By shifting the focus from "what to build" to "what the user needs to see," we transformed a fragmented process into a streamlined experience.
