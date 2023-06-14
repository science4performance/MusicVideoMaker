# MusicVideoMaker
 A Stable Diffusion generative AI pipeline to create music videos from song lyrics
 
 Sample videos here https://www.youtube.com/channel/UCyE1DTRfUNzJ_WH3RTHw-XA
 
 For more details check out my blog https://science4performance.com/2023/06/14/generating-music-videos-using-stable-diffusion/
 
 In order to produce an effective music video, I needed the images to change in time with the lyrics. Rather than messing around editing my Python code, I ended up using a Excel template spreadsheet as a convenient way to enter the lyrics alongside the time in the track. It was useful to enter "text" as a negative prompt and a particular colour stop it dominating the output. By default an overall style is added to each prompt, but it is convenient to change the style on certain prompts. By default the initial image is used as a "shadow", which contributes 1% to every subsequent frame, in an attempt to retain an overall theme. This can also be overridden on each prompt. 

Finally, it was very useful to be able to define target images. If defined for the initial image, this saves loading an additional Stable Diffusion text-to-image pipeline to create the first frame.  Defining a target image for a particular prompt drags the animation towards the target, by mixing increasing proportions of the target with the current image, starting at the previous prompt. This is also useful for the final frame of the animation. One way to create target images is to run a few prompts through Stable Diffusion here.

Although some lyrics explicitly mention objects that Stable Diffusion can illustrate, I found it helps to focus on specific key words. This is my template for "No more heroes" by The Stranglers. It produced an awesome video.

Once an Excel template is complete, the following pipeline generates the key frames by looping through each prompt and calculating how many frames are required to fill the time until the next prompt for the desired seconds per frame. A basic GPU takes about 3 seconds per key frame, so a song takes about 10-20 minutes, including inserting a smoothing steps between the key frames.  


