'''
Goal: Save a file of number of revisions per month for Zika virus page in Spanish Wikipedia.
'''

import requests
import json
import csv

#Step 1: Write the endpoints and parameters

ENDPOINT = 'https://es.wikipedia.org/w/api.php'

parameters = { 'action' : 'query',
               'prop' : 'revisions',
               'titles' : 'Virus_del_Zika',
               'format' : 'json',
               'rvprop' : 'user|timestamp',
               'rvdir' : 'newer',
               'rvlimit' : 500,
               'continue' : '' }

#Step 2: Aggregate number of revisions per day

days = {}

done = False
while not done:
	wp_call = requests.get(ENDPOINT, params=parameters)
	response = wp_call.json()

	pages = response['query']['pages']

	for page_id in pages:
		revisions = pages[page_id]["revisions"]
		for rev in revisions:
			revday = rev['timestamp'][0:10]
			if revday in days.keys():
				days[revday] += 1
			else:
				days[revday] = 1
		
	if 'continue' in response:
		parameters.update(response['continue'])
	else:
		done = True
#print(json.dumps(days, indent=4))

#Step 3: Aggregate dates into months

monthly_revisions = {}

for day in days:
	month = day[0:4] + "-" + day[5:7]
	if month in monthly_revisions:
		monthly_revisions[month] += days[day]
	else:
		monthly_revisions[month] = days[day]
print (json.dumps(monthly_revisions, indent=4))

#Step 4: Iterate over the dictionary to extract and sort the keys, then append sorted keys to a new list

temp_list = list() 

for key in monthly_revisions.keys():
	temp_list.append(key)
#print (temp_list)

temp_list.sort()
#print (temp_list)

result_list = list()

for key_sorted in temp_list:
	result_list.append(key_sorted)
print (json.dumps(result_list, indent=4))

#Step 5: Find month that had the most revisions

top_month = []
max_rev = 0

for month in result_list:
	num_rev = monthly_revisions[month]
	if num_rev > max_rev:
		max_rev = num_rev
		top_month = [month]
	elif num_rev == max_rev:
		top_month.append(month)
	else:
		pass
print ("The top month is", top_month, "with", max_rev, "revisions")

#Step 6: Find total revisions since inception of page

total_revisions = 0

for r in monthly_revisions.keys():
	total_revisions += monthly_revisions[r]
print ("Total revisions since", result_list[0], ":", total_revisions)

#Step 7: Save the data to a file

fname = "zika_virus_revisions_es4.csv"

fout = open(fname, "w")
fout.write("Month,Revisions\n")
for m in result_list:
	string = m + "," + str(monthly_revisions[m])
	print (string)
	fout.write(string + "\n")
fout.close()
