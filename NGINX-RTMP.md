#NGINX-RTMP

While working on a side project, we noticed that the NGINX-RTMP module that allows incoming RTMP video streams (via FFMPEG) was absolutely hammering all 8 CPUs of the AWS EC2 M4.2XLARGE instance we were testing on. After looking at the documentation we found that FFMPEG has some pretty handy baked-in optimization arguments. **-tune** to the rescue:

  **... -tune superfast...**
  
  Provides a more stable video but marginally reduced quality. After adding the argument to our FFMPEG command we noticed a performance increase from 100% CPU usage to hovering around 30% CPU usage while streaming 1080 60fps. 
