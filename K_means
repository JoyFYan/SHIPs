clc
clear
tic
RGBD= imread ('1.bmp'); %读入像
% RGBD= imread ('my4.bmp'); %读入像
img=rgb2gray(RGBD);
img=myhistf( img,1.5,600 );
[m,n]=size(img);
subplot(2,2,1),imshow(img);title(' 图一 原图像')
subplot(2,2,2),imhist(img);title(' 图二 原图像的灰度直方图')
hold off;
img=double(img);
for i=1:200
    c1(1)=15;
    c2(1)=125;
    c3(1)=200;
    c4(1)=255;%选择三个初始聚类中心
    r=abs(img-c1(i));
    g=abs(img-c2(i));
    b=abs(img-c3(i));
    d=abs(img-c4(i));%计算各像素灰度与聚类中心的距离
    r_g=r-g;
    g_b=g-b;
    b_d=b-d;
    r_b=r-b;
    r_d=r-d;
    g_d=g-d;
    n_r=find(r_g<=0&r_b<=0&r_d<=0);%寻找最小的聚类中心
    n_g=find(r_g>0&g_b<=0&g_d<=0);%寻找较小的一个聚类中心
    n_b=find(r_b>0&g_b>=0&b_d<=0);%寻找较大的一个聚类中心
    n_d=find(g_d>0&r_d>0&b_d>0);%寻找最大的聚类中心
    i=i+1;
    c1(i)=sum(img(n_r))/length(n_r);%将所有低灰度求和取平均，作为下一个低灰度中心
    c2(i)=sum(img(n_g))/length(n_g);%将所有较低灰度求和取平均，作为下一个中间灰度中心
    c3(i)=sum(img(n_b))/length(n_b);%将所有较高灰度求和取平均，作为下一个高灰度中心
    c4(i)=sum(img(n_d))/length(n_d);%将所有高灰度求和取平均，作为下一个高灰度中心
    d1(i)=abs(c1(i)-c1(i-1));
    d2(i)=abs(c2(i)-c2(i-1));
    d3(i)=abs(c3(i)-c3(i-1));
    d4(i)=abs(c4(i)-c4(i-1));
    if d1(i)<=0.001&&d2(i)<=0.001&&d3(i)<=0.001&&d4(i)<=0.001
        R=c1(i);
        G=c2(i);
        B=c3(i);
        D=c4(i);
        k=i; 
        break;
    end
end
R 
G 
B
D
img=uint8(img);
img(find(img<R))=0;
img(find(img>R&img<G))=85;
img(find(img>G&img<D))=170;
img(find(img>D))=255;
toc
subplot(2,2,3),imshow(img);title(' 图三 聚类后的图像') 
subplot(2,2,4),imhist(img);title(' 图四 聚类后的图像直方图') 
