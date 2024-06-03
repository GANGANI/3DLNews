# 3DLNews: A Three-decade Dataset of US Local News Articles

## 1. About 
We present 3DLNews, a novel dataset with local news articles from the United States spanning the period from 1996 to 2024. It contains almost 1 million URLs (and HTML text) from over 14,000 local newspapers, TV, and radio stations across all 50 states, and provides a broad snapshot of the US local news landscape. The dataset was collected by scraping Google and Twitter search results. We employed a multi-step filtering process to remove non-news article links and enriched the dataset with metadata such as the names and geo-coordinates of the source news media organizations, article publication dates, etc. Furthermore, we demonstrated the utility of 3DLNews by outlining four applications.
  
To cite, kindly use:

```
@article{gangani_nwala_3dlnews,
  title={A Three-decade Dataset of US Local News Articles},
  author={Gangani Ariyarathne, Nwala, Alexander C.},
  year = {2024},
  url = {https://github.com/GANGANI/3DLNews}
}
```

- Clone this repository to your local machine using git clone.
  ```
  git clone https://github.com/GANGANI/3DLNews.git
  ```
## 2. 3DL News Dataset

### 2.1 Local news media dataset
We used an extended version of the Local Memory Project's (LMP) US local news dataset to get the local news media outlets. LMP's dataset consists of the websites of 5,993 local newspapers, 2,539 TV stations, and 1,061 radio stations, primarily extracted from (thepaperboy.com)[thepaperboy.com] in 2016. We extended it by crawling and scraping thepaperboy.com (again), web.archive.org/web/20221203031956/http://www.usnpl.com/, 50states.com, and einpresswire.com/world-media-directory/3/united-states. Table 1 outline the number of local news media outlets that we have used to extract local news articles. The ``broadcast'' type refers to either TV or radio stations, because we could not accurately distinguish them during scraping.

**Table 1:  US local news media dataset.**
| Media Type | Number of websites |
|------------|---------------------|
| Newspapers | 9,441               |
| Radio      | 2,449               |
| Broadcast  | 1,310               |
| TV         | 886                 |
| **Total**  | **14,086**          |
 and filtering

We issued Google and Twitter search queries to their respective search engines and scraped their links. For Google, we reated queries from 1996 – 2024, for Twitter, 2006 – 2024. Table 2
presents the number of links scraped from Google and Twitter for each media type.

**Table 2: 3DLNews-raw: Number of URLs (non-news URLs included)**

| Type        | Google        | Twitter       | Total         |
|-------------|---------------|---------------|---------------|
| Newspapers  | 853,543       | 199,996       | 1,053,539     |
| Radio       | 140,401       | 102,494       | 242,895       |
| TV          | 99,001        | 66,880        | 165,881       |
| Broadcast   | 164,028       | 100,119       | 264,147       |
| **Total**   | **1,256,973** | **469,489**   | **1,726,462** |

### 2.2 Data Filtering

We removed non-news article links by applying a filtering process outlined below. 
```
Step 1: Dereferenced all URLs to resolve redirects and retrieved final URLs that returned HTTP 200 response codes.
Step 2: Removed links with domains not present in our local news media dataset.
Step 3: Third, we converted all URLs to lowercase, discarded trailing slashes, and removed duplicate URLs.
Step 4: As URLs with a path depth of zero, typically representing homepages, URLs with a path depth of zero were removed.
Step 5: As we observed that news URLs occurred at lower path depths (e.g.,< 3), we kept such news article URLs only if they included popular word-boundary separators such as ‘-’, ‘_’, or ‘.’ We kept all URLs with path depth ≥ 3. 
```

Table 3 presents the number of news articles after filtering.

**Table 3: 3DLNews: Number of news article URLs (non-news URLs excluded)**

| Type        | Google    | Twitter   | Total     |
|-------------|-----------|-----------|-----------|
| Newspapers  | 502,530   | 64,886    | 618,686   |
| Radio       | 52,925    | 555       | 64,658    |
| TV          | 62,727    | 22,675    | 105,008   |
| Broadcast   | 110,494   | 7,783     | 130,144   |
| **Total**   | **728,676** | **95,899** | **824,575** |

### 2.3 Data Enrichment 
We enhanced the usefulness of the news article URLs in 3DLNews by adding attributes to each URL. Table 4 outlines the complete list of attributes. 

# Table 4: Properties of news article URLs in 3DLNews

| Property          | Description                                                                                                                                               | Example                                               |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| link              | The URL of the local news article.                                                                                                                         | `[[https://www.example.com/article123](https://www.adn.com/alaska-news/article/womans-death-montana-has-eerie-echoes-yakutat-killing/2009/01/23/)](https://www.adn.com/alaska-news/article/womans-death-montana-has-eerie-echoes-yakutat-killing/2009/01/23/)`                  |
| html_filename     | Filename with HTML content of the article.                                                                                                                 | `556a766d0ee6d588632f30b662ada710.html`                                     |
| publication_date  | Article publication date.                                                                                                                                 | `2023-06-01/23/2009`                                          |
| title             | Title of the article.                                                                                                                                      | "Woman's death in Montana has eerie echoes of Yakutat killing - Anchorage Daily News"                                   |
| media_name        | Name of local media organization.                                                                                                                          | "Alaska Dispatch News"                                       |
| media_type        | Type of media source (*Newspaper* or *TV* or *Radio station* or *Broadcast*). "Broadcast" refers to either TV or radio stations.                           | `newspaper`                                           |
| location          | Location of the media organization. This includes: US state, city, & latitude/longitude.                                                                   | <details>
  <summary>{"state": "Alaska", "city": "Anchorage", "longitude": -149.87828, "latitude": 61.216799}<summary>   |
