# Repurposing YouTube content for Linkedin and Instagram

<!-- META DATA
git-location: https://github.com/eviltester/talotics-videos.git
source-path: ffmpeg-video-repurposing/source.yml
-->

To re-promote my YouTube videos on Linkedin, Twitter and Instagram. I want to create smaller excerpts of my YouTube videos and have these send traffic to the main video on YouTube.

Short videos work well on Instagram, and Linkedin, when people scroll through their feed.

On mobile devices, videos auto play when shown in the feed.

But if you have a video with a talking head, people will see the talking head, but they won't hear the audio. And that just looks silly.

I could upload a subtitle file to Linkedin, but I'd have to edit that for the excerpt. Or, I can use hard captions, "burned in", to the video to avoid that problem.

I use ffmpeg to help with this. The software is free and runs from the command line. Although that can make it seem quite complicated.

`ffmpeg` is multi-platform free software that you can download from `https://www.ffmpeg.org/`.


Let me walk you through the workflow I use for taking a YouTube video, with subtitles, and converting it into smaller videos with burned in subtitles.

Here's a video on YouTube. It's only four minutes, but I can easily re-purpose this and get three or four short videos. I can then promote those shorter videos on Linkedin, Twitter and Instagram.

First I want to download the mp4 file.

And I want to download the subtitle file as a `.srt` file.

I'll use ffmpeg to generate a different format of subtitle file so I can burn it on to the video.

~~~~~~~~
ffmpeg -i captions.srt captions.ass
~~~~~~~~

And I'll burn it on to the video like this:

~~~~~~~~
ffmpeg -i video.mp4  -vf "subtitles=captions.ass:force_style='OutlineColour=&H80000000,BorderStyle=4,Outline=1,Shadow=0,MarginV=20'" subtitled-video.mp4
~~~~~~~~
 
I also want to create a video resized for Instagram. I can use the scale filter from `ffmpeg` to do that.

~~~~~~~~
ffmpeg -i video.mp4 -vf scale=720:720:force_original_aspect_ratio=decrease,pad=720:720 instagram-sized.mp4
~~~~~~~~

I can burn in the subtitles for this video as well.

~~~~~~~~
ffmpeg -i instagram-sized.mp4 -vf "subtitles=captions.ass:force_style='OutlineColour=&H80000000,BorderStyle=4,Outline=1,Shadow=0,MarginV=90'" instagram-subs.mp4
~~~~~~~~

Now I have a video which is perfect for uploading to Instagram. But it is too long. I need to cut it into smaller sections.

I want to create 3 new videos from my original. I watch the video to identify which sections I want. Each section starts from a point in the video and lasts for a specific length of time in seconds.

I've watched the video so I know I want sections from:

* from 01:05 for 52 seconds
* from 02:00 for 33 seconds
* from 03:10 for 51 seconds

I can use ffmpeg to create those sections.

~~~~~~~~
ffmpeg -i instagram-subs.mp4 -ss 00:01:05 -t 00:00:52 instagram-01-05.mp4
~~~~~~~~

That was for instagram, and now I have a fifty two second video, with subtitles, which is the right shape and length to upload to instagram.

Now I'll create one for linkedin. The only differences are the input file and output file name.

~~~~~~~~
ffmpeg -i subtitled-video.mp4 -ss 00:01:05 -t 00:00:52 subtitled-01-05.mp4
~~~~~~~~

If I repeat that for each of the segments, I'll have three videos that I can upload to Linkedin, and three that I can upload to Instagram. All will have subtitles visible on the screen.

It seems complicated, but if you copy and paste the commands and change the filenames and timings for your sections, you could easily be using Free software to repurpose your YouTube content on Linkedin, Instagram and other social networks.

And you can do this without having to do any more edits to the YouTube video or subtitles.

For more Digital Marketing Tactics, Tips and tricks. Visit www.talotics.com



