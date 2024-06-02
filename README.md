# 3DLNews: A Three-decade Dataset of US Local News Articles

We present 3DLNews, a novel dataset with local news articles from the United States spanning the period from 1996 to 2024. It contains almost 1 million URLs (and HTML text) from over 14,000 local newspapers, TV, and radio stations across all 50 states, and provides a broad snapshot of the US local news landscape. The dataset was collected by scraping Google and Twitter search results. We employed a multi-step filtering process to remove non-news article links and enriched the dataset with metadata such as the names and geo-coordinates of the source news media organizations, article publication dates, etc. Furthermore, we demonstrated the utility of 3DLNews by outlining four applications.

### Key Features
- **Time Span:** Articles from 1996 to 2024, offering a nearly three-decade perspective on local news.
- **Geographical Coverage:** Nearly 1 million URLs sourced from more than 10,000 local news outlets across all 50 states.
- **Metadata Enrichment**: The dataset includes relevant metadata to provide additional context for analysis.
  
### Potential Applications.
- Exploring the Nationalization of Local News
- Media Bias Analysis
- Studying US Local News Deserts
- Community Understanding, Trend Analysis and Prediction
  
To cite, kindly use:

```
@article{gangani_nwala_3dlnews,
  title={A Three-decade Dataset of US Local News Articles},
  author={Gangani Ariyarathne, Nwala, Alexander C.},
  year = {2024},
  url = {https://github.com/GANGANI/3DLNews}
}
```

### Getting Started

- Clone this repository to your local machine using git clone.
  ```
  git clone https://github.com/GANGANI/3DLNews.git
  ```
- The structure of the data is as follows.
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
  └── Google
      ├── 1-Newspapers
      ├── 2-Radio
      ├── 3-TV
      └── 4-Broadcast
  ```
  
**Table: US local news media dataset**

| Media Type | Number of websites |
|------------|---------------------|
| Newspapers | 9,441               |
| Radio      | 2,449               |
| Broadcast  | 1,310               |
| TV         | 886                 |
| **Total**  | **14,086**          |



**Table: 3DLNews-raw: Number of URLs (non-news URLs included)**

| Type        | Google        | Twitter       | Total         |
|-------------|---------------|---------------|---------------|
| Newspapers  | 853,543       | 199,996       | 1,053,539     |
| Radio       | 140,401       | 102,494       | 242,895       |
| TV          | 99,001        | 66,880        | 165,881       |
| Broadcast   | 164,028       | 100,119       | 264,147       |
| **Total**   | **1,256,973** | **469,489**   | **1,726,462** |


**Table: 3DLNews: Number of news article URLs (non-news URLs excluded)**

| Type        | Google    | Twitter   | Total     |
|-------------|-----------|-----------|-----------|
| Newspapers  | 502,530   | 64,886    | 618,686   |
| Radio       | 52,925    | 555       | 64,658    |
| TV          | 62,727    | 22,675    | 105,008   |
| Broadcast   | 110,494   | 7,783     | 130,144   |
| **Total**   | **728,676** | **95,899** | **824,575** |

