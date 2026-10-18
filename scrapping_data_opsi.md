# scrapping_data_
## Saya memakai (compass/crawler-google-places), ini tersedia di apify store

# ── Code cell 1 ──
```
!pip install apify-client 
!pip install pandas
```

# **Scrapping per-rumah sakit**

## ── Code cell 3 ──
```from google.colab import userdata

from apify_client import ApifyClient
import pandas as pd
client = ApifyClient(userdata.get("APIFY_TOKEN"))

run = client.actor("compass/crawler-google-places").call(run_input={
    "startUrls": [{"url": "https://www.google.com/maps/place/RS+Awal+Bros+Botania+Batam/@1.1108346,104.0744448,13z/data=!4m10!1m2!2m1!1srumah+sakit+di+batam3m61s0x31d98910e0bb27fd:0xcefae14a6bb4b82e8m2!3d1.1069458!4d104.090210215sChRydW1haCBzYWtpdCBkaSBiYXRhbVoWIhRydW1haCBzYWtpdCBkaSBiYXRhbZIBEHByaXZhdGVfaG9zcGl0YWyaASNDaFpEU1VoTk1HOW5TMFZKUTBGblNVTkVaMHBtVG1SbkVBReABAPoBBAgAEEk!16s%2Fg%2F11k4pkzztxentry=ttu&g_ep=EgoyMDI2MTAxMy4wIKXMDSoASAFQAw%3D%3D"}],
    "maxReviews": 20,
    "language": "id",
    "personalData": False,
})'''

rows = [
    {"nama_tempat": p.get("title"), "bintang": r.get("stars"), "review": r.get("text")} # No username
    for p in client.dataset(run.default_dataset_id).iterate_items()
    for r in p.get("reviews", [])
]
pd.DataFrame(rows).dropna(subset=["review"]).to_csv("reviews54.csv", index=False, encoding="utf-8-sig")
```

# **Scrapping berdasarkan search mencakup lebih dari 1 rs**

## ── Code cell 5 ──
```from apify_client import ApifyClient
import pandas as pd

client = ApifyClient("apify_api_.......")  # Console > Settings > Integrations

run_input = {
    "searchStringsArray": ["rumah sakit di batam"],
    "locationQuery": "Batam, Indonesia",
    "maxCrawledPlacesPerSearch": 10,
    "maxReviews": 10,
    "reviewsSort": "newest",
    "scrapeReviewsPersonalData": True,
    "language": "id",
}

run = client.actor("compass/crawler-google-places").call(run_input=run_input)
items = list(client.dataset(run.default_dataset_id).iterate_items())

rows = []
for place in items:
    for r in place.get("reviews") or []:
        rows.append({
            "nama_tempat": place.get("title"),
            "nama_user": r.get("name"),
            "bintang": r.get("stars"),
            "review": r.get("text"),
        })

df = pd.DataFrame(rows).dropna(subset=["review"]).drop_duplicates()
df.to_csv("reviews.csv", index=False, encoding="utf-8-sig")
print(df.shape)
```
