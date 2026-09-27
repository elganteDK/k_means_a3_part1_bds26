# City Profiles for International Digital Nomads

**Target audience:** International digital nomads that want to choose a city to live and work from, balancing estimated monthly costs with internet connectivity.

## Decision question

How can global cities be grouped by the cost of a nomad lifestyle and recorded internet speed, and do K-means and Archetypal Analysis (AA) tell a similar story?

## Data and approach

The analysis uses `cost_nomad` and `internet_speed`, two variables directly connected to the audience's budget and remote-work needs. Because they use different units and scales, both features are standardized before distance-based clustering. The notebook excludes records where internet speed is zero, which is treated as unknown, and fits both methods on the remaining 673 cities. Fourteen selected cities are highlighted on the full-dataset visualization.

## Method choice and visualization

For a digital nomad comparing destinations, **K-means is the primary method** because it assigns every city to one distinct group that can be summarized by an average cost and internet speed. This makes it convenient for organizing a shortlist. **AA is also applied** because its archetypes provide contrasting extreme profiles, such as unusually fast internet or unusually high/low cost, that help explain the range of trade-offs. It complements K-means rather than serving as another city-ranking method.

Both methods are fitted to the same two standardized features and all 673 valid cities. The notebook compares candidate values of `k` using K-means inertia and silhouette scores, then fits both methods with `k=3` for the ARI comparison. The full-dataset visualization plots cost against internet speed in original units, highlights 14 selected cities, and overlays K-means centroids and AA archetypes. It helps to see where those examples sit relative to the overall city distribution and the model profiles. In the current plot, however, all non-highlighted cities share the same gray style; individual K-means and AA city assignments are color-coded, so the figure shows the model representatives and context.

## Findings and interpretation

The diagnostics do not identify one uniquely correct number of groups. Among the tested values, K-means has its highest silhouette score at `k=4` (0.491), only slightly above its score at `k=3` (0.485). AA has its highest score at `k=2` (0.558), with a relatively strong score at `k=3` (0.531). We use `k=3` as a practical shared value to compare the methods, not as proof that three is the objectively correct number of city types. A silhouette score describes how separated groups are on the selected features; it does not measure how good a city is to live in.

At `k=3`, the K-means centers suggest three cost-connectivity trade-offs:

- **Lower estimated cost, slower connection:** **Denpasar** about $1,554 per month and 8 Mbps on average. This profile may appeal to a nomad with a tight budget, but the recorded speed could be limiting for bandwidth-heavy work.
- **Higher estimated cost, moderate connection:** **Panama City** about $3,556 per month and 16 Mbps. A higher budget does not necessarily correspond to the fastest connection in this dataset, so cost alone is not a proxy for remote-work quality.
- **Mid-to-high estimated cost, faster connection:** **Ogden** about $2,849 per month and 55 Mbps. For someone who prioritizes connectivity, this profile has the strongest average recorded speed, at a lower average cost than the second profile.

These figures are K-means cluster centers converted back to the original units. They summarize groups of cities; they are not the costs or speeds of a particular city, and a group average can hide substantial differences between its members. A nomad should use the city-level points and current local information to identify candidates within a profile.

At the same `k`, AA produces three different extremes: approximately $10,117 per month with 2 Mbps, $2,783 with 197 Mbps, and $608 with about 2 Mbps. These extremes make the range of observed trade-offs vivid, but they are archetypal profiles rather than recommended destinations. 

The ARI is **0.056**, which means the two methods assign cities to very different groups at `k=3`. It does not mean K-means is more accurate or better for relocation. Rather, the method choice changes the resulting segmentation: K-means summarizes broad groups around averages, while AA emphasizes extreme profiles. The differing silhouette peaks reinforce that there is no single method-independent answer to how many useful city types exist.

## What the city types mean to the audience

Use the K-means groups as a first-pass way to organize a shortlist around budget and connection needs. Use AA's extremes to consider edge cases, such as very fast but costly connectivity or low cost with slow connectivity. Then compare the actual cities in the relevant group against personal requirements. Someone who frequently makes video calls may reject the lowest-speed profile even if it is inexpensive; someone with mostly offline work may accept that trade-off. The analysis helps frame that choice but does not select a winning city.

## Decision based on the comparison

Keep K-means as the primary segmentation for a simple shortlist, and retain AA as a complementary view of extreme trade-offs. The practical conclusion is that both views can inform exploration, but the segmentation depends on the method and chosen `k`.

This project is a first-pass comparison, not a full relocation analysis. It uses only `cost_nomad` and `internet_speed` for 673 cities with nonzero recorded internet speed. It omits safety, housing detail, visas, taxes, healthcare, time-zone fit, internet reliability, and personal preferences. The cost and speed values are dataset estimates, not guarantees about current conditions. A real relocation decision needs those additional factors and up-to-date checks for the specific cities being considered.

Note: In particular, very high or low values may be driven by unusual records and should be checked against source data before being treated as typical.
