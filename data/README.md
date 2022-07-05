- 190K medium articles -- <https://www.kaggle.com/datasets/fabiochiusano/medium-articles>
- Spanish emoji classification prediction task -- 50k tweets labeled as one of 64 emojis -- <https://github.com/sadit/TextClassificationTutorial/blob/main/data/emo50k.json.gz> 
- Spanish news in twitter -- ~42k tweets from journals and journalists collected from mid 2021 - mid 2022 in Twitter public stream
```
DATA = [JSON.parse(line) for line in eachline("../data/news.json")]

D = DataFrame(id=Int[], screen_name=String[], timestamp_ms=Int[], text=String[])
for d in DATA
    id, screen_name, timestamp_ms = d["id"], d["user"]["screen_name"], parse(Int, d["timestamp_ms"])
    x = get(d, "extended_tweet", nothing)
    text = x === nothing ? d["text"] : x["full_text"]
    push!(D, (id, screen_name, timestamp_ms, base64encode(text)))
end

CSV.write("../data/spanish-news-in-twitter.csv", D; delim=',')
```