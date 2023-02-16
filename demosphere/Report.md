# Programming project : Analyzing data from protests in the area of Paris

## Collecting the data

The firts step was to collect the necessary data. We choose to retrieve this data from paris.demosphère.net .We used Beautiful soup to retrieve the data which was in json format and then convert it inot the python data type.

```bash
#get every event from january 2012 to march 2023
L=[]
for month in months[1:3]:
  print(month)
  start = f"{base}{month}"
  print(start)
  days = get_days(start)
  for day in days:
    try: 
      res = requests.get(f"{base}{day}")
      soup = BeautifulSoup(res.text,'html.parser')
      events = soup.find('script', {'type': 'application/ld+json'})
      data = json.loads(events.text)
      L.append(data)
    except Exception as err:
      print(err)

len(L)
```

The data we obtain for each event can be presented like this : 

| @context                 | @type   |Name                                               | url                                     | startDate         | endDate    | location                                          | description |
| :----                    | :----   | :----                                             | :----                                   |:----              | :----      | :----                                             | :----        |                
| `http://www.schema.org`  | `Event` | 'Réunion des Indignés- Groupe de travail Const...'| 'https://paris.demosphere.net/rv/19667' | '2012-01-02T19:00'|'2012-01-02'|'{'@type': 'Place', 'name': 'Devant le café « L...'| 'Groupe de travail Constituante\n\nIndignés - D...' |


## Let's look at the weekly patterns

With the python notebook Weekday.ipynb, we looked at the weekly patterns for each month of the year 2012.

![Weekly pattern january](/demosphere/jan2012.png)

![Weekly pattern february](/demosphere/feb2012.png)