| media_metadata    | More information about the news media.                                                                                                                     | `Owned by Example Corp.`                              |
| source            | Platform (Google or Twitter) where the news article was extracted from.                                                                                    | `Google`                                              |
| source_metadata   | More information about the platform scraped.                                                                                                               | `Indexed by Google News`                              |
| response_code     | Response code returned following GET request of link.                                                                                                      | `200`                                                 |
| expanded_url      | Final target URL for links that redirect.                                                                                                                  | `https://www.example.com/final_article123`            |

Next, we highlight a few.
The link represents the news article URL. The html_filename
attribute points to the file containing the HTML text of news arti-
cle, while the publication_date refers to the article publication date
which was extracted using htmldate [3]. The location property of
each URL includes the US state, city, and latitude/longitude of the
source news media organization. The media_metadata contains in-
formation (e.g., newspaper or TV or radio name) about the news me-
dia website where the article was published. The source_metadata
includes information (e.g., search query link) about the source (Twit-
ter or Google) from which the article was scraped.
Each news article URL, along with its attributes (Table 5) is en-
capsulated in a JSON object within a single line in a file in 3DLNews

# Data Format

- The structure of the dataset is as follows.
  ```
  ├── Google
  │   ├── 1-Newspapers
  │   │   ├── state
  │   │   │   ├── AK
  │   |   │   |   ├── google_newspaper_AK_2006.jsonl.gz
  │   |   │   |   ├── google_newspaper_AK_2007.jsonl.gz
  │   |   │   |   ├── -------------------------------
  │   │   │   ├── --
  │   │   │   └── WY
  │   |   │       ├── google_newspaper_AK_2006.jsonl.gz
  │   |   │       ├── google_newspaper_AK_2007.jsonl.gz
  │   |   │       ├── -------------------------------
  │   │   ├── preprocessed_stat
  │   │   │   ├── AK
  │   |   │   |   ├── preprocessed_google_newspaper_AK_2006.jsonl.gz
  │   |   │   |   ├── preprocessed_google_newspaper_AK_2007.jsonl.gz
  │   |   │   |   ├── -------------------------------
  │   │   │   ├── --
  │   │   │   └── WY
  │   |   │       ├── preprocessed_google_newspaper_AK_2006.jsonl.gz
  │   |   │       ├── preprocessed_google_newspaper_AK_2007.jsonl.gz
  │   |   │       ├── -------------------------------
  │   │   ├── filtered_state
  │   │   │   ├── AK
  │   │   │   │   └── preprocessed_google_newspaper_AK.jsonl.gz
  │   │   │   └── AL
  │   │   │   │    └── preprocessed_google_newspaper_AL.jsonl.gz
  │   │   │   ├── --
  │   │   │   │   └── -----------------------------------------
  │   │   ├── HTML
  │   │   │   ├── AK
  │   │   │   │   ├── 1996
  │   │   │   │   │   ├── 0106eb41fcb93351d3bba81a67ecf487.html
  │   │   │   │   │   ├── 024b602f2a0c7edf53ee2a1b0228bfc5.html
  │   │   │   │   │   ├── -------------------------------------  
  │   │   │   │   ├── ----
  │   │   │   │   └──2024
  │   │   │   │       ├── 0106eb41fcb93351d3bba81a67ecf487.html
  │   │   │   │       ├── 024b602f2a0c7edf53ee2a1b0228bfc5.html
  │   │   │   │       ├── -------------------------------------  
  │   ├── 2-Radio
  │   ├── 3-TV
  │   └── 4-Broadcast
  └── Twitter
      ├── 1-Newspapers
      ├── 2-Radio
      ├── 3-TV
      └── 4-Broadcast
  ```
The directory named 'Google' contains JSONL files with news article URLs extracted via Google scraping. Each JSONL file represents a collection of URLs and their associated metadata gathered through automated searches on Google. The directory named 'Twitter' holds JSONL files with news article URLs obtained through Twitter scraping. Each JSONL file includes URLs and metadata collected from tweets, providing a diverse set of news articles shared on the Twitter platform.

Inside each Twitter and Google directories, it has 4 main directories for each news media type. Then inside the each media type folder it has for main directories as explained below.
- **state:** This directory contains the scarped data for each state for each year.
- **preprocessed_data:** This folder has set of directories for each state and inside that it has set of jsonl.gz files for each year. inside that Jsonl file it has data objects for each URL.
- **filtered_data:**  
##  
**Table:** US local news media dataset** his folder has set of directories for each state and inside that it has filtered article URLs.
**HTML:** This folder has the HTML content for each of the article named with the hash value of each article URL.









### Key Features
- **Time Span:** Articles from 1996 to 2024, offering a nearly three-decade perspective on local news.
- **Geographical Coverage:** Nearly 1 million URLs sourced from more than 10,000 local news outlets across all 50 states.
- **Metadata Enrichment**: The dataset includes relevant metadata to provide additional context for analysis.
  
### Potential Applications.
- Exploring the Nationalization of Local News
- Media Bias Analysis
- Studying US Local News Deserts
- Community Understanding, Trend Analysis and Prediction
