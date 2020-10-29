# MATLAB视频处理

```matlab
clc;
filepath=pwd;
video1=VideoReader('ch01.avi');
video2=VideoReader('ch03.avi');
videoWidth=video1.Width;
videoHeight=video2.Height;

k=1;
while hasFrame(video1)
    frame=readFrame(video1);
    frame_gray=rgb2gray(frame);
    frame_gray_new=adapthisteq(frame_gray);
    subplot(121);imshow(frame_gray_new);
    subplot(122);imshow(frame_gray);
    cd('image1\')
    imwrite(frame_gray,strcat(num2str(k,'%03d'),'.jpg'),'jpg');
    k=k+1;
    cd(filepath)
end

k=1;
while hasFrame(video2)
    frame=readFrame(video2);
    frame_gray=rgb2gray(frame);
   %%frame_gray_new=adapthisteq(frame_gray);
    %%imshow(frame_gray_new);
    cd('image2\')
    imwrite(frame_gray,strcat(num2str(k,'%03d'),'.jpg'),'jpg');
    k=k+1;
    cd(filepath)
end

%% 
new_video=VideoWriter('new1.avi','MPEG-4');
new_video.FrameRate=25;
open(new_video);
image1_Dir=dir(['image1\' '*.jpg']);
for i = 1:length(image1_Dir) % 遍历结构体就可以一一处理图片了
    img = imread(['image1\' image1_Dir(i).name]); %读取每张图片
    writeVideo(new_video,img);
end

%% %% 
new_video2=VideoWriter('new2.avi','MPEG-4');
new_video2.FrameRate=25;
open(new_video2);
image2_Dir=dir(['image2\' '*.jpg']);
for i = 1:length(image2_Dir) % 遍历结构体就可以一一处理图片了
    img = imread(['image2\' image2_Dir(i).name]); %读取每张图片
    writeVideo(new_video2,img);
end
```

