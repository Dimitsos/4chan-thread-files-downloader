from os import makedirs, chdir, startfile
from urllib.request import URLopener, urlopen
from re import finditer
from os.path import expanduser

link = input("Copy paste the link of the thread: ")
request = "https://a.4cdn.org" + link[link.find("org")+3:] + ".json"
response = str(urlopen(request).read())
board = request[request.find("org")+3:request.rfind("/")-6]

id_list = [response[e.end()+1:e.end()+14] for e in finditer('"tim"', response)]

ext_list = [(response[s.end()+2:e.start()-2]) for s,e in zip(finditer('"ext"', response), finditer('"w"', response))]

img_list = ["https://i.4cdn.org" + board + ID + EXT for ID, EXT in zip(id_list, ext_list)]


download_dir = expanduser("~") + "\Downloads\\"
new_folder_name = input("Name the new folder: ")
download_folder = download_dir + new_folder_name
makedirs(download_folder)
chdir(download_folder)

print(len(id_list), "files")

for img, ids, ext in zip(img_list, id_list, ext_list):
	URLopener().retrieve(img, ids+ext)

startfile(download_folder)
