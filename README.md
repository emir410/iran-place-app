# iran-place-app
app android
import requests
import json

def get_places(place_type):
    url = "https://api.foursquare.com/v2/venues/explore"
    params = {
        "near": "Iran",
        "radius": "20000",
        "section": place_type,
        "client_id": "YOUR_CLIENT_ID",
        "client_secret": "YOUR_CLIENT_SECRET",
        "v": "20220308"
    }
    response = requests.get(url, params=params)
    places = json.loads(response.text)["response"]["groups"][0]["items"]
    return places

def display_places(place_type):
    places = get_places(place_type)
    print("در حال جستجوی مکان‌های دیدنی...")
    for i, place in enumerate(places):
        name = place["venue"]["name"]
        address = place["venue"]["location"]["address"]
        rating = place["venue"]["rating"]
        print(f"{i+1}. نام: {name}")
        print(f"آدرس: {address}")
        print(f"امتیاز: {rating}")
        print("--------------------------------------")

# استفاده از برنامه
place_type = input("لطفا نوع مکان دیدنی را وارد کنید (مثلاً رستوران، موزه، پارک و غیره): ")
display_places(place_type)
