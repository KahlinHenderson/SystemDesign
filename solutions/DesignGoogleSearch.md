Google Search is a system that finds and returns web pages containing keywords given by the user. It’s comprised of three main components.

Web Crawler: maintains a list of URLs to visit. As the crawler visits the URLs it identifies the links in the pages and adds them to the list. It extracts the content of each page and uses the information to measure the relevance of the page compared to similar ones.

Inverted Index: A hashmap in which each key is a keyword and the corresponding value is a list of pages containing the keyword.

Query Processor: Retrieves pages containing the keywords in the search query. It may perform a conjunctive search, a disjunctive search or a combination of both. A conjunctive search finds pages that contain all of the keywords. A disjunctive search finds pages that contain at least one of the keywords.



