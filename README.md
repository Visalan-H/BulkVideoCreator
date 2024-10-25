# BulkVideoCreator
Created by Vizz

This project is a Python script that overlays text from a CSV file onto a background video.  
It’s a tool for automating video creation—because why do things manually when you can automate?  
        
Softwares only supported bulk creation when you had a premium subscription, so I built my own. 👍🏻
## Features
- Overlay text on your videos directly from CSV—quick and efficient, like a well-placed Batarang.
- Automates the generation of multiple videos in one go—because no one has time to do things one by one.
- Outputs videos to a designated folder, neatly organized, just like the Batcave.

## Requirements
- Python 3.x
- MoviePy
- Pandas
- FFMPEG (installed and in your system’s path—just like having all your gear ready)

Install the required libraries with:

```bash
pip install moviepy pandas
```
## The Program
```py
"""
BulkVideoCreator - A script for overlaying text on videos using MoviePy and Pandas.

License:
This project uses MoviePy, which is licensed under the MIT License. 
See the MoviePy GitHub repository for more details: https://github.com/Zulko/moviepy

Ensure any third-party assets used comply with their respective licenses.
"""
import pandas as pd
from moviepy.editor import VideoFileClip, TextClip, CompositeVideoClip
import os

# Paths
video_path = 'GIVE VIDEO PATH HERE (.mp4)'  # Path to your video file to be put in background
csv_path = 'GIVE CSV PATH HERE (.csv)'   # Path to your CSV file that has the texts to put in the video
output_folder = 'bulk_create/bulkoutput'          # Folder to save the output videos
font="GIVE FONT PATH HERE (C->WINDOWS->FONTS->SELECT FONT)"

# Coordinates for the text elements (adjusted for 9:16 aspect ratio)
title_position = ('center', 150)   # Center horizontally, 150px from the top
qn_position = ('center', 1200)     # Center horizontally, 1200px from the top
ans_position = ('center', 1450)    # Center horizontally, 1400px from the top

# Create output folder if it doesn't exist
if not os.path.exists(output_folder):
    os.makedirs(output_folder)

# Load pickup lines from CSV
df = pd.read_csv(csv_path)

# Load the video
video = VideoFileClip(video_path)

for index, row in df.iterrows():
    title = row['TITLE']
    pickup_line_qn = row['QUESTION']
    pickup_line_ans = row['ANSWER']
    
    #This is for the title text eg:"Art Rizz"
    title_clip = TextClip(title, fontsize=16, color='white',stroke_width=2, size=(500, None),font=font)
    title_clip = title_clip.set_position(title_position).set_duration(video.duration)
    
    #This is for the question text eg:"Are you an artist?"
    qn_clip = TextClip(pickup_line_qn, fontsize=58, color='white',stroke_width=1, size=(0.8*(video.size[0]), None),font=font,method='caption')
    qn_clip = qn_clip.set_position(qn_position).set_duration(video.duration)
    
    #This is for the answer text eg:"Because you've drawn me in."
    ans_clip = TextClip(pickup_line_ans, fontsize=58, color='white',stroke_width=1, size=(0.8*(video.size[0]), None),font=font,method='caption')
    ans_clip = ans_clip.set_position(ans_position).set_duration(video.duration)
    
    # Where all the texts and bg video gets merged
    video_with_text = CompositeVideoClip([video, title_clip, qn_clip, ans_clip])

    # Define the output file name
    output_file = os.path.join(output_folder, f"{index + 1}.mp4") #this numbers videos from 1 to n
    
    # Write the result video to a file
    video_with_text.write_videofile(output_file, codec='libx264', audio_codec='aac')

#end   
print("All videos have been processed and saved.")

```
## Results
### 50 days of posting 3-6 reels each day (didn't post on sep 27 phone broke :[ )
![image](https://github.com/user-attachments/assets/a2cfba52-d9d8-4973-bba8-04848d595cbc)
### Output folder
![image](https://github.com/user-attachments/assets/3dc4f4b7-607c-4ea3-9ac8-1b7d24b30420)
### Instagram Page
![image](https://github.com/user-attachments/assets/4ce1f580-01a1-4486-bf15-5d65ef4e1e3d)

### Here's the link to the page:[Click here!](https://www.instagram.com/rizz_cat._.daily/)

## PS 
I should say the pickup lines ChatGPT gave me were not up to the mark, but they work, I guess?<br>

Because here's what i got in my DM's:
 - Your rizz are really helpful 
 - How only 130 followers?This cat is fire
 - Bro I send my girl your reels everyday 😎 Keep it up
 - Hey 👋 I really like ur posts and those pickups lines are making me smile 😊

Also, we have one more page of motivational quotes and two more pages coming up. All automated coz I'm lazy.
Feel free to use it and spread the word—let’s make this resource available to all! ~Vizz

## Dependencies

This project uses the following libraries:

- [MoviePy](https://github.com/Zulko/moviepy): MIT License
- [Pandas](https://pandas.pydata.org/): MIT License

## License
This project is licensed under The MIT License—use it, enhance it, and remember to give credit where it's due. Check the LICENSE file for more details.

## Attributions
This script uses the MoviePy library, which is licensed under MIT. Make sure any fonts and media you use are properly licensed. After all, even the Joker would agree that it's best to stay on the right side of the law. Ensure any third-party assets comply with their respective licenses.

## Important Note on Dependencies
The MoviePy library is licensed under the MIT License. When using MoviePy or any other MIT-licensed code in your project, you must retain the original MIT license text and copyright notice intact. This ensures proper attribution and maintains compliance with the license terms.

## Disclaimer
This repository includes the code required to generate the videos. Any video files or other media used should be sourced and handled in accordance with copyright laws—because justice always prevails.
