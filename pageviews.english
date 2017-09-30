'''
Goal: Collect pageviews for Zika virus page in English Wikipedia.
'''

import requests
import json
import requests
import csv

#Step 1: Write the ENDPOINT and parameters

ENDPOINT = 'https://wikimedia.org/api/rest_v1/metrics/pageviews/per-article/'

wp_code = 'en.wikipedia.org'
access = 'all-access'
agents = 'all-agents'
page_title = 'Zika virus'
period = 'daily'
start_date = '20091025'
end_date = '20160519'

wp_call = requests.get(ENDPOINT + wp_code + '/' + access + '/' + agents + '/' + page_title + '/' + period + '/' + start_date + '/' + end_date)
response = wp_call.json()

#Step 2: Create a list of dictionaries containing "date" : "pageviews"

pageviews = {}
	
for v in response['items']:
	date = v['timestamp'][4:6] + "-" + v['timestamp'][6:8] + "-" + v['timestamp'][0:4]
	if date in pageviews.keys():
		pageviews[date] += v['views']
	else:
		pageviews[date] = v['views']
#print (json.dumps(pageviews, indent=4))

#Step 3: Aggregate dates into months

monthly_pageviews = {}

for day_of_month in pageviews:
	month = day_of_month[0:2] + "-" + day_of_month[6:10]
	if month in monthly_pageviews:
		monthly_pageviews[month] += pageviews[day_of_month]
	else:
		monthly_pageviews[month] = pageviews[day_of_month]
print (json.dumps(monthly_pageviews, indent=4))

#Step 4: Iterate over the dictionary to extract and sort the keys, then append sorted keys to a new list

temp_list = list() 

for key in monthly_pageviews.keys():
	temp_list.append(key)
#print (temp_list)

temp_list.sort()
#print (temp_list)

result_list = list()

for key_sorted in temp_list:
	result_list.append(key_sorted)
print (json.dumps(result_list, indent=4))

#Step 5: Find month that had the most pageviews

top_month = []
max_pageviews = 0

for month in result_list:
	num_pageviews = monthly_pageviews[month]
	if num_pageviews > max_pageviews:
		max_pageviews = num_pageviews
		top_month = [month]
	elif num_pageviews == max_pageviews:
		top_month.append(month)
	else:
		pass
print ("The top month is", top_month, "with", max_pageviews, "pageviews")

#Step 6: Find total pageviews since inception of page

total_pageviews = 0

for p in monthly_pageviews.keys():
	total_pageviews += monthly_pageviews[p]
print ("Total pageviews since", result_list[0], ":", total_pageviews)

#Step 7: Write each sorted monthly pageview by rows in spreadsheet

fname = "zika_virus_pageviews_en4.csv"

fout = open(fname, "w")
fout.write("Month,Pageviews\n")
for m in result_list:
	string = m + "," + str(monthly_pageviews[m])
	print (string)
	fout.write(string + "\n")
fout.close()
