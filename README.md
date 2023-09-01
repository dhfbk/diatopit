# DiatopIt: A Corpus of Social Media Posts for the Study of Diatopic Language Variation in Italy

This repository contains materials associated to the paper:

Alan Ramponi and Camilla Casula. 2023. **DiatopIt: A Corpus of Social Media Posts for the Study of Diatopic Language Variation in Italy**. In *Tenth Workshop on NLP for Similar Languages, Varieties and Dialects (VarDial 2023)*, pages 187–199, Dubrovnik, Croatia. Association for Computational Linguistics. [[cite]](#citation) [[paper]](https://aclanthology.org/2023.vardial-1.19/)


The dataset has recently been used in the context of the [GeoLingIt shared task](https://github.com/dhfbk/geolingit-evalita2023) at [EVALITA 2023](https://www.evalita.it/campaigns/evalita-2023/).


## Data

The corpus is released in the form of tweet IDs to be hydrated, in compliance to the Twitter developer policy. Data is in the `data/` folder and includes three files:

- `train.txt`: the training set, totalling 13,669 posts;
- `dev.txt`: the development set, totalling 552 posts;
- `test.txt`: the test set, totalling 818 posts.

The text of the post can be rehydrated from the [Tweet object](https://developer.twitter.com/en/docs/twitter-api/data-dictionary/object-model/tweet) of the Twitter json response. Just iterate over the posts (i.e., `for post in json_object["data"]`) and get the `post["text"]` content.

The location labels can be rehydrated from the [Place object](https://developer.twitter.com/en/docs/twitter-api/data-dictionary/object-model/place) of the Twitter json response. Just iterate over the places for the posts (i.e., `for place in json_object["includes"]["places"]`) and get the relevant information:
- **region**: `place["name"].split(", ")[1]`;
- **latitude**: `from_bbox_to_point(place["geo"]["bbox"])[0]`;
- **longitude**: `from_bbox_to_point(place["geo"]["bbox"])[1]`.

The `from_bbox_to_point()` function computes latitude and longitude coordinates by
taking the central point from the 4-point bounding box of city areas given by the Twitter APIs. It is defined as follows:

```python
def from_bbox_to_point(bbox):
    w_long, s_lat, e_long, n_lat = bbox
    latitude = (s_lat + n_lat) / 2
    longitude = (w_long + e_long) / 2
    return [latitude, longitude]
```

If you find any issues, please get in touch with us.


## Citation

If you use or build on top of this work, please cite our paper as follows:

```
@inproceedings{ramponi-casula-2023-diatopit,
    title = "{D}iatop{I}t: A Corpus of Social Media Posts for the Study of Diatopic Language Variation in {I}taly",
    author = "Ramponi, Alan  and
      Casula, Camilla",
    booktitle = "Tenth Workshop on NLP for Similar Languages, Varieties and Dialects (VarDial 2023)",
    month = may,
    year = "2023",
    address = "Dubrovnik, Croatia",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.vardial-1.19",
    pages = "187--199",
}
```
