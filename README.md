# Geo localisation & Web Science

![Geolocation Data (地理定位数据) ⭐⭐⭐⭐](./img/419000991-733b9b45-fffb-4368-bf78-30530165fcb1.png)

> **Geolocalisation** refers to the process of identifying or estimating the real-world geographic location of an object, such as a mobile device, internet-connected computer, or website visitor. 

> From a **geographical perspective**, geolocalisation involves determining physical coordinates (latitude and longitude) or place names (countries, cities, addresses) of entities in the real world. It relies on various technologies including GPS (Global Positioning System), cell tower triangulation, IP address mapping, and Wi-Fi positioning systems.

> From a **Web Science perspective**, geolocalisation is a fundamental component of location-based services, enabling personalized user experiences based on spatial context. It encompasses the collection, processing, and application of location data in web applications, social media platforms, and online services. This includes techniques for location-aware content delivery, spatial data visualization, privacy considerations around location tracking, and the analysis of geographic patterns in user behavior across the web.

## Table of Contents
- [Geo localisation \& Web Science](#geo-localisation--web-science)
  - [Table of Contents](#table-of-contents)
  - [Introduction to Geolocalisation](#introduction-to-geolocalisation)
    - [Definition and Importance](#definition-and-importance)
    - [Benefits of Geolocalisation](#benefits-of-geolocalisation)
    - [Geo-coordinate Definitions](#geo-coordinate-definitions)
  - [Types of Geolocalisation](#types-of-geolocalisation)
    - [Coarse-grained Geolocalisation](#coarse-grained-geolocalisation)
    - [Fine-grained Geolocalisation](#fine-grained-geolocalisation)
    - [Comparison of Approaches](#comparison-of-approaches)
  - [Geolocalisation in Social Media](#geolocalisation-in-social-media)
    - [Twitter Geolocation Data](#twitter-geolocation-data)
    - [Place Objects and Coordinates](#place-objects-and-coordinates)
    - [Privacy Considerations](#privacy-considerations)
  - [Geolocalisation Techniques](#geolocalisation-techniques)
    - [Information Retrieval Approach](#information-retrieval-approach)
    - [Grid-based Methods](#grid-based-methods)
    - [Majority Voting and Weighted Algorithms](#majority-voting-and-weighted-algorithms)
  - [Credibility in Geolocalisation](#credibility-in-geolocalisation)
    - [Defining Credibility](#defining-credibility)
    - [Computing Credibility Scores](#computing-credibility-scores)
    - [Weighted Approaches Using Credibility](#weighted-approaches-using-credibility)
  - [Evaluation Methodology](#evaluation-methodology)
    - [Ground Truth and Gold Standards](#ground-truth-and-gold-standards)
  - [Real-world Applications](#real-world-applications)
    - [Emergency Response](#emergency-response)
    - [Traffic Incident Detection](#traffic-incident-detection)
- [Social Media Data – Twitter/X](#social-media-data--twitterx)
  - [Importance of X platform](#importance-of-x-platform)
  - [Demographics](#demographics)
  - [Income distribution - above average?](#income-distribution---above-average)
  - [Political Beliefs](#political-beliefs)
  - [Bias in data](#bias-in-data)
  - [It's not about Twitter but about data](#its-not-about-twitter-but-about-data)
  - [Data Structure](#data-structure)
  - [Tweet Structure and Metadata](#tweet-structure-and-metadata)
    - [Basic Tweet Structure](#basic-tweet-structure)
      - [Example of Basic Tweet JSON Structure](#example-of-basic-tweet-json-structure)
    - [Communication Elements](#communication-elements)
    - [Metadata for Geolocation](#metadata-for-geolocation)
      - [Example: Tweet with Only Place Object (No Precise Coordinates)](#example-tweet-with-only-place-object-no-precise-coordinates)
      - [Example: Tweet with Location Mentioned in Text (No Explicit Geolocation)](#example-tweet-with-location-mentioned-in-text-no-explicit-geolocation)
    - [Data Structure for Analysis](#data-structure-for-analysis)
      - [Example: Structured Data for Geolocation Analysis](#example-structured-data-for-geolocation-analysis)
  - [Place Object](#place-object)
    - [Detailed Place Object Example](#detailed-place-object-example)
    - [Example: Tweet with Credibility Indicators for Geolocation](#example-tweet-with-credibility-indicators-for-geolocation)
  - [Tutorial Questions and Answers](#tutorial-questions-and-answers)
    - [Why do you think location information is important?](#why-do-you-think-location-information-is-important)
    - [What are the benefits of location information?](#what-are-the-benefits-of-location-information)
    - [How does Twitter encode location information \& their advantages and limitations?](#how-does-twitter-encode-location-information--their-advantages-and-limitations)
- [Content Processing](#content-processing)
  - [Processing and Cleansing Social Media Data](#processing-and-cleansing-social-media-data)
    - [Text Preprocessing Pipeline](#text-preprocessing-pipeline)
  - [Text Vector Representation](#text-vector-representation)
    - [Vector Space Model for Documents and Queries](#vector-space-model-for-documents-and-queries)
    - [Binary Representation Approach](#binary-representation-approach)
  - [Similar Documents](#similar-documents)
  - [Cosine Similarity Measure](#cosine-similarity-measure)
  - [Length of a Vector](#length-of-a-vector)
  - [Unit Vector](#unit-vector)
  - [Similarity Computation](#similarity-computation)
    - [Cosine Similarity](#cosine-similarity)
    - [Similarity vs. Dissimilarity (Distance)](#similarity-vs-dissimilarity-distance)
    - [Working with Normalized Vectors:](#working-with-normalized-vectors)
  - [Text Processing Pipeline](#text-processing-pipeline)
  - [Term Weighting](#term-weighting)
    - [In documents, such as web pages:](#in-documents-such-as-web-pages)
    - [However, in tweets and short social media posts:](#however-in-tweets-and-short-social-media-posts)
  - [Finding similar tweets](#finding-similar-tweets)
    - [What is a cluster?](#what-is-a-cluster)
    - [Clustering in Text Analysis](#clustering-in-text-analysis)
    - [Applications of Tweet Clustering](#applications-of-tweet-clustering)
  - [Single-pass clustering](#single-pass-clustering)
  - [Cluster centroid](#cluster-centroid)
  - [Stream of tweets](#stream-of-tweets)
  - [Single Pass Clustering Steps](#single-pass-clustering-steps)
  - [How to group tweets](#how-to-group-tweets)
  - [Comments](#comments)
  - [Comments \& Observations](#comments--observations)
  - [Moving average](#moving-average)

## Introduction to Geolocalisation

### Definition and Importance

"Geo-localisation is the process of determining real-world geographic location of objects or people, important for personalized services and spatial analysis, implemented through various methods (GPS, IP, cell towers) with accuracy limitations, requiring careful evaluation methodology and awareness of potential biases."

### Benefits of Geolocalisation

Identifying the location of events, people, or incidents provides numerous critical benefits for society and services:

- **Quick responses from civil or security services**: Precise location information enables emergency services to respond rapidly to incidents. For example, when a fire is reported with accurate geolocation data, fire departments can dispatch the nearest units, potentially reducing response time by 3-5 minutes, which can be life-saving in critical situations.

- **Marking alerts to citizens**: Geolocation enables targeted emergency notifications to people in specific areas. During natural disasters like floods or wildfires, authorities can send evacuation orders or safety instructions only to those in affected zones, preventing unnecessary panic while ensuring those at risk receive timely information.

- **Enhanced service delivery**: Location data allows service providers to tailor their offerings based on geographical context. For instance, food delivery platforms can show only restaurants that deliver to a customer's specific location, improving user experience by filtering out irrelevant options.

- **Resource optimization**: Emergency management agencies can allocate resources more efficiently when they have precise location data. During large-scale incidents, they can visualize the geographic distribution of events and deploy personnel strategically.

The primary aim is to identify locations as precisely as possible:
- **Specific street vs. general area**: Identifying "Byres Road" provides much more actionable information than simply stating "west-end" of a city. This level of precision can be the difference between finding a victim quickly or conducting a prolonged search across a larger area.

- **Fine-grained nature**: The more precise the location information, the more effective the response can be. For example, knowing which floor and room number in a building can save precious minutes during medical emergencies.

Alternative approaches involve using fixed sensor networks:
- **Traffic cameras**: Strategically placed CCTV systems can monitor traffic conditions and detect incidents, but they are limited to their fixed viewpoints and cannot cover all areas.

- **Traffic flow measurements**: Sensors embedded in roadways can detect unusual patterns in vehicle movement that might indicate accidents, but they require extensive infrastructure investment and maintenance.

- **Environmental sensors**: These can detect conditions like flooding or air quality issues, providing location-specific data without relying on human reports.

While these sensor-based approaches provide reliable data, they lack the flexibility and coverage of crowdsourced geolocation information from mobile devices and social media, which can provide real-time updates from virtually anywhere people are present.

### Geo-coordinate Definitions

Geo-coordinates are numerical values that represent specific locations on the Earth's surface. They typically consist of:

- **Latitude**: A measure of the north-south position, expressed in degrees ranging from -90° (South Pole) to 90° (North Pole), with 0° representing the Equator.
- **Longitude**: A measure of the east-west position, expressed in degrees ranging from -180° to 180°, with 0° representing the Prime Meridian (passing through Greenwich, London).

These coordinates can be expressed in several formats:
- Decimal degrees (DD): e.g., 55.8724° N, 4.2900° W
- Degrees, minutes, seconds (DMS): e.g., 55° 52' 21" N, 4° 17' 24" W
- Degrees and decimal minutes (DMM): e.g., 55° 52.35' N, 4° 17.40' W

Additional parameters sometimes included with geo-coordinates:
- **Altitude**: Height above or below sea level
- **Accuracy**: Margin of error in the coordinate measurement
- **Timestamp**: When the coordinates were recorded

Geo-coordinates serve as the foundation for mapping, navigation systems, GIS (Geographic Information Systems), location-based services, and spatial analysis in various applications.

## Types of Geolocalisation

### Coarse-grained Geolocalisation

Coarse-grained geolocalisation refers to the process of determining location at a broader level, such as:
- Country level
- State/region level
- City level

This approach provides less precise location information but may be sufficient for many applications and has fewer privacy implications.

### Fine-grained Geolocalisation

Fine-grained geolocalisation aims to determine location at a much more detailed level:
- Neighborhood level
- Street level
- Specific coordinates (latitude/longitude)

This approach provides highly precise location information, enabling more targeted services but raising greater privacy concerns.

### Comparison of Approaches

| Aspect | Coarse-grained Geolocalisation | Fine-grained Geolocalisation |
|--------|--------------------------------|------------------------------|
| **Precision** | Lower precision (region/city level) | Higher precision (street/neighborhood level) |
| **Use Cases** | Regional trends, country-specific services | Emergency response, hyperlocal services |
| **Data Requirements** | Less data needed | More detailed data required |
| **Privacy Concerns** | Lower privacy impact | Higher privacy impact |
| **Implementation Complexity** | Simpler to implement | More complex algorithms needed |
| **Example** | "Northeast England", "Newcastle" | "Elephant & Castle station, London" |

The choice between coarse-grained and fine-grained approaches depends on:
- The specific application requirements
- Available data sources
- Privacy considerations
- Required accuracy level
- Computational resources

For applications like emergency response or traffic incident detection, fine-grained geolocalisation is essential to provide precise location information. For broader applications like regional trend analysis or country-specific content delivery, coarse-grained approaches may be sufficient.

## Geolocalisation in Social Media

### Twitter Geolocation Data

Twitter provides several types of location data in tweets:
- User profile location (self-reported)
- Geo-tagged coordinates (when geo_enabled=true)
- Place objects (broader location information)

### Place Objects and Coordinates

Twitter provides different types of location data in tweets:

1. **Coordinates**: When a user enables precise location sharing (geo_enabled=true), tweets can include exact latitude and longitude coordinates:
   ```json
   {
     "user": {
       "id": 12345678,
       "screen_name": "example_user",
       "geo_enabled": true
     },
     "coordinates": {
       "type": "Point",
       "coordinates": [-0.27955033, 51.55598294]
     },
     "text": "Just witnessed a traffic accident on the highway #traffic #accident"
   }
   ```
   These coordinates provide the most precise location information and are ideal for fine-grained geolocalisation. The coordinates array follows the GeoJSON format where the first element is longitude and the second is latitude. This level of precision allows for exact positioning on a map, which is crucial for emergency response applications.

2. **Place Objects**: Twitter also provides place objects, which represent a larger geographic area:
   ```json
   {
     "user": {
       "id": 87654321,
       "screen_name": "another_user"
     },
     "place": {
       "id": "e4a0dfa469c30504",
       "place_type": "city",
       "place_name": "Wexford",
       "full_name": "Wexford, Ireland",
       "country": "Ireland",
       "country_code": "IE",
       "bounding_box": {
         "type": "Polygon",
         "coordinates": [[
           [-7.017507, 52.122381],
           [-7.017507, 52.797086],
           [-6.141269, 52.797086],
           [-6.141269, 52.122381]
         ]]
       }
     },
     "text": "Beautiful day in Wexford today! #sunshine"
   }
   ```
   The place object contains a bounding_box field with coordinates that define the boundaries of the place as a polygon. This provides less precise location information than exact coordinates but still offers valuable geographic context. The bounding box coordinates represent the southwest, northwest, northeast, and southeast corners of the area, respectively.

3. **User Profile Location**: Users can also specify their location in their profile, but this is:
   - Self-reported and can be found in the user object:
   ```json
   {
     "user": {
       "id": 98765432,
       "screen_name": "profile_location_user",
       "location": "London, UK",
       "geo_enabled": false
     },
     "text": "Just my thoughts on the current situation #opinion"
   }
   ```
   This location field is:
   - Not verified by Twitter
   - Often imprecise (e.g., "London" could refer to London, UK or London, Ontario)
   - Sometimes fictional (e.g., "Hogwarts" or "Somewhere in cyberspace")
   - Not directly tied to individual tweets (represents the user's general location, not where they were when tweeting)

When working with Twitter data for geolocalisation, it's important to understand the differences between these location types and their implications for accuracy and reliability. Coordinates provide the highest precision but are the least common, while profile locations are the most common but least reliable. Place objects offer a middle ground, providing verified geographic information at a broader scale.

### Privacy Considerations

Geolocalisation raises significant privacy concerns, particularly in social media contexts:

1. **User Consent and Awareness**:
   - Many users may not fully understand the implications of sharing their location
   - The granularity of shared location data may not be clear to users
   - Users might inadvertently reveal sensitive locations (home, workplace)

2. **Personal Safety Risks**:
   - Precise location data can expose users to physical risks
   - Stalking and harassment concerns
   - Potential for burglary when users share that they're away from home

3. **Regulatory Considerations**:
   - GDPR and other privacy regulations place restrictions on location data collection
   - Requirements for explicit consent and data minimization
   - Right to be forgotten applies to historical location data

4. **Ethical Research Practices**:
   - Researchers must consider privacy implications when using geolocation data
   - Anonymization techniques should be applied
   - Aggregation of data to protect individual privacy

5. **Technical Safeguards**:
   - Geofencing to limit precision of shared location
   - Time-limited location sharing
   - User controls for location history

The tension between utility and privacy is particularly acute in geolocalisation. While precise location data enables valuable services and research, it also creates significant privacy risks that must be carefully managed through technical, legal, and ethical frameworks.

## Geolocalisation Techniques

### Information Retrieval Approach

The Information Retrieval (IR) approach to geolocalisation treats location prediction as a retrieval problem:

1. **Basic Concept**:
   - Treat each location as a "document"
   - Treat the content of a tweet (or other text) as a "query"
   - Rank locations based on their relevance to the query
   - Assign the highest-ranked location to the query

2. **Implementation Steps**:
   - Collect geo-tagged tweets as training data
   - Create location "documents" by aggregating all tweets from each location
   - Build an inverted index mapping terms to locations
   - For a new tweet without location, query the index to find the most relevant location
   - Rank locations using standard IR ranking functions (e.g., TF-IDF, BM25)

3. **Example Process**:
   - For a tweet mentioning "Elephant & Castle station fire"
   - The IR system would match these terms against the location index
   - Locations where these terms frequently appear (e.g., London) would rank highly
   - The highest-ranked location would be assigned to the tweet

4. **Advantages**:
   - Leverages well-established IR techniques
   - Can handle textual content effectively
   - Scales well to large datasets
   - Can incorporate various ranking functions

5. **Limitations**:
   - Relies on the assumption that language is location-specific
   - May struggle with ambiguous location references
   - Performance depends on the quality and quantity of training data

The IR approach is particularly effective for fine-grained geolocalisation when there is sufficient training data with distinctive vocabulary for different locations.

### Grid-based Methods

Grid-based methods divide geographical space into discrete cells to simplify the geolocalisation process:

1. **Grid Creation**:
   - Divide the geographical area of interest into uniform grid cells
   - Common grid sizes include 1km × 1km for fine-grained analysis
   - Each grid cell is treated as a distinct location unit
   - Example: New York City might be divided into 48 rows × 47 columns = 2,256 grid cells

2. **Data Aggregation**:
   - Aggregate all tweets or text content within each grid cell
   - Create a language model or feature representation for each grid
   - This aggregation helps overcome data sparsity in individual locations

3. **Implementation Process**:
   - Assign each geo-tagged tweet to its corresponding grid cell based on coordinates
   - Combine all text from tweets in the same grid to create a "document" per grid
   - For non-geotagged tweets, predict the most likely grid cell using text analysis

4. **Advantages**:
   - Provides a standardized spatial framework for analysis
   - Simplifies the continuous geographical space into discrete units
   - Enables more efficient computational processing
   - Facilitates visualization and mapping of results

5. **Challenges**:
   - Grid size selection affects precision (smaller grids = higher precision but sparser data)
   - Boundary effects where relevant information crosses grid lines
   - Uneven distribution of data across grid cells
   - Urban areas typically have more data than rural areas

Grid-based methods are particularly useful for fine-grained geolocalisation in urban environments where sufficient data exists across the grid cells. The approach provides a balance between precision and computational efficiency.

### Majority Voting and Weighted Algorithms

Majority voting and weighted algorithms are ensemble approaches used to improve geolocalisation accuracy:

1. **Basic Majority Voting**:
   - Retrieve the top-N most similar geo-tagged tweets to a query tweet
   - Each similar tweet "votes" for its location
   - The location with the most votes is assigned to the query tweet
   - Simple implementation: count the number of votes for each location
   
   For example, if we have a query tweet Q and retrieve 10 similar tweets, where 6 are from London, 3 from Manchester, and 1 from Birmingham, the majority voting would assign London as the predicted location for Q.

2. **Weighted Majority Voting**:
   - Similar to basic majority voting, but each vote is weighted
   - Weights can be based on:
     - Similarity score between the query and retrieved tweet
     - Credibility of the tweet or user
     - Temporal relevance (more recent tweets may get higher weights)
   - The location with the highest weighted sum is assigned
   
   The weighted voting formula can be expressed as:
   ```
   Score(Location_i) = Σ(Similarity(Q, Tj) × I(Tj, Location_i))
   ```
   Where:
   - Q is the query tweet
   - Tj is the jth retrieved tweet
   - I(Tj, Location_i) is an indicator function that equals 1 if tweet Tj is from Location_i and 0 otherwise
   - Similarity(Q, Tj) is the similarity score between the query tweet and retrieved tweet

3. **Implementation Example**:
   ```python
   # Pseudocode for weighted majority voting
   def predict_location(query_tweet, reference_tweets):
       location_scores = {}
       for tweet in reference_tweets:
           similarity = calculate_similarity(query_tweet, tweet)
           location = tweet.location
           if location not in location_scores:
               location_scores[location] = 0
           location_scores[location] += similarity
       
       return max(location_scores, key=location_scores.get)
   ```
   
   This implementation calculates a weighted score for each location based on the similarity between the query tweet and reference tweets from that location. The location with the highest score is predicted.

4. **Advantages**:
   - Reduces the impact of outliers or irrelevant matches
   - Incorporates multiple signals for more robust prediction
   - Can be easily extended with different weighting schemes
   - Provides a confidence measure through vote distribution

5. **Research Reference**:
   - "On fine-grained geolocalisation of tweets and real-time traffic incident detection" by Jorge David Gonzalez Paule, Yeran Sun, Yashar Moshfeghi (https://doi.org/10.1016/j.ipm.2018.03.011)
   - This research demonstrates the effectiveness of weighted voting approaches for fine-grained geolocalisation

Weighted voting algorithms are particularly effective when combined with credibility measures, as they can prioritize more reliable information sources while still considering the diversity of evidence.

## Credibility in Geolocalisation

### Defining Credibility

The credibility of a user is a score that represents the user's posting activity and its relevance to the physical location they are posting from. In the context of geolocalisation, credibility measures how reliable a user's content is for determining geographic location. 

Credibility encompasses several dimensions:

1. **Spatial Credibility**: How consistently a user posts from or about specific locations. Users who regularly post from the same area are likely to have higher spatial credibility for that area.

2. **Content Credibility**: The accuracy and relevance of location-specific information in a user's posts. Users who provide detailed, verifiable information about locations tend to have higher content credibility.

3. **Temporal Credibility**: The recency and frequency of a user's location-related posts. More recent and frequent posts about a location may indicate higher credibility.

4. **Social Credibility**: The user's reputation and influence within the community. Verified accounts or accounts with large followings might be considered more credible sources of location information.

For example, a local news reporter who frequently posts about events in their city with accurate details would have high credibility for geolocalisation in that area. In contrast, a bot account posting generic content with randomly attached locations would have low credibility.

### Computing Credibility Scores

<!-- TODO: Updated based on the lecture slide -->

### Weighted Approaches Using Credibility

Incorporating credibility scores into geolocalisation algorithms can significantly improve accuracy:

1. **Credibility-Weighted Voting**:
   - In a voting-based geolocalisation system, each vote is weighted by the credibility score
   - Higher credibility tweets have more influence on the final location prediction
   - Formula: `Score(Location) = Sum(Credibility(Tweet_i) * Vote(Tweet_i, Location))`

   For example, if we have three tweets suggesting different locations:
   - Tweet 1: Location A, Credibility = 0.8
   - Tweet 2: Location A, Credibility = 0.3
   - Tweet 3: Location B, Credibility = 0.6

   The scores would be:
   - Location A: 0.8 + 0.3 = 1.1
   - Location B: 0.6

   Location A would be selected as it has the highest credibility-weighted score.

2. **Credibility Factors**:
   - User activity patterns (frequency and consistency of posting)
   - Relevance of content to the location
   - User verification status
   - Historical accuracy of location information
   - Account age and reputation

   Each of these factors can be quantified and combined into a comprehensive credibility score. For example:

   $$
   \text{Credibility}(\text{User}) = w_1 \times \text{ActivityScore} + w_2 \times \text{RelevanceScore} + w_3 \times \text{VerificationScore} + w_4 \times \text{HistoricalAccuracyScore} + w_5 \times \text{AccountAgeScore}
   $$

   Where w₁, w₂, w₃, w₄, and w₅ are weights that determine the relative importance of each factor.

3. **Implementation Considerations**:
   - Credibility scores may be normalized to ensure fair weighting:
     ```
     NormalizedCredibility(User) = (Credibility(User) - MinCredibility) / (MaxCredibility - MinCredibility)
     ```
   - Different aspects of credibility may be weighted differently based on their importance
   - Credibility can be computed dynamically or pre-computed for efficiency

   A practical implementation might look like:
   ```python
   def predict_location_with_credibility(query_tweet, reference_tweets, user_credibility):
       location_scores = {}
       for tweet in reference_tweets:
           similarity = calculate_similarity(query_tweet, tweet)
           credibility = user_credibility.get(tweet.user_id, 0.5)  # Default to 0.5 if unknown
           location = tweet.location
           
           if location not in location_scores:
               location_scores[location] = 0
           
           # Weight the vote by both similarity and credibility
           location_scores[location] += similarity * credibility
       
       return max(location_scores, key=location_scores.get)
   ```

4. **Advantages**:
   - Reduces the impact of spam or unreliable sources
   - Improves precision in fine-grained geolocalisation
   - Provides a mechanism to handle conflicting location evidence
   - Can adapt to different contexts and requirements

5. **Challenges**:
   - Defining appropriate credibility metrics
   - Balancing different credibility factors
   - Avoiding bias in credibility assessment
   - Computational overhead of calculating credibility scores

Credibility-weighted approaches represent an advanced technique in geolocalisation that goes beyond simple text matching or majority voting. By incorporating the reliability of information sources, these methods can achieve higher accuracy, especially in noisy or ambiguous scenarios.

## Evaluation Methodology

### Ground Truth and Gold Standards

For evaluating geolocalisation techniques, establishing reliable ground truth data is essential. This process involves:

1. **Using Geo-enabled Tweets as Ground Truth**:
   - Tweets with explicit geo-coordinates provide the most reliable ground truth
   - These coordinates are typically obtained from GPS-enabled devices
   - Example of geo-enabled tweet data:
   ```json
   {
     "id": "1234567890",
     "text": "Enjoying the view from Glasgow University tower!",
     "coordinates": {
       "type": "Point",
       "coordinates": [-4.2885, 55.8724]
     },
     "created_at": "2023-04-15T14:32:18Z"
   }
   ```
   - The coordinates field contains the exact longitude and latitude, which serves as the ground truth location

2. **Training and Testing Methodology**:
   - Split geo-enabled tweets into training and testing sets (typically 80/20 or 70/30 split)
   - Use the training set to build geolocalisation models
   - For testing, remove the location information and attempt to predict it
   - Compare predicted locations with the actual coordinates to measure accuracy
   - Cross-validation techniques (e.g., k-fold) can be used to ensure robust evaluation

3. **Creating Gold Standard Datasets**:
   - Manually verify a subset of geo-tagged tweets for higher confidence
   - Ensure diverse geographic coverage to avoid regional biases
   - Include tweets from different time periods to account for temporal variations
   - Balance urban and rural locations to test performance across population densities
   - Document the creation process and potential limitations for transparency

4. **Real-life Application Testing**:
   - After initial evaluation with ground truth data, apply techniques to real-world scenarios
   - Collect feedback from end-users or domain experts
   - Conduct case studies for specific applications (e.g., emergency response)
   - Measure performance metrics in production environments
   - Continuously update models based on new data and feedback

5. **Handling Ambiguous Cases**:
   - Some locations may have multiple valid interpretations
   - Create guidelines for resolving ambiguities consistently
   - Consider using multiple annotators and measuring inter-annotator agreement
   - Document cases where ground truth itself may be uncertain

By establishing reliable ground truth data and following rigorous evaluation methodologies, researchers can accurately assess the performance of different geolocalisation techniques and make meaningful comparisons between approaches.

## Real-world Applications

### Emergency Response

Geolocalisation plays a critical role in emergency response scenarios:

1. **Disaster Management**:
   - Identifying affected areas through social media posts
   - Monitoring the spread of disasters (floods, fires, earthquakes) in real-time
   - Example: During hurricanes, geolocated tweets can help identify areas with flooding or damage

2. **Resource Allocation**:
   - Prioritizing areas with the most urgent needs
   - Directing emergency services to specific locations
   - Optimizing evacuation routes based on real-time information

3. **Public Safety Alerts**:
   - Sending targeted warnings to people in specific areas
   - Providing location-specific instructions during emergencies
   - Reaching people who might not have access to traditional media

4. **Implementation Challenges**:
   - Need for real-time processing with minimal latency
   - Handling misinformation during crisis situations
   - Ensuring system reliability when infrastructure may be compromised

5. **Case Study Example**:
   - During the London Elephant & Castle fire (mentioned in the lecture), fine-grained geolocalisation of tweets helped emergency services understand the situation and respond appropriately

Fine-grained geolocalisation is particularly valuable in emergency scenarios where precise location information can save lives and optimize resource allocation.

### Traffic Incident Detection

Geolocalisation enables advanced traffic monitoring and incident detection:

1. **Real-time Traffic Monitoring**:
   - Detecting traffic incidents through geolocated social media posts
   - Complementing traditional sensors with crowdsourced information
   - Providing earlier detection than official reporting systems

2. **Incident Verification**:
   - Cross-referencing multiple geolocated reports
   - Using credibility scores to filter reliable information
   - Combining social media data with official traffic data

3. **Traffic Management**:
   - Rerouting traffic based on incident locations
   - Estimating incident duration and impact
   - Providing location-specific alternative route suggestions

4. **Research Applications**:
   - The paper "On fine-grained geolocalisation of tweets and real-time traffic incident detection" demonstrates how tweet geolocalisation can be used for traffic incident detection
   - Such systems can detect incidents faster than traditional methods

5. **Implementation Example**:
   - Monitor tweets containing traffic-related terms
   - Apply fine-grained geolocalisation to determine precise incident location
   - Verify through multiple sources and credibility assessment
   - Integrate with traffic management systems

This application demonstrates how social media geolocalisation can complement traditional sensor networks to improve urban mobility and safety.


![](./img/Twitter_X%20Data%20(Twitter_X%20数据)%20⭐⭐⭐.png)

# Social Media Data – Twitter/X

## Importance of X platform

- Vital communications platform in times of disasters
  - Hurricanes, earthquakes, political upheavals, travel disruptions
  - Enables real-time information sharing when traditional media may be unavailable
  - Facilitates coordination between affected individuals and emergency services
- Hence, scientists (social science), business leaders, security experts gather:
  - Twitter data to understand human behavior and dynamics
  - For example, role of micro-influencers: detection of informative tweets in crisis events
  - Analysis of information spread patterns during emergencies helps improve disaster response

## Demographics

- Men use X more than women, accounting for almost 68% of the platform's user base
  - This gender imbalance may affect the representativeness of data collected from the platform
- More than 80% of Twitter's global population is under 50 years old
  - Indicates a skew toward younger generations, potentially underrepresenting older perspectives
- More teenagers are on Twitter in the U.S. than on:
  - WhatsApp, Pinterest, LinkedIn, and Reddit
  - Shows Twitter's significant penetration among youth demographics
- Twitter ranks only slightly behind Instagram when it comes to 65+ users in the U.S. (7% vs. 8%)
  - Despite being youth-oriented, still maintains some presence among older populations

> Similarly ranked sites include Snapchat and TikTok for younger demographics, while Facebook has higher penetration among older users

## Income distribution - above average?

- 41% of Twitter users surveyed earn a household income about $75,000 (vs. 32% overall)
- Only 23% of people on Twitter earn less than $30,000 annually (vs. 30% overall)
- Education level of Twitter Users tends to be higher than average, with more college-educated users compared to the general population

> What does this mean?
> 
> This demographic profile indicates that Twitter users tend to be wealthier and more educated than the general population. This creates potential biases in geolocation data and analysis:
> 
> 1. Socioeconomic bias: Lower-income communities may be underrepresented in Twitter data, leading to "data deserts" in certain geographic areas
> 2. Educational bias: Higher education levels may influence how users describe locations and events
> 3. Geographic bias: Urban areas with better internet access may be overrepresented compared to rural regions
> 4. Age and gender biases: The perspectives of women, older adults, and certain minority groups may be underrepresented
> 
> These biases must be considered when using Twitter data for geolocation analysis, especially in emergency response scenarios where reaching all affected populations is critical.

## Political Beliefs

Twitter users in the United States tend to have a distinct political profile compared to the general population:

- 36% of Twitter users identify as Democrats, while only 21% identify as Republicans
- This 15-point gap is significantly larger than the 7-point difference in the general U.S. adult population
- Liberal and progressive viewpoints are more prevalent in Twitter discussions
- Users who post political content are more likely to be politically active offline as well
- Political polarization on Twitter often exceeds that observed in face-to-face interactions

> These political demographics have important implications for geolocation analysis:
> 
> 1. Political events may receive disproportionate attention based on alignment with the platform's dominant political leaning
> 2. Geographic areas with higher concentrations of conservative populations might be underrepresented in Twitter data
> 3. Interpretation of events may skew toward progressive perspectives
> 4. Researchers must account for this political bias when analyzing geolocation data related to politically sensitive topics or regions

## Bias in data

When analyzing social media data, particularly from Twitter/X, we must consider inherent biases:

- Social media usage varies significantly across different population segments
  - Twitter represents only a subset of the general population (as shown in demographics above)
  - Not everyone has equal access to or interest in social media platforms

- While Twitter has widespread adoption, it functions differently than traditional data sources:
  - A physical sensor (like a traffic camera or weather station) makes objective measurements
  - Twitter acts as a "social sensor" where humans generate the data points
    - For example, during the 2011 Japan earthquake, Twitter users reported the event 2-3 minutes before official seismic detection systems alerted authorities
    - During Hurricane Sandy (2012), geotagged tweets helped emergency services identify flooded areas faster than traditional reporting methods

- Twitter data often contains valuable information collected implicitly:
  - Users typically share information for personal reasons, not for data collection
  - This creates both an opportunity (authentic, real-time data) and challenge (noise and bias)
  - If we can effectively filter out irrelevant content and misinformation, tweets become valuable social sensors

- Demographics significantly impact data interpretation:
  - Why? Because the Twitter population doesn't mirror the general population
  - As shown above, Twitter users tend to be younger, more affluent, more educated, and more politically liberal
  - Geographic distribution is uneven, with urban areas overrepresented compared to rural regions
  
- When using Twitter for geolocation analysis, we must:
  - Acknowledge these biases in our methodology
  - Avoid making sweeping generalizations about entire populations
  - Supplement Twitter data with other sources when possible
  - Be especially cautious when analyzing underrepresented communities
  - Document limitations and potential biases in research findings

![](./img/2025-03-11-20-21-24.png)

## It's not about Twitter but about data

This course extends beyond Twitter/X to focus on the broader challenge of extracting meaningful insights from large-scale unstructured data sources. Social media platforms provide excellent case studies for several reasons:

- **Unstructured and noisy data**: Social media content lacks formal organization and contains significant noise (irrelevant information, spam, etc.), presenting real-world data processing challenges.
- **Massive volume**: These platforms generate billions of interactions daily, requiring efficient processing techniques and methodologies.
- **Rich analytical potential**: Despite the challenges, these datasets contain valuable patterns about human behavior, events, trends, and geographic phenomena when properly analyzed.

We focus primarily on Twitter and Reddit data because:
- They offer diverse usage patterns (short-form vs. long-form content, different community structures)
- Extensive historical datasets are available for research purposes
- They provide accessible APIs for data collection and analysis
- They contain location-based information that enables geospatial analysis

## Data Structure

![](./img/2025-03-11-20-23-25.png)

![](./img/2025-03-11-20-23-37.png)

## Tweet Structure and Metadata

A tweet contains rich structured and unstructured data that can be leveraged for geolocation analysis:

### Basic Tweet Structure
- **Limited to 280 characters** (formerly 140 characters)
  - It was 140 until Twitter expanded the limit in 2017
  - Limits to certain circumstances still apply
- **Each tweet has a unique ID**
  - On Twitter, a message, a unique ID, a timestamp of when it was posted, and information about the user
  - This metadata is crucial for temporal analysis
- **Each user has a Twitter name, an ID, a profile description, and often a location field**
- **Tweets can be retweeted, replied to, liked, and bookmarked**

#### Example of Basic Tweet JSON Structure

```json
{
  "created_at": "Wed Oct 10 20:19:24 +0000 2023",
  "id": 1580623451872395264,
  "id_str": "1580623451872395264",
  "text": "Beautiful sunset over Glasgow Green today! #Glasgow #Sunset",
  "truncated": false,
  "source": "<a href=\"http://twitter.com/download/iphone\" rel=\"nofollow\">Twitter for iPhone</a>",
  "user": {
    "id": 87654321,
    "id_str": "87654321",
    "name": "Jane Smith",
    "screen_name": "janesmith",
    "location": "Glasgow, Scotland",
    "description": "Urban photographer and coffee enthusiast",
    "verified": false,
    "followers_count": 1243,
    "friends_count": 567,
    "time_zone": "London"
  },
  "coordinates": {
    "type": "Point",
    "coordinates": [-4.2333, 55.8500]
  },
  "place": {
    "id": "0e8b2a4c5f6d7e8f",
    "url": "https://api.twitter.com/1.1/geo/id/0e8b2a4c5f6d7e8f.json",
    "place_type": "city",
    "name": "Glasgow",
    "full_name": "Glasgow, Scotland",
    "country_code": "GB",
    "country": "United Kingdom",
    "bounding_box": {
      "type": "Polygon",
      "coordinates": [[
        [-4.3939, 55.7943],
        [-4.3939, 55.9072],
        [-4.0892, 55.9072],
        [-4.0892, 55.7943]
      ]]
    }
  },
  "entities": {
    "hashtags": [
      {"text": "Glasgow", "indices": [35, 43]},
      {"text": "Sunset", "indices": [44, 51]}
    ]
  },
  "geo_enabled": true
}
```

**Key Fields Explained:**
- `created_at`: Timestamp when the tweet was created, crucial for temporal analysis
- `text`: The actual content of the tweet, which may contain location references
- `user.location`: Self-reported location in the user's profile ("Glasgow, Scotland")
- `user.time_zone`: User's selected time zone, which can provide coarse location information
- `coordinates`: Precise geolocation data with longitude (-4.2333) and latitude (55.8500)
- `place`: A structured object representing the location (Glasgow, Scotland)
- `entities.hashtags`: May contain location-relevant hashtags like "#Glasgow"

### Communication Elements
- What can we communicate?
  - Text, URLs, hashtags, mentions, pictures, videos, GIFs
  - If a tag is related to another tweet, it is, however, reply or retweet, and this information will be embedded into the tweet

### Metadata for Geolocation
- **Explicit location data**:
  - Precise coordinates (if location services enabled)
  - Place tags (city, neighborhood, venue)
  - User-defined location in profile (often unreliable)
- **Implicit location indicators**:
  - Time zones
  - Language settings
  - Local references in content
  - Mentioned locations in text

#### Example: Tweet with Only Place Object (No Precise Coordinates)

```json
{
  "created_at": "Thu Oct 12 13:45:10 +0000 2023",
  "id": 1581298765432198765,
  "id_str": "1581298765432198765",
  "text": "Traffic is terrible on the M8 this morning! #TrafficAlert #Glasgow",
  "user": {
    "id": 12345678,
    "id_str": "12345678",
    "name": "John Doe",
    "screen_name": "johndoe",
    "location": "Scotland, UK",
    "description": "Daily commuter, coffee lover",
    "verified": false
  },
  "coordinates": null,
  "place": {
    "id": "0e8b2a4c5f6d7e8f",
    "place_type": "city",
    "name": "Glasgow",
    "full_name": "Glasgow, Scotland",
    "country_code": "GB",
    "country": "United Kingdom",
    "bounding_box": {
      "type": "Polygon",
      "coordinates": [[
        [-4.3939, 55.7943],
        [-4.3939, 55.9072],
        [-4.0892, 55.9072],
        [-4.0892, 55.7943]
      ]]
    }
  },
  "geo_enabled": true
}
```

**Explanation:**
- This tweet has a `place` object but `coordinates` is null
- The user has enabled geolocation (`geo_enabled: true`) but chose to share only the general place (Glasgow) rather than precise coordinates
- For geolocation analysis, we can still determine that this tweet is about Glasgow, but we don't know the exact location within the city

#### Example: Tweet with Location Mentioned in Text (No Explicit Geolocation)

```json
{
  "created_at": "Fri Oct 13 09:23:45 +0000 2023",
  "id": 1582345678901234567,
  "id_str": "1582345678901234567",
  "text": "Hearing reports of a traffic accident near Buchanan Street station in Glasgow city center. Anyone know what's happening? #Glasgow",
  "user": {
    "id": 23456789,
    "id_str": "23456789",
    "name": "Local News Watcher",
    "screen_name": "newswatcher",
    "location": "UK",
    "description": "Keeping an eye on local events",
    "verified": false
  },
  "coordinates": null,
  "place": null,
  "geo_enabled": false,
  "entities": {
    "hashtags": [
      {"text": "Glasgow", "indices": [102, 110]}
    ]
  }
}
```

**Explanation:**
- This tweet has no explicit geolocation data (`coordinates` and `place` are both null)
- The user has not enabled geolocation (`geo_enabled: false`)
- However, the tweet text mentions specific locations: "Buchanan Street station" and "Glasgow city center"
- The tweet also includes a hashtag "#Glasgow"
- For geolocation analysis, natural language processing techniques would be needed to extract these location references from the text

### Data Structure for Analysis
The JSON structure of tweets provides multiple fields relevant to geolocation:
- `coordinates`: Contains precise latitude and longitude (when available)
- `place`: Contains location information like country, city, bounding box
- `user.location`: Free-text location field from user profile
- `user.time_zone`: User's selected time zone
- `lang`: Language of the tweet

#### Example: Structured Data for Geolocation Analysis

```json
{
  "tweet_id": "1583456789012345678",
  "timestamp": "2023-10-14T15:30:22Z",
  "text": "Major traffic accident on M8 eastbound near junction 15. Emergency services on scene. Expect delays. #TrafficScotland",
  "user": {
    "id": "34567890",
    "screen_name": "trafficscotland",
    "verified": true,
    "followers_count": 213456
  },
  "location_data": {
    "explicit_coordinates": [-4.2650, 55.8680],
    "place_name": "Glasgow, Scotland",
    "place_type": "city",
    "bounding_box": [[-4.3939, 55.7943], [-4.3939, 55.9072], [-4.0892, 55.9072], [-4.0892, 55.7943]],
    "user_profile_location": "Scotland, UK",
    "mentioned_locations": ["M8", "junction 15"]
  },
  "credibility_score": 0.92,
  "event_type": "traffic_incident"
}
```

**Explanation:**
- This structured format combines various location indicators from the original Twitter JSON
- `explicit_coordinates`: Precise location if available
- `place_name` and `place_type`: From the Place object
- `bounding_box`: Geographical boundaries of the place
- `user_profile_location`: From the user's profile
- `mentioned_locations`: Extracted from the tweet text using NLP
- `credibility_score`: Calculated based on user verification, follower count, etc.
- `event_type`: Categorized based on content analysis

![](./img/2025-03-11-20-24-52.png)

![](./img/2025-03-11-20-25-37.png)


![](./img/2025-03-11-20-27-00.png)

![](./img/2025-03-11-20-27-11.png)

![](./img/2025-03-11-20-27-17.png)

![](./img/2025-03-11-20-27-23.png)

![](./img/2025-03-11-20-27-29.png)

![](./img/2025-03-11-20-27-35.png)

![](./img/2025-03-11-20-27-43.png)

## Place Object

- Places are specific, named locations with corresponding geo-coordinates
- When users decide to assign a location to their Tweet, they are presented with a list of candidate Twitter Places
- When suing the API to post a Tweet, a Twitter Place can be attached b y specifying a place_id when posting the Tweet
- Tweets associated with Places are not necessarily issued from that location but could also potentially be about that location

### Detailed Place Object Example

```json
{
  "place": {
    "id": "1a2b3c4d5e6f7g8h",
    "url": "https://api.twitter.com/1.1/geo/id/1a2b3c4d5e6f7g8h.json",
    "place_type": "poi",
    "name": "Glasgow Central Station",
    "full_name": "Glasgow Central Station, Glasgow",
    "country_code": "GB",
    "country": "United Kingdom",
    "contained_within": [
      {
        "id": "0e8b2a4c5f6d7e8f",
        "place_type": "city",
        "name": "Glasgow",
        "full_name": "Glasgow, Scotland"
      }
    ],
    "bounding_box": {
      "type": "Polygon",
      "coordinates": [[
        [-4.2590, 55.8581],
        [-4.2590, 55.8599],
        [-4.2570, 55.8599],
        [-4.2570, 55.8581]
      ]]
    },
    "attributes": {
      "street_address": "Gordon Street",
      "locality": "Glasgow City Centre",
      "region": "Scotland",
      "iso3": "GBR"
    }
  }
}
```

**Explanation:**
- This is a detailed Place object for a point of interest (POI) - Glasgow Central Station
- `place_type`: "poi" indicates this is a specific point of interest rather than a city or country
- `contained_within`: Shows the hierarchical relationship (this POI is within Glasgow city)
- `bounding_box`: Provides precise geographical boundaries of the station
- `attributes`: Contains additional location details like street address and locality
- This level of detail is valuable for fine-grained geolocation analysis, allowing precise mapping of tweets to specific venues or landmarks

### Example: Tweet with Credibility Indicators for Geolocation

```json
{
  "created_at": "Sat Oct 14 15:30:22 +0000 2023",
  "id": 1583456789012345678,
  "id_str": "1583456789012345678",
  "text": "Major traffic accident on M8 eastbound near junction 15. Emergency services on scene. Expect delays. #TrafficScotland",
  "user": {
    "id": 34567890,
    "id_str": "34567890",
    "name": "Traffic Scotland Official",
    "screen_name": "trafficscotland",
    "location": "Scotland, UK",
    "description": "Official account for traffic updates in Scotland",
    "verified": true,
    "followers_count": 213456,
    "statuses_count": 45678,
    "created_at": "Mon Jan 15 10:00:00 +0000 2015"
  },
  "coordinates": {
    "type": "Point",
    "coordinates": [-4.2650, 55.8680]
  },
  "place": {
    "id": "0e8b2a4c5f6d7e8f",
    "place_type": "city",
    "name": "Glasgow",
    "full_name": "Glasgow, Scotland",
    "country_code": "GB",
    "country": "United Kingdom"
  },
  "geo_enabled": true,
  "source": "<a href=\"https://traffic.gov.uk\" rel=\"nofollow\">Traffic Scotland Web App</a>"
}
```

**Explanation:**
- This tweet contains several indicators that would contribute to high credibility for geolocation:
  - `user.verified`: True indicates this is an official verified account
  - `user.followers_count`: High number of followers (213,456) suggests authority
  - `user.description`: Identifies as an "Official account for traffic updates"
  - `source`: Posted from "Traffic Scotland Web App" rather than a general consumer app
  - `coordinates`: Contains precise location data
- When using weighted algorithms for geolocation analysis, tweets like this would receive higher credibility scores
- The combination of verified status, official source, and precise coordinates makes this tweet highly reliable for traffic incident detection

![](./img/2025-03-11-20-29-16.png)

![](./img/2025-03-11-20-29-24.png)

![](./img/2025-03-11-20-29-41.png)

![](./img/2025-03-11-20-29-49.png)

![](./img/2025-03-11-20-29-55.png)

## Tutorial Questions and Answers

### Why do you think location information is important?
Location information is critically important for numerous applications:
- **Emergency response and disaster management**: Enables rapid identification of affected areas and coordination of resources during crises
- **Urban planning and infrastructure development**: Helps understand population movement patterns and service needs
- **Targeted marketing and business intelligence**: Allows businesses to reach relevant local audiences
- **Transportation and logistics optimization**: Facilitates route planning and traffic management
- **Public health monitoring**: Helps track disease spread and allocate healthcare resources
- **Social research and behavioral analysis**: Provides context for understanding human activities and interactions
- **Content personalization**: Enables delivery of location-relevant information to users

### What are the benefits of location information?
Location information provides several key benefits:
- **Contextual understanding**: Adds spatial dimension to data, making it more meaningful
- **Pattern recognition**: Reveals geographic trends and clusters that might otherwise be invisible
- **Predictive capabilities**: Enables forecasting based on spatial relationships and historical patterns
- **Resource optimization**: Allows for more efficient allocation of services and infrastructure
- **Enhanced user experiences**: Provides personalized, location-relevant content and services
- **Improved decision-making**: Offers critical spatial context for both operational and strategic decisions
- **Cross-domain insights**: Connects data from different sources based on shared geographic attributes

### How does Twitter encode location information & their advantages and limitations?

Twitter encodes location information through several methods:

**Methods of Encoding:**
1. **Precise coordinates**: Exact latitude/longitude when users opt to share their precise location
2. **Place objects**: Named locations with defined boundaries (countries, cities, neighborhoods)
3. **User profile location**: Free-text field where users can enter their location
4. **Time zone information**: User's selected time zone
5. **Content-based location references**: Mentions of places within tweet text

**Advantages:**
- **Multiple granularity levels**: From precise coordinates to general regions
- **User control**: Users can choose how much location data to share
- **Structured data**: Place objects provide standardized location information
- **Contextual enrichment**: Adds geographic dimension to social media analysis
- **Real-time insights**: Provides location data for events as they unfold

**Limitations:**
- **Opt-in nature**: Only a small percentage of tweets contain precise coordinates
- **Accuracy issues**: User-provided location fields may contain inaccurate or fictional places
- **Inconsistent availability**: Not all tweets have associated location data
- **Privacy constraints**: API restrictions limit access to certain location data
- **Ambiguity**: Place mentions in text may be references rather than actual locations
- **Representativeness concerns**: Location-sharing users may not represent the broader population

![](./img/Content%20Processing%20&%20Clustering%20(内容处理与聚类)%20⭐⭐⭐⭐.png)

# Content Processing

![](./img/2025-03-11-20-42-49.png)

![](./img/2025-03-11-20-42-56.png)

![](./img/2025-03-11-20-43-03.png)

![](./img/2025-03-11-20-43-08.png)

![](./img/2025-03-11-20-43-14.png)

## Processing and Cleansing Social Media Data

From a data science perspective, processing social media data involves several critical steps to transform raw, unstructured content into analyzable information:

### Text Preprocessing Pipeline

1. **Data Collection and Extraction**
   - API-based collection (rate limits and sampling considerations)
   - Web scraping (ethical and legal considerations)
   - Historical data access limitations

2. **Basic Cleaning Operations**
   - Removing duplicate content
   - Handling missing values
   - Filtering out non-relevant content
   - Normalizing text encoding (UTF-8 standardization)

3. **Text Normalization**
   - Case normalization (typically lowercasing)
   - Punctuation removal or standardization
   - Whitespace normalization
   - Special character handling
   - URL standardization or removal

4. **Linguistic Processing**
   - Tokenization (word, sentence, n-gram)
   - Stop word removal (context-dependent)
   - Stemming and lemmatization
   - Part-of-speech tagging
   - Named entity recognition (identifying locations, organizations, people)

5. **Social Media-Specific Elements**
   - Hashtag segmentation (#ClimateChangeNow → Climate Change Now)
   - Username handling (@mentions)
   - Emoji interpretation and standardization
   - Handling platform-specific features (retweets, quote tweets)
   - Slang and abbreviation normalization

6. **ASCII Processing Considerations**
   - Converting non-ASCII characters to ASCII equivalents
   - Handling extended character sets
   - Detecting and managing encoding errors
   - ASCII art and special formatting removal
   - Control character filtering

7. **Feature Engineering**
   - Text vectorization (Bag-of-Words, TF-IDF, embeddings)
   - Sentiment analysis features
   - Temporal features (posting time, frequency)
   - Network-based features (user interactions)
   - Geographic feature extraction

8. **Quality Assessment**
   - Spam and bot content detection
   - Credibility scoring
   - Content relevance evaluation
   - Representativeness analysis
   - Bias identification

9. **Ethical Considerations**
   - Privacy protection (PII removal)
   - Demographic bias awareness
   - Context preservation
   - Source attribution
   - Responsible reporting of findings

10. **Data Storage and Documentation**
    - Structured storage formats (CSV, JSON, databases)
    - Processing pipeline documentation
    - Version control for datasets
    - Metadata preservation
    - Reproducibility considerations

The cleansing process must balance removing noise while preserving meaningful signal, especially considering the informal, abbreviated, and context-dependent nature of social media communication.

![](./img/2025-03-11-20-46-47.png)

![](./img/2025-03-11-20-46-54.png)

![](./img/2025-03-11-20-47-03.png)

![](./img/2025-03-11-20-47-10.png)

## Text Vector Representation

### Vector Space Model for Documents and Queries

Text vector representation is a fundamental concept in information retrieval and natural language processing that converts text documents into mathematical vectors for computational analysis:

- **Document Vectorization**: Each document is transformed into a numerical vector
  $$D_i = (t_{i1}, t_{i2}, \dots, t_{in})$$
  Where:
  - $D_i$ represents document i
  - Each element $t_{ij}$ represents the weight of term j in document i
  - n is the total number of unique terms in the collection

- **Query Vectorization**: Similarly, search queries are converted into the same vector space
  $$Q = (qt_1, qt_2, \dots, qt_n)$$
  Where:
  - Each element $qt_j$ represents the weight of term j in the query
  - The dimensionality matches the document vectors for direct comparison

### Binary Representation Approach

The simplest implementation uses binary weights:
- $t_{ik} = 1$ if term k appears in document i (regardless of frequency)
- $t_{ik} = 0$ if term k is absent from document i
- Similarly, $qt_k = 1$ if term k appears in the query, otherwise $qt_k = 0$

Example:
For the vocabulary ["glasgow", "traffic", "weather"], a tweet "Traffic in Glasgow" would be represented as:
$$D = (1, 1, 0)$$

This vector representation enables:
- Computing similarity between documents and queries using vector operations
- Clustering similar documents together
- Performing document classification
- Supporting geolocalisation by representing location terms in the vector space

More sophisticated weighting schemes like TF-IDF (Term Frequency-Inverse Document Frequency) extend this model by considering term frequency and importance.

![](./img/2025-03-11-20-49-24.png)

![](./img/2025-03-11-20-49-47.png)

## Similar Documents

The most relevant documents for a query are expected to be those represented by the vectors closest to the query vector, meaning documents that use similar words to the query. This concept is fundamental to information retrieval and document similarity analysis.

Closeness is often calculated by examining the angles between document vectors and the query vector rather than the absolute distances. This approach normalizes for document length, ensuring that the similarity measure focuses on content overlap rather than document size.

We need a robust similarity measure to quantify this closeness, which is why cosine similarity is commonly used in text analysis.

## Cosine Similarity Measure

Cosine similarity measures the cosine of the angle between two vectors, providing a value between -1 and 1 (though with text data, values are typically between 0 and 1 since term weights are non-negative).

For a document vector D and query vector Q:

$$
D = (t_1, t_2, \dots, t_n)
$$

$$
Q = (qt_1, qt_2, \dots, qt_n)
$$

The cosine similarity is calculated as:

$$
\cos(D, Q) = \frac{\sum^n_{i=1}t_i \times qt_i}{\sqrt{\sum^n_{i=1}t_i^2} \times \sqrt{\sum^n_{i=1}qt_i^2}}
$$

Where:
- The numerator represents the dot product of the two vectors
- The denominator normalizes by the product of the vector magnitudes
- n is the number of dimensions (terms) in the vector space

The result indicates:
- 1: Vectors are identical (0° angle)
- 0: Vectors are orthogonal (90° angle)
- -1: Vectors point in opposite directions (180° angle)

Example:
For D = (1, 1, 0) and Q = (1, 0, 0):
$$
\cos(D, Q) = \frac{1 \times 1 + 1 \times 0 + 0 \times 0}{\sqrt{1^2 + 1^2 + 0^2} \times \sqrt{1^2 + 0^2 + 0^2}} = \frac{1}{\sqrt{2} \times 1} = \frac{1}{\sqrt{2}} \approx 0.707
$$

## Length of a Vector

The magnitude (or length) of a vector is its size, calculated using the Euclidean norm:

$$
\|V\| = \sqrt{\sum^n_{i=1}v_i^2}
$$

Where:
- $\|V\|$ denotes the magnitude of vector V
- $v_i$ is the value of the ith component
- n is the number of dimensions

Example:
For a vector V = (3, 4):
$$
\|V\| = \sqrt{3^2 + 4^2} = \sqrt{9 + 16} = \sqrt{25} = 5
$$

## Unit Vector

A unit vector has a magnitude of 1 while maintaining the same direction as the original vector. To normalize a vector (convert it to a unit vector):

For any vector $\vec{v}$, its unit vector $\hat{v}$ is calculated as:

$$
\hat{v} = \frac{\vec{v}}{\|\vec{v}\|}
$$

Where:
- $\vec{v}$ is the original vector
- $\|\vec{v}\|$ is the magnitude of the vector
- $\hat{v}$ is the resulting unit vector

Example:
For a vector $\vec{v} = (3, 4)$:
1. Calculate magnitude: $\|\vec{v}\| = \sqrt{3^2 + 4^2} = 5$
2. Normalize: $\hat{v} = (\frac{3}{5}, \frac{4}{5})$

In text analysis:
- If each term has weight 1, normalizing by $\frac{1}{\sqrt{n}}$ where n is the number of terms
- For a tweet with 19 terms, each term's normalized weight would be $\frac{1}{\sqrt{19}} \approx 0.229$

This normalization ensures that document length doesn't dominate similarity calculations, focusing instead on term distribution patterns.

## Similarity Computation

### Cosine Similarity

Cosine similarity measures the cosine of the angle between two vectors, providing a value between -1 and 1 (though in text analysis with non-negative weights, the range is typically 0 to 1). A value of 1 means the vectors are identical in direction, 0 means they are orthogonal (completely different), and -1 means they point in opposite directions.

### Similarity vs. Dissimilarity (Distance)

- **Similarity measures** increase as objects become more alike (cosine similarity, Jaccard similarity)
- **Dissimilarity measures** (or distances) increase as objects become more different (Euclidean distance, Manhattan distance)
- The relationship is often inverse: similarity = 1 - normalized_distance

### Working with Normalized Vectors:

- **Benefits are**:
  - Eliminates the influence of document length on similarity calculations
  - Makes documents comparable regardless of their size
  - Simplifies computational complexity
  - Focuses on term distribution patterns rather than absolute frequencies
- **Similarity can be computed just using sum of $t_i\times qt_i$** when vectors are normalized, as the denominator in the cosine similarity formula becomes 1

![](./img/2025-03-11-21-00-11.png)

![](./img/2025-03-11-21-00-19.png)

![](./img/2025-03-11-21-00-25.png)

![](./img/2025-03-11-21-00-30.png)

![](./img/2025-03-11-21-00-35.png)

## Text Processing Pipeline

The text processing pipeline is a series of steps applied to raw text to transform it into a format suitable for computational analysis:

1. **Tokenization**: Breaking text into individual words or tokens. For example, "The cat sat on the mat" becomes ["The", "cat", "sat", "on", "the", "mat"].

2. **Normalization**: Converting text to lowercase, removing accents, and standardizing characters. This ensures consistency in analysis by treating "Cat" and "cat" as the same token.

3. **Stopword removal**: Eliminating common words with little semantic value (e.g., "the", "is", "and", "of") that occur frequently but contribute minimal meaning to the analysis.

4. **Stemming/Lemmatization**: Reducing words to their root forms.
   - Stemming: A heuristic process that chops off word endings (e.g., "running" → "run", "cats" → "cat")
   - Lemmatization: A more sophisticated approach using vocabulary and morphological analysis to return the base dictionary form (e.g., "better" → "good", "was" → "be")

5. **Feature extraction**: Converting processed text into numerical representations such as:
   - Bag-of-Words (BoW): Counting word occurrences
   - TF-IDF: Weighting terms by their importance
   - Word embeddings: Representing words as dense vectors in a continuous vector space

This systematic approach ensures consistency in text analysis and improves the quality of results in applications like search, classification, and clustering.

![](./img/2025-03-11-21-01-13.png)

## Term Weighting

Term weighting is the process of assigning importance values to unique words (features) in a document, determining how significant each dimension is in the vector space model.

### In documents, such as web pages:
- If a word is repeated many times within a document, it generally indicates that the document focuses on that concept
- Repetition is considered a signal of importance
- Term frequency (TF) is often used as a basic weighting scheme, defined as:

$$TF(t,d) = \frac{\text{Number of times term } t \text{ appears in document } d}{\text{Total number of terms in document } d}$$

- More sophisticated approaches like TF-IDF (Term Frequency-Inverse Document Frequency) balance term frequency with how common the term is across all documents:

$$TF\text{-}IDF(t,d,D) = TF(t,d) \times IDF(t,D)$$

Where IDF is calculated as:

$$IDF(t,D) = \log\frac{\text{Total number of documents in corpus } D}{\text{Number of documents containing term } t}$$

### However, in tweets and short social media posts:
- Words are rarely repeated due to the limited character count (typically 280 characters for Twitter)
- The binary presence of a term is often more meaningful than its frequency
- We typically assume all present words are equally important
- If a word appears in the tweet, that dimension becomes active (value of 1) in the underlying vector representation
- This binary representation works well for short text classification and clustering, and can be formalized as:

$$weight(t,d) = \begin{cases} 
1 & \text{if term } t \text{ appears in document } d \\
0 & \text{otherwise}
\end{cases}$$

![](./img/2025-03-11-21-02-57.png)

![](./img/2025-03-11-21-03-03.png)

## Finding similar tweets

### What is a cluster?

In General Usage:
- A cluster is simply a collection or group of similar things located close together: Example: a cluster of grapes, buildings, or ideas
- In our context:
  - A group of similar tweets grouped together based on certain characteristics or features
  - Tweets sharing common words, topics, or semantic meaning
  - Documents that are close to each other in the vector space representation
  
### Clustering in Text Analysis
- Clustering organizes tweets into meaningful groups without predefined categories (unsupervised learning)
- Each cluster contains tweets that are more similar to each other than to tweets in other clusters
- Similarity is typically measured using distance metrics like cosine similarity in the vector space
- The goal is to maximize intra-cluster similarity while minimizing inter-cluster similarity, which can be expressed mathematically as:
  - Maximize: $\sum_{i=1}^{k} \sum_{x \in C_i} similarity(x, \mu_i)$ where $\mu_i$ is the centroid of cluster $C_i$
  - Minimize: $\sum_{i=1}^{k} \sum_{j=1, j \neq i}^{k} similarity(\mu_i, \mu_j)$ for all pairs of cluster centroids

### Applications of Tweet Clustering
- Topic detection: Identifying emerging topics or trends in social media
- Event detection: Recognizing real-world events based on sudden clusters of related tweets
- Information summarization: Condensing large volumes of tweets into representative groups
- Anomaly detection: Identifying outliers that don't fit well into any cluster
- Geographic analysis: Finding location-based patterns when combined with geolocation data


## Single-pass clustering
- Requires a single, sequential pass over the set of documents it attempts to cluster
- The idea is to group similar documents (tweets) as and when they arrive: sequential nature
- The algorithm classifies a document (the next one) in the sequence
  - Based on the current set of clusters and
  - According to a condition on the similarity function employed
  
- At every stage, the algorithm decides on whether a newly seen document should become a member of an already defined cluster or the center of a new one
  - In its most simple form, the similarity function gets defined based on
  - Just some similarity (or alternatively, dissimilarity) measure
  - Between document-feature vectors
- Cosine similarity is commonly used, defined as:

$$similarity(A, B) = \cos(\theta) = \frac{A \cdot B}{||A|| \times ||B||} = \frac{\sum_{i=1}^{n} A_i B_i}{\sqrt{\sum_{i=1}^{n} A_i^2} \times \sqrt{\sum_{i=1}^{n} B_i^2}}$$

Where $A$ and $B$ are the vector representations of two documents.

## Cluster centroid

Given a set of documents (tweets) in a cluster $C = \{D_1, D_2, ..., D_n\}$:
- We take the average of the vector representation as a representation of the cluster/group
- The centroid $\mu_C$ is calculated as:

$$\mu_C = \frac{1}{|C|} \sum_{D \in C} D$$

Where:
- $|C|$ is the number of documents in cluster $C$
- $D$ is the vector representation of a document

Remember, we are grouping based on the content representation:
- Hence, we assume the documents are similar
- In terms of word similarity and hence
- Semantic similarity

Cluster centroid is the representation of group/cluster:
- Think of it as a "virtual document" that represents the average content of all documents in the cluster
- It may not correspond to any actual document in the cluster, but serves as an abstract representation of the cluster's central theme

![](./img/2025-03-11-21-09-30.png)

## Stream of tweets

Twitter generates approximately 500 million tweets per day (about 6,000 tweets per second). These tweets arrive one after another in a continuous stream.

We want to cluster them as they arrive, which presents several challenges:
- Limited memory: Cannot store all tweets in memory
- Real-time processing: Need to make decisions quickly
- Evolving topics: Clusters may change over time
- One-pass constraint: Cannot revisit all previous tweets

## Single Pass Clustering Steps

The general algorithm is as follows:
1. Step 1
   1. Assign the first document $D_1$ as the representative of the first cluster $C_1$
   2. Document vector becomes the cluster vector/centroid
2. Step 2
   1. For each incoming document $D_i$, calculate the similarity $S$ with the representative for each existing cluster
   2. Document vector $D_i$ is compared to each cluster centroid
      1. We need a cluster centroid - or an average representation of documents in the cluster
   3. Let $S_{max}$ be the maximum similarity between the incoming document and any existing cluster:
      $$S_{max} = \max_{j} \{similarity(D_i, \mu_{C_j})\}$$
3. Step 3
   1. If $S_{max}$ is greater than a predefined threshold value $S_{T}$
      1. Add the item to the corresponding cluster $C_j$ -> we need to make sure the similarity is substantial
      2. Recalculate the cluster representative (centroid):
         $$\mu_{C_j}^{new} = \frac{|C_j| \times \mu_{C_j}^{old} + D_i}{|C_j| + 1}$$
   2. Otherwise, use $D_i$ to initiate a new cluster $C_{k+1}$ where $k$ is the current number of clusters
4. Step 4
   1. For a new item $D_{i+1}$ to be clustered, return to step 2

## How to group tweets

The key components for effective tweet clustering are:

1. **Cosine similarity**: Measures the angle between two document vectors, providing a value between -1 and 1 (though with non-negative weights, the range is typically 0 to 1).

2. **Similarity Threshold** ($S_T$): A critical parameter that determines when to create a new cluster versus adding to an existing one. Typically set between 0.3 and 0.7, depending on:
   - Desired granularity of clusters
   - Nature of the data
   - Specific application requirements

The threshold can be determined empirically through experimentation or by domain knowledge.

## Comments

The single pass method is particularly simple (and useful in this scenario):
   - It requires that the dataset be processed only once
   - It handles data as it arrives (streaming)
   - It has O(nk) time complexity, where n is the number of documents and k is the number of clusters

Obviously, the results for this method are highly dependent:
- On the similarity threshold that is used
- The order in which documents are processed


## Comments & Observations

It tends to produce large clusters early in the clustering pass:
- The clusters formed are not independent of the order in which the dataset is processed
  - Because similar documents arriving in different order would create different clusters
  - You should use your judgment in setting the threshold so that you are left with a reasonable number of clusters
- Post-processing tips:
  - Use to form the groups initially, which are used to reallocate/create new clusters
  - If we get large noisy clusters of tweets, we could re-cluster them
  - Consider periodic rebalancing of clusters to improve quality

## Moving average

Moving average is a calculation technique used to analyze data points by creating a series of averages of different subsets of the full dataset. In the context of clustering tweets, moving averages can help adapt to evolving topics and trends.

The simple moving average (SMA) of a cluster centroid can be calculated as:

$$\mu_{C,t} = \frac{1}{w} \sum_{i=t-w+1}^{t} D_i$$

Where:
- $\mu_{C,t}$ is the centroid at time t
- $w$ is the window size (number of recent documents to consider)
- $D_i$ represents the document vectors in the cluster

The exponential moving average (EMA) gives more weight to recent documents:

$$\mu_{C,t} = \alpha \times D_t + (1-\alpha) \times \mu_{C,t-1}$$

Where:
- $\alpha$ is the smoothing factor (typically between 0.1 and 0.3)
- $D_t$ is the newest document
- $\mu_{C,t-1}$ is the previous centroid

How moving averages affect our clusters:

1. **Temporal relevance**: Recent tweets have more influence on cluster representation
2. **Drift adaptation**: Clusters can gradually shift to follow evolving topics
3. **Noise reduction**: Smooths out random fluctuations in cluster centroids
4. **Memory efficiency**: Only need to store the current centroid and smoothing parameters, not all historical tweets
5. **Concept decay**: Older content gradually loses influence, reflecting the natural lifecycle of topics on social media

By incorporating moving averages, the clustering algorithm becomes more responsive to current trends while maintaining computational efficiency in a streaming environment.

![](./img/Credibility%20&%20Newsworthiness%20(可信度与新闻价值)%20⭐⭐⭐⭐.png)