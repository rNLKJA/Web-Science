# Geo localisation & Web Science

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
