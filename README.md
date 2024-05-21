# Repo# Repo[# Repo](https://github.com/Warxone/Repo.git)
Here's a more complete version of the code:
```
import pywhatkit as whatsapp
import requests
from bs4 import BeautifulSoup

# Connect to WhatsApp Web
whatsapp.connect()

# Get the messages
messages = whatsapp.get_messages()

# Create a folder to store the downloaded media
import os
media_folder = "downloaded_media"
if not os.path.exists(media_folder):
	os.makedirs(media_folder)

# Loop through the messages
for message in messages:
	# Check if the message has media
	if message.has_media:
		# Download the media
		media_url = message.media_url
		response = requests.get(media_url)
		
		# Get the file name from the media URL
		file_name = media_url.split("/")[-1]
		
		# Save the media to the folder
		with open(os.path.join(media_folder, file_name), "wb") as file:
			file.write(response.content)
		
		print(f"Downloaded {file_name}")
