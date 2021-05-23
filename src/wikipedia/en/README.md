# Wikipedia, English language exploratory data analysis

## Wikipedia Stubs

### Analysis 1: Proportion of stub files

Methods: Pulled three samples of 1000 random English language Wikipedia articles by HTTP GET request with the Wikipedia API and analyzed the proportion of articles that were classified as "stubs" (i.e. incomplete articles that require additional content).  HTML was parsed with BeautifulSoup v4 and content was extracted from `<p>` fields in the articles.  Text strings were pre-processed with the following Python source prior to analysis:

```python
REF_RE = re.compile(r"\[\d{1,3}\]")

def clean(text):
    # remove "[edit]" strings that are used for content editing
    cleaned_content = text.replace("[edit]", "")
    # remove "[\d]" style reference strings
    cleaned_content = re.sub(REF_RE, "", cleaned_content)
    # remove "[citation neeeded]" editorial strings
    cleaned_content = cleaned_content.replace("[citation needed]", "")

    return cleaned_content
```

Results: The stub content counts for the three test trials were:

- Trial 1: 366 / 1000 (36.6%)
- Trial 2: 374 / 1000 (37.4%)
- Trial 3: 381 / 1000 (38.1%)

A mean of 37.4% English language articles were classified as article stubs.

### Analysis 2: Stub vs. Full Article (Non-Stub) Lengths

Stub and full-length (non-stub) articles were compared for:

1. Content byte size
2. Content token count
3. Content sentence count

Stub articles had significantly smaller content byte size, token counts, and sentence counts relative to full-length articles.  This was a highly statistically significant finding at the p<0.00001 level.  The analysis implementation and findings are documented in the [EDA_WikipediaStubs.ipynb](wikipedia-stubs/EDA_WikipediaStubs.ipynb) notebook.  Analysis data available in the [wikipedia-stubs/data.tar.xz](wikipedia-stubs/data.tar.xz) archive.

