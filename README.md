# localjson
analyse local json files
#!/usr/bin/env python
# -*- coding:utf-8 -*-

import json
import os
import sys
import pdb
import codecs
import urllib
import urllib.request
import urllib.parse
import zlib
import re
import logging

global counter
counter = 0
#...................................
global project_path
project_path = os.getcwd()
global data
global json_data

class Crawler:

	def _start(self):
		while counter < 251 :
			#reader = codecs.getreader('utf-8')
			#f = open(project_path +'\\notes.txt', 'rb', encoding = ('utf-8'))
			f = open(project_path + '/notesa.txt', 'rb')#, encoding = ('utf-8'))
			datastr = f.readline()
			data = datastr.decode('utf-8', errors = 'ignore')
			#data = f.read()
			#headers = {'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.100 Safari/537.36','Host':'openreview.net'}
			#url = r'https://openreview.net/notes?invitation=ICLR.cc%2F2017%2Fconference%2F-%2Fsubmission&maxtcdate=1480752222868'
			#url1 = r'https://openreview.net/group?id=ICLR.cc/2017/conference'
			#req1 = urllib.request.Request(url=url1, headers=headers)
			#req = urllib.request.Request(url=url, headers=headers)
			#page = urllib.request.urlopen(req)
			#data = page.read().decode('utf8')
			#data = re.sub(r"(,?)(\w+?)\s+?:", r"\1'\2' :", data);
			#data = data.replace("'", "\"");
			#logging.debug("after filter, respCmtJson=%s", data);
 
			json_data = json.loads(data, "utf-8");
			#logging.debug("json_data=%s", json_data);

			#json_data = json.loads(data)#reader(datastr))

			#pdb.set_trace()
			#print (data)
			#print (json['notes'])
			#strTxt.close()
			#pdb.set_trace()
			self._save(json_data)
			f.close()
		print('finish')
		return


	def _save(self,json):
		#for info in json_data.:
		#counter = len(os.listdir(project_path +'/ICLR/')) + 1
		for info in json["notes"]:
			#pdb.set_trace()
			#try:
				#if self._download(info) == False:
					#counter -= 1
			#except:
				#print('error!')
				#pass
			#else:
				#print('already got --' + str(counter) + 'papers')
				#counter += 1
			self._download(info)
			print('already got --' + str(counter) + 'papers')
			
		return


	def _download(self,info):
		global counter
		title = info['content']['title']
		#title = info['title']
		#print (title)
		abstract = info['content']['abstract']
		
		#print(abstract)
		s = open(project_path +'/titleabstract.txt', 'a+')
		counter += 1
		s.write(str(title) + '\n' )
		s.write(str(abstract) + '\n'+'\n')
		s.close()
#...................................
crawler = Crawler()
crawler._start()
