# the-Note-Making-Project

Implemented Optical Character Recognition using MATLAB as part of the Note Making Project.

<p align="center">
  <img src="https://github.com/UjwalKandi/Note-Making-Project/blob/main/img/output.jpg" style='height: 40%; width: 95%; object-fit: contain'/>
</p>

``` python
  clc
  Inputimage=imread("/MATLAB Drive/caution.jpg");
  figure(1)
  imshow(Inputimage);
  title('INPUT IMAGE WITH NOISE')
```  
<br/>
<p align="center">
  <img src="https://github.com/UjwalKandi/Note-Making-Project/blob/main/img/caution.jpg" style='height: 35%; width: 35%; object-fit: contain'/>
</p>
    
``` python
  # Convert to gray scale
  if size(Inputimage,3)==3 % RGB image
  Inputimage=rgb2gray(Inputimage);
  end

  # Convert to binary image
  threshold = graythresh(Inputimage);
  Inputimage =~im2bw(Inputimage,threshold);


  # Remove all object containing fewer than 30 pixels
  Inputimage = bwareaopen(Inputimage,30);
  pause(1);


  # Label connected components
  [L Ne]=bwlabel(Inputimage);
  propied=regionprops(L,'BoundingBox');
  imshow(~Inputimage);
  hold on
  for n=1:size(propied,1)
  rectangle('Position',propied(n).BoundingBox,'EdgeColor','g','LineWidth',2)
  end
  hold off
  pause (1);
```  
<br/>
<p align="center">
  <img src="https://github.com/UjwalKandi/Note-Making-Project/blob/main/img/caution.png" style='height: 40%; width: 39%; object-fit: contain'/>
</p>

``` python
  # Objects extraction
  figure
  for n=1:Ne
  [r,c] = find(L==n);
  n1=Inputimage(min(r):max(r),min(c):max(c));
  imshow(~n1);
  pause(0.5)
  end
```  
<br/>
<p align="center">
  <img src="https://github.com/UjwalKandi/Note-Making-Project/blob/main/img/caution.gif" style='height: 40%; width: 40%; object-fit: contain'/>
</p>


