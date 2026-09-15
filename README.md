# Marketing_Analysis
This project looks at 1,000 marketing campaign records across 8 campaign types, 6 regions, and 6 industries, split between digital and traditional channels. The same dataset was analyzed three ways: SQL queries, an Excel workbook, and a Power BI dashboard. This file pulls together the actual findings, not just the numbers.

Key Insights
1. Traditional campaigns have a real edge over digital, and it's not just chance
The KPI tables show traditional campaigns returning 71.79% ROI compared to 62.31% for digital, on a combined spend of 8.83M for traditional versus 16.87M for digital. That's already a meaningful gap, but a gap in a summary table could still be a fluke.
To check that, I ran a two sample t-test comparing the average ROI of every individual campaign record, treating each one equally regardless of how much was spent on it. Digital campaigns averaged 62.12% ROI, traditional campaigns averaged 69.30%. The test gave a p-value of 0.026 (two tail), which is below the usual 0.05 cutoff. In plain terms, there's less than a 3% chance this gap happened by random luck. So both the simple comparison and the statistical test agree on the same direction: traditional media is outperforming digital in this dataset.

2. Spending more doesn't make a campaign more efficient
I checked the correlation between spend and ROI across all 1,000 records and got 0.036, which is close to zero. That means how much a campaign spends tells you almost nothing about how good its return will be. A campaign with a small budget can be just as efficient, or more efficient, than one with a huge budget. This points to campaign strategy and execution mattering more than budget size.

3. Two ways to measure ROI, and why they're both here
You'll notice two different ROI numbers for traditional vs digital: 71.79% and 62.31% in the KPI tables, but 69.30% and 62.12% in the t-test. Both are correct, they just answer different questions.
The KPI tables use a spend-weighted ROI. It's calculated from total revenue divided by total spend across everything, so it reflects the actual return on the whole marketing budget, and naturally gives more influence to bigger campaigns.
The t-test uses an equal-weighted average, where every campaign record counts the same regardless of its budget. This is the fairer way to test whether the difference between digital and traditional is statistically real, since one or two massive campaigns can't skew the result.
The fact that both methods point the same direction (traditional ahead of digital) is what makes this finding solid rather than an artifact of how the average was calculated.

Notes on the Data

Why 52 rows with impossible numbers were kept in, not deleted: The raw data has a built in check for two things that shouldn't be possible: conversions being higher than clicks, and clicks being higher than impressions. 51 rows fail the first check and 1 row fails the second, out of 1,000 total. Rather than deleting these rows, I kept them in every calculation. The likely explanation is multi-touch attribution or a delay in tracking pixels firing, not bad spend or revenue data, and the spend and revenue figures for these rows are unaffected either way. The one thing this does affect is CTR and conversion rate for the 8 campaign types that have flagged rows. Those two metrics should be read as directionally correct rather than exact, until the tracking source behind them gets investigated.

Why SQL and Excel might list campaigns in a different order: In the Best 5 and Worst 5 breakdowns, several campaigns tie on ROI (for example, multiple campaigns tie at 150% in the Best 5 list). When there's a tie, SQL and Excel don't always break it the same way. SQL ends up picking the record with the lowest Campaign ID first, so if you compare the two side by side and see a different campaign at position 3 or 4, that's why. For the Best 5, that's Influencer Marketing (ID 433) and TV Commercial (ID 11). For the Worst 5, that's Content Marketing (ID 799) and Search Engine Ads (ID 244).
