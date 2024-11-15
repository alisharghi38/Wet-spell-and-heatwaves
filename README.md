# Wet-spell-and-heatwaves
These MATLAB codes could potentially extract frequency duration and intensity of any wet spell, heat wave and IDF curves if correct format is given.
%Heatwave codes
clc
clear all
load obs_jun;
A=obs_jun;
n=1;
h=1;
q=1;
m=length(A);
Xout=[];
for i=1:m-1
 if A(i)>=34.26 && A(i+1)>=34.26
     n=n+1;
 else
     n=1;
 end
 W(i)=n;
end
disp(W);
 L=length(W);
 for i=1:L-1
 if W(i)>W(i+1)
     h=W(i);
     Xout=[Xout;h];
 end
 end
 if W(L-1)<W(L)
     q=W(L);
     disp(q);
 end
 
 MAXHL=max(Xout)
 MEANHL=mean(Xout)
 
% Wet spells code
clc
clear all
m=0;
prompt=('input wet searies = ');
wet = input(prompt);
l=length(wet);
for i=1:l
    if wet(i)<=2
        m=m+1;
    end
end
probebility=m/l;
disp (probebility)
%IDF codes
clc
clear all
%t= duration of precipitation (min)
t=61:15:121;
%
idf_245=zeros(1,5);
idf_585=zeros(1,5);
idf=zeros(1,5);
    for i=1:5
    h(i)=t(i)/180;
    A=0.1372;
    B=0.4778;
    a1=0.4606;
    a2=0.2349;
    a3=0.6;
    idf(1,i)= (A*(h(i)^B)*(a1+a2*log(20-a3))*36.9585) /h(i);
    idf_245(1,i)=(A*(h(i)^B)*(a1+a2*log(20-a3))*42.4842) /h(i);
    idf_585(1,i)=(A*(h(i)^B)*(a1+a2*log(20-a3))*41.63723) /h(i);
    end
    t2=121:15:451;
    idf_245_2=zeros(1,23);
idf_585_2=zeros(1,23);
idf_2=zeros(1,23);

    for i2=1:23
    h(i2)=t2(i2)/180;
    A=0.1589;
    B=0.4361;
    a1=0.5565;
    a2=0.1948;
    a3=0.8;
    idf_2(1,i2)= (A*(h(i2)^B)*(a1+a2*log(20-a3))*36.9585) /h(i2);
    idf_245_2(1,i2)=(A*(h(i2)^B)*(a1+a2*log(20-a3))*42.4842) /h(i2);
    idf_585_2(1,i2)=(A*(h(i2)^B)*(a1+a2*log(20-a3))*41.63723) /h(i2);
    end
figure;
hold on
 k = plot(t,idf);
%  k1= plot(t,idf_245);
%  k2= plot(t,idf_585);
k4 = plot(t2,idf_2);
% k5= plot(t2,idf_245_2);
% k6= plot(t2,idf_585_2);


% elseif 60<t<=120
%     A=0.1372;
%     B=0.4778;
%     a1=0.4608;
%     a2=0.2349;
%     a3=0.62;
% elseif 120<t<=540
%     A=0.2009;
%     B=0.3937;
%     a1=0.5565;
%     a2=0.1948;
%     a3=0.8;
% end
