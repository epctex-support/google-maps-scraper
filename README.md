[https://apify.com/epctex/google-maps-scraper?fpr=yhdrb](https://apify.com/epctex/google-maps-scraper?fpr=yhdrb)

# Actor - Google Maps Scraper

## Google Maps Scraper

Since Google Maps doesn't provide a good and free API, this actor should help you to retrieve data from it.

The Google Maps data scraper supports the following features:

- Search by keyword - Discover places that match your interests effortlessly with our advanced Google Maps scraper. Simply input your desired keywords, and let our tool gather a curated list of places that cater to your preferences.

- Search by location - Explore any area virtually using our Google Maps scraper. Whether you're planning a trip or researching a neighborhood, just provide the location, and our scraper will compile a comprehensive list of establishments in that area for your convenience.

- Fetch reviews of any place - Access a wealth of user experiences by extracting reviews through our Google Maps scraper. Uncover valuable insights about various places before you visit, helping you make informed decisions based on the collective opinions of other customers.

- Fetch information of reviewers - Get a deeper understanding of places by accessing reviewer information through our Google Maps scraper. From profile details to reviewing history, gather the context you need to evaluate the credibility and relevance of reviews.

- Sort reviews and retrieve all - Take control of review sorting with our Google Maps scraper. Whether you want the most recent opinions or the highest-rated feedback, our tool lets you customize how you view and analyze reviews according to your preferences. Access all the reviews you need in one go.



## Bugs, fixes, updates, and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/google-maps-scraper/issues).


## Input Parameters

The input of this scraper should be JSON containing the list of pages on Google Maps that should be visited. Possible fields are:

- `startUrls`: (Optional) (Array) List of Google Maps URLs. It should be a search,or place detail URL.

- `search`: (Optional) (String) Keyword you would like to search on the Google Maps. Required if `startUrls` is not provided.

- `searchLocation`: (Optional) (String) Location that you would like to search on Google Maps. The location should be explicitly defined so that the Google Maps Scraper can retrieve it for you. Required if `startUrls` is not provided.

- `language`: (Optional) (String) Language of the results. Some of the fields on the Google Maps are being supported by language option. Required if `startUrls` is not provided.

- `includeReviews`: (Optional) (Boolean) Enables the actor to retrieve reviews per each place.

- `reviewsSort`: (Optional) (String) Sorting option for the reviews. This can be only used whenever `includeReviews` is enabled.

- `includeReviewerInformation`: (Optional) (Boolean) This option enables fetching of the reviewer information per each review. This can be only used whenever `includeReviews` is enabled.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `maxReviews`: (Optional) (Number) You can limit scraped reviews per place. This should be useful when you search through the places where it contains a lot of reviews.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as an argument and returns an object with data.

- `customMapFunction`: (Optional) (String) Function that takes each object's handle as an argument and returns an object with executing the function.

This solution requires using **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Compute Unit Consumption

The actor is optimized to run blazing fast and scrape many as listings as possible. Therefore, it forefronts all listing detail requests. If the actor doesn't block very often it'll scrape 100 listings in 2 minutes with ~0.3-0.5 compute units.

### Google Maps Scraper Input example

```json
{
  "startUrls":[
      "https://www.google.com/maps/search/cafe/@40.6976437,-74.3093257,10z/data=!3m1!4b1?authuser=0&hl=en&entry=ttu",
      "https://www.google.com/maps/place/The+Museum+of+Modern+Art/@40.7614367,-73.9801965,17z/data=!3m2!4b1!5s0x89c258fbd5ec7547:0x7edf0a3ade84ad50!4m6!3m5!1s0x89c258f97bdb102b:0xea9f8fc0b3ffff55!8m2!3d40.7614327!4d-73.9776216!16zL20vMGhoams?authuser=0&hl=en&entry=ttu"
  ],
  "search":"cafe",
  "searchLocation": "San Francisco, USA",
  "maxItems":100,
  "includeReviews":true,
  "includeReviewerInformation":true,
  "reviewsSort":"newest",
  "language":"en",
  "maxReviews":20,
  "customMapFunction": "(object) => { return {...object} }",
  "extendOutputFunction": "($) => { return {} }",
  "proxy":{
    "useApifyProxy": true
  }
}


```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Google Maps Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Google Maps actor.

## Scraped Google Maps Output

The structure of each item in Google Maps looks like this:

```json
{
	"url": "https://www.google.com/maps/place/Good+Thanks+Cafe/data=!4m7!3m6!1s0x89c259a31b639d95:0x90a673b3e3ed8540!8m2!3d40.7197434!4d-73.9895105!16s%2Fg%2F11ghtdlp63!19sChIJlZ1jG6NZwokRQIXt47NzppA?authuser=0&hl=en&rclk=1",
	"title": "Good Thanks Cafe",
	"description": "Breakfast, lunch and brunch enthusiasts. Hip neighbourhood cafe serving our In-house roasted coffee, natural wine, thoughtful food dishes. Come as you are.",
	"address": "Good Thanks Cafe, 131a Orchard St, New York, NY 10002, United States",
	"neighborhood": "Manhattan",
	"street": "131a Orchard St",
	"district": "New York",
	"postalCode": "10002",
	"city": "New York",
	"countryCode": "US",
	"location": {
		"lat": 40.7197434,
		"lng": -73.9895105
	},
	"menu": "https://www.goodthanksnyc.com/menu",
	"website": "http://goodthanksnyc.com/",
	"phone": "+1 646-370-4426",
	"phoneUnformatted": "+16463704426",
	"plusCode": "P296+V5 New York, USA",
	"price": "$$",
	"totalScore": 4.7,
	"cid": "-8023598469653625536",
	"reviewsCount": 526,
	"reviewsDistribution": {
		"oneStar": 8,
		"twoStar": 13,
		"threeStar": 24,
		"fourStar": 61,
		"fiveStar": 420
	},
	"categories": [
		"Cafe",
		"Australian restaurant",
		"Breakfast restaurant",
		"Cocktail bar",
		"Restaurant",
		"Wine bar"
	],
	"imagesCount": 826,
	"openingHours": [
		{
			"day": "Thursday",
			"hours": "8 AM–3 PM"
		},
		{
			"day": "Friday",
			"hours": "8 AM–3 PM"
		},
		{
			"day": "Saturday",
			"hours": "8:30 AM–4 PM"
		},
		{
			"day": "Sunday",
			"hours": "8:30 AM–4 PM"
		},
		{
			"day": "Monday",
			"hours": "8 AM–3 PM"
		},
		{
			"day": "Tuesday",
			"hours": "8 AM–3 PM"
		},
		{
			"day": "Wednesday",
			"hours": "8 AM–3 PM"
		}
	],
	"peopleAlsoSearch": [
		{
			"title": "Dudley's",
			"totalScore": 4.5,
			"reviewsCount": 1126
		},
		{
			"title": "Sonnyboy",
			"totalScore": 4.7,
			"reviewsCount": 347
		},
		{
			"title": "Russ & Daughters Cafe",
			"totalScore": 4.6,
			"reviewsCount": 2845
		},
		{
			"title": "Two Hands",
			"totalScore": 4.3,
			"reviewsCount": 794
		},
		{
			"title": "Sunday to Sunday",
			"totalScore": 4.2,
			"reviewsCount": 190
		}
	],
	"reviewTags": [
		{
			"title": "brunch",
			"count": 57
		},
		{
			"title": "kimchi scramble",
			"count": 33
		},
		{
			"title": "avocado toast",
			"count": 23
		},
		{
			"title": "scrambled eggs",
			"count": 23
		},
		{
			"title": "acai bowl",
			"count": 18
		},
		{
			"title": "server",
			"count": 13
		},
		{
			"title": "breakfast sandwich",
			"count": 11
		},
		{
			"title": "sourdough",
			"count": 8
		},
		{
			"title": "plate",
			"count": 8
		},
		{
			"title": "ingredients",
			"count": 6
		}
	],
	"additionalInfo": {
		"Service options": [
			{
				"Outdoor seating": true
			},
			{
				"Kerbside pickup": true
			},
			{
				"Delivery": true
			},
			{
				"Takeaway": true
			},
			{
				"Dine-in": true
			}
		],
		"Highlights": [
			{
				"Fast service": true
			},
			{
				"Great coffee": true
			},
			{
				"Great tea selection": true
			}
		],
		"Popular for": [
			{
				"Breakfast": true
			},
			{
				"Lunch": true
			},
			{
				"Solo dining": true
			}
		],
		"Accessibility": [
			{
				"Wheelchair-accessible entrance": true
			},
			{
				"Wheelchair-accessible seating": true
			},
			{
				"Wheelchair-accessible toilet": true
			},
			{
				"Wheelchair-accessible car park": false
			}
		],
		"Offerings": [
			{
				"Alcohol": true
			},
			{
				"Beer": true
			},
			{
				"Cocktails": true
			},
			{
				"Coffee": true
			},
			{
				"Comfort food": true
			},
			{
				"Healthy options": true
			},
			{
				"Organic dishes": true
			},
			{
				"Quick bite": true
			},
			{
				"Vegetarian options": true
			},
			{
				"Wine": true
			}
		],
		"Dining options": [
			{
				"Breakfast": true
			},
			{
				"Brunch": true
			},
			{
				"Lunch": true
			},
			{
				"Dessert": true
			},
			{
				"Seating": true
			}
		],
		"Amenities": [
			{
				"Toilets": true
			}
		],
		"Atmosphere": [
			{
				"Casual": true
			},
			{
				"Cosy": true
			},
			{
				"Trendy": true
			}
		],
		"Crowd": [
			{
				"LGBTQ+ friendly": true
			},
			{
				"Tourists": true
			}
		],
		"Payments": [
			{
				"Credit cards": true
			},
			{
				"Debit cards": true
			},
			{
				"NFC mobile payments": true
			},
			{
				"Credit cards": true
			}
		],
		"Children": [
			{
				"Good for kids": true
			}
		]
	},
	"updatesFromCustomers": [
		{
			"id": "ChdDSUhNMG9nS0VJQ0FnSUNHdjVicG9RRRAB",
			"text": "Love the kimchi eggs and gluten free banana bread with the salted honey butter",
			"date": 1636873217610677,
			"reviewer": {
				"id": "109178936832129224577",
				"name": "Ido Simyoni",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMTk9UpxTs7dZ06MrGTQss1YkOWYRuNyIZHSnaO9Xb2LaXU=s120-c-rp-mo-ba7-br100",
				"url": "https://www.google.com/maps/contrib/109178936832129224577?hl=en-US",
				"totalReviews": 832,
				"totalPhotos": 5793
			},
			"language": "en",
			"photos": [
				"https://lh5.googleusercontent.com/p/AF1QipMvyIeK9c--VetTk429H2jrCc4UM_D88QfQW2Za"
			]
		}
	],
	"reviews": [
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSURwX3NLakhnEAE",
			"text": "Magnifique découverte !\nTout est absolument délicieux\nLe personnel et super gentil !\nNous nous sommes régaler et le cadre et super jolie .",
			"stars": 5,
			"date": 1692742849770,
			"reviewer": {
				"id": "115795399366627873984",
				"name": "Lesia Janisson Lovichi",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMQw6rrUlKWc4-w3OJoIlGJqa-J56GqRYZ_AyHBdLO9-Np8=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/115795399366627873984?hl=en-US",
				"totalReviews": 3,
				"totalPhotos": 3
			},
			"language": "fr",
			"details": [
				{
					"Meal type": "Brunch"
				},
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSURwdHJUNUp3EAE",
			"text": "Good Thanks Cafe is a hidden gem! Cozy atmosphere, friendly staff, and delicious coffee. A perfect spot to unwind. Highly recommend!\"",
			"stars": 5,
			"date": 1692635208029,
			"reviewer": {
				"id": "116138585131810873629",
				"name": "Ehsan Ali",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMTa5CCrQX7aCBFS-4GxmghGLe0DDmA8sZbTLyhVeYWBjlU=s120-c-rp-mo-ba4-br100",
				"url": "https://www.google.com/maps/contrib/116138585131810873629?hl=en-US",
				"totalReviews": 49,
				"totalPhotos": 60
			},
			"language": "en",
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSURwdXR2dUlREAE",
			"text": "Cool, good,\nSuper café et très Boone cuisine\nJe recommande cette adresse 👍",
			"stars": 5,
			"date": 1692544649684,
			"reviewer": {
				"id": "107849700411735755439",
				"name": "sebastien rastel",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtdD6q02i9_DdfaGkfSg99MVs-O2Vq9yYvcQsgXtUvGR=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/107849700411735755439?hl=en-US",
				"totalReviews": 1,
				"totalPhotos": 0
			},
			"language": "fr",
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChdDSUhNMG9nS0VJQ0FnSURwNUtYSDZRRRAB",
			"text": null,
			"stars": 3,
			"date": 1692198926391,
			"reviewer": {
				"id": "116629757117601619229",
				"name": "AI LINH Duong",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtfnpP-pxG0M0bIlGNTzocHP1UlUdus6oJpAEIHZv3Sj=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/116629757117601619229?hl=en-US",
				"totalReviews": 0,
				"totalPhotos": 0
			},
			"language": null,
			"details": [
				{
					"Food": 3
				},
				{
					"Service": 2
				},
				{
					"Atmosphere": 3
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSUNwNThMcldREAE",
			"text": null,
			"stars": 5,
			"date": 1691789412904,
			"reviewer": {
				"id": "109000545884843875553",
				"name": "Alexander Guggenberger",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtfnFMQf2sWPCxcgoxOXwfmLztmPGdcr3Ny4hMKRHery=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/109000545884843875553?hl=en-US",
				"totalReviews": 2,
				"totalPhotos": 0
			},
			"language": null,
			"details": [
				{
					"Service": "Dine in"
				},
				{
					"Meal type": "Breakfast"
				},
				{
					"Price per person": "$10–20"
				},
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				},
				{
					"Recommended dishes": "Kimchi Scrambled Eggs on Sourdough"
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChdDSUhNMG9nS0VJQ0FnSUNwN1lLMnhnRRAB",
			"text": "Such nice place for a quick lunch, brunch. healthy and tasty. Will Recommend to my friends and family.",
			"stars": 5,
			"date": 1691505342362,
			"reviewer": {
				"id": "106294703376144109512",
				"name": "Sholpan Sultanbekov",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMScKaFXB02pacJIbxxVv9qPZWP-dF9X07yHQtwc0X8Rv7E=s120-c-rp-mo-ba2-br100",
				"url": "https://www.google.com/maps/contrib/106294703376144109512?hl=en-US",
				"totalReviews": 15,
				"totalPhotos": 22
			},
			"language": "en",
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 4
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSUNwbWZxc1RnEAE",
			"text": "My favourite breakfast in NY, great eggs and bread.",
			"stars": 5,
			"date": 1691330547935,
			"reviewer": {
				"id": "104671033762646916163",
				"name": "James Kachan",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMTw2kfXN8esqAyEqhvH-iAXLdM2F-nbopdYpq0c_k1v72bE=s120-c-rp-mo-ba3-br100",
				"url": "https://www.google.com/maps/contrib/104671033762646916163?hl=en-US",
				"totalReviews": 52,
				"totalPhotos": 24
			},
			"language": "en",
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChdDSUhNMG9nS0VJQ0FnSUNwa3JhbHhnRRAB",
			"text": "New favorite! friendly staff! inviting and calm atmosphere. Great espresso and sourdough. I can’t wait to try the bigger plates next time",
			"stars": 5,
			"date": 1690828884145,
			"reviewer": {
				"id": "112139727141545012977",
				"name": "LP",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtcXq--qfHQQ2BlA9J6GuTpoYDOkTPZEl_zJM0BitIsQuw=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/112139727141545012977?hl=en-US",
				"totalReviews": 6,
				"totalPhotos": 4
			},
			"language": "en",
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChdDSUhNMG9nS0VJQ0FnSUNwdk5lR3VRRRAB",
			"text": null,
			"stars": 5,
			"date": 1690758188852,
			"reviewer": {
				"id": "106753444063603884174",
				"name": "Angela L",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTteYZvTtmjYAuk93CqLwoCp2DyeiVYT71N_bS6YeVvTD=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/106753444063603884174?hl=en-US",
				"totalReviews": 10,
				"totalPhotos": 0
			},
			"language": null,
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSURKdFlPZUZnEAE",
			"text": "We had a wonderful breakfast with Blue Bowl and Avocado Toast. We loved the vibe. Highly recommended.",
			"stars": 5,
			"date": 1689947646582,
			"reviewer": {
				"id": "104737142602731694420",
				"name": "Sveinung Rindal",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtewPo2TSQTIWmuXIAOAAESgdDNAgQIAZ04z7I79FvY5=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/104737142602731694420?hl=en-US",
				"totalReviews": 11,
				"totalPhotos": 3
			},
			"language": "en",
			"photos": [
				"https://lh5.googleusercontent.com/p/AF1QipNmTPS2AWrXsk_mup3SsTqs_SXILBQ4SwCieibL",
				"https://lh5.googleusercontent.com/p/AF1QipMd7SiaaonCznFMZUvKzGDw36hs1BHSVxecpWLY"
			],
			"details": [
				{
					"Service": "Dine in"
				},
				{
					"Meal type": "Breakfast"
				},
				{
					"Price per person": "$20–30"
				},
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSURKNGZYTFV3EAE",
			"text": "האוכל מאוד טעים והאווירה טובה. השירות גרוע ביותר, המלצריות לא נחמדות ועושות ״טובה״ שהן נותנות שירות. יש הרגשה לא טובה מהמלצריות.",
			"stars": 2,
			"date": 1689697450640,
			"reviewer": {
				"id": "103673992798261205615",
				"name": "יובל קוטלובסקי",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtedkCRjFYJHobvMFLjKKWPOr56eUXylkACXBRDJpara=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/103673992798261205615?hl=en-US",
				"totalReviews": 2,
				"totalPhotos": 0
			},
			"language": "iw",
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 1
				},
				{
					"Atmosphere": 3
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChdDSUhNMG9nS0VJQ0FnSURKNk1pVzRnRRAB",
			"text": "This place is great the food is delicious with fresh ingredients that are paired very well. I love the sourdough bread and the coffee is wonderful.",
			"stars": 5,
			"date": 1688964236697,
			"reviewer": {
				"id": "111068659621609496542",
				"name": "Afomeya Habtamu",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtfRvglzV-gBMAM9UrJfk1xRfHGHf_u4K1xfmyoCxGCY=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/111068659621609496542?hl=en-US",
				"totalReviews": 15,
				"totalPhotos": 1
			},
			"language": "en",
			"photos": [
				"https://lh5.googleusercontent.com/p/AF1QipNMSnshKekUdQTzCg2SKTeUjxDVRH_xAvRy9UMQ"
			],
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSURKOFBxTmNREAE",
			"text": "coffee and blue bowl mediocre for me. sour fruits and burnt coffee taste linger in my mouth an hour later",
			"stars": 1,
			"date": 1688913637247,
			"reviewer": {
				"id": "105181137186970702514",
				"name": "Nicolas Romer",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMQhw8dw59uqrfYu4hZ-UNN6tZJmNTWx65GAEqSO2feVh6c=s120-c-rp-mo-ba2-br100",
				"url": "https://www.google.com/maps/contrib/105181137186970702514?hl=en-US",
				"totalReviews": 22,
				"totalPhotos": 3
			},
			"language": "en",
			"details": [
				{
					"Service": "Dine in"
				},
				{
					"Meal type": "Breakfast"
				},
				{
					"Price per person": "$20–30"
				}
			],
			"ownersResponse": {
				"text": "Well that’s very rude ",
				"textTranslated": null,
				"date": 1688914281417,
				"language": "en"
			}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSURKZ0ozVmRnEAE",
			"text": null,
			"stars": 4,
			"date": 1688827775157,
			"reviewer": {
				"id": "109049049249992749394",
				"name": "סיגל רון",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMTOKF_X5PahbuyEHFJwz1zGKUqEW26MTyNkXvtYZ2SIBshX=s120-c-rp-mo-ba5-br100",
				"url": "https://www.google.com/maps/contrib/109049049249992749394?hl=en-US",
				"totalReviews": 278,
				"totalPhotos": 1471
			},
			"language": null,
			"ownersResponse": {}
		},
		{
			"id": "ChdDSUhNMG9nS0VJQ0FnSURKZ0thVjRnRRAB",
			"text": "A really cute cafe to grab breakfast and a coffee. The food is delicious and the atmosphere is great! I’ve lived in the lower east side for a few years now and this is certainly one of my favorite spots.",
			"stars": 5,
			"date": 1688824387984,
			"reviewer": {
				"id": "102228148806775842096",
				"name": "Abbigail Coe",
				"photo": "https://lh3.googleusercontent.com/a/AAcHTtfWaJgYtLyzn-K6o0fK1V-MXxEmLINrsf8H-k5zdGoTgQ=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/102228148806775842096?hl=en-US",
				"totalReviews": 11,
				"totalPhotos": 0
			},
			"language": "en",
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSUNKel9PRUZ3EAE",
			"text": "Cute little breakfast spot with great art and music. The plates are fresh and beautiful to look at. We loved our coffee and matcha.",
			"stars": 4,
			"date": 1688738184937,
			"reviewer": {
				"id": "109140661329831645288",
				"name": "Camille Théophile",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMRz12HVm7z6jKsG0X4W7cQ3WqXwdMnZ2OwUoirZCFNHWVNx=s120-c-rp-mo-ba5-br100",
				"url": "https://www.google.com/maps/contrib/109140661329831645288?hl=en-US",
				"totalReviews": 238,
				"totalPhotos": 435
			},
			"language": "en",
			"photos": [
				"https://lh5.googleusercontent.com/p/AF1QipO9hbkaRYNXV8ahZiG84qEEU5chfPNlV-RtIDZ6"
			],
			"details": [
				{
					"Service": "Dine in"
				},
				{
					"Meal type": "Breakfast"
				},
				{
					"Food": 4
				},
				{
					"Service": 4
				},
				{
					"Atmosphere": 5
				},
				{
					"Recommended dishes": "Acai Bowl and Avocado Toast"
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSUNKOF9iRk1BEAE",
			"text": "Food was great! Delicious with a good amount of options and variety! A great small cafe in LES to make a regular breakfast spot! Service was decent. The Environment and food is def the best part tho!",
			"stars": 5,
			"date": 1688490112328,
			"reviewer": {
				"id": "103647725412499019041",
				"name": "Owen Murphy",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMTtwTy8aMtmm-xTohNbQWsHc6aE588Rm1l9yVPzxtL9vs1b=s120-c-rp-mo-ba4-br100",
				"url": "https://www.google.com/maps/contrib/103647725412499019041?hl=en-US",
				"totalReviews": 38,
				"totalPhotos": 164
			},
			"language": "en",
			"details": [
				{
					"Service": "Dine in"
				},
				{
					"Meal type": "Breakfast"
				},
				{
					"Price per person": "$20–30"
				},
				{
					"Food": 5
				},
				{
					"Service": 4
				},
				{
					"Atmosphere": 5
				},
				{
					"Recommended dishes": "Curry Scramble"
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSUNKcllUdEZ3EAE",
			"text": "Hands down one of the best brunches in NYC. The faro bowl was immaculate. Filled me up with joy the whole day. Staff is so nice too! 10/10",
			"stars": 5,
			"date": 1688314987738,
			"reviewer": {
				"id": "105791649907686447987",
				"name": "ELL",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMTdu6dzUf93I8TmnetI0MOf922T6-WaO94gZqm7ce0Oj8M=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/105791649907686447987?hl=en-US",
				"totalReviews": 9,
				"totalPhotos": 4
			},
			"language": "en",
			"photos": [
				"https://lh5.googleusercontent.com/p/AF1QipO3hkUYaltsWaRSSQnsC2jge1iLllzu5oDRxgDg"
			],
			"details": [
				{
					"Service": "Take out"
				},
				{
					"Meal type": "Brunch"
				},
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSUNKbnVLdkN3EAE",
			"text": "Love",
			"stars": 5,
			"date": 1687894675304,
			"reviewer": {
				"id": "115398655128381145221",
				"name": "Chris Coulthrust",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMQsYGSFj3yx0S86sG7Ysr4RIR5n5Oz9SF7S6GLZwcWFgKc=s120-c-rp-mo-ba5-br100",
				"url": "https://www.google.com/maps/contrib/115398655128381145221?hl=en-US",
				"totalReviews": 433,
				"totalPhotos": 639
			},
			"language": "en",
			"details": [
				{
					"Service": "Dine in"
				},
				{
					"Meal type": "Brunch"
				},
				{
					"Price per person": "$30–50"
				},
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		},
		{
			"id": "ChZDSUhNMG9nS0VJQ0FnSUNKcnRtU2RREAE",
			"text": null,
			"stars": 5,
			"date": 1687875807398,
			"reviewer": {
				"id": "116928773395785373846",
				"name": "Catalina Echeverri",
				"photo": "https://lh3.googleusercontent.com/a-/AD_cMMRcJjMi_4_v0SJvBiqdkSVqPE_B8cKXVDX1z4o_MpUSwcg=s120-c-rp-mo-br100",
				"url": "https://www.google.com/maps/contrib/116928773395785373846?hl=en-US",
				"totalReviews": 10,
				"totalPhotos": 0
			},
			"language": null,
			"details": [
				{
					"Food": 5
				},
				{
					"Service": 5
				},
				{
					"Atmosphere": 5
				}
			],
			"ownersResponse": {}
		}
	]
}
```

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that are available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.
