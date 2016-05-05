clear;
clc;
load('data.mat');

figure1 = figure('units','normalized','position',[.1 .1 .4 .6]);
xvalues = [0,0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1];
[a,b]=hist(Data_Business.DeathRate,xvalues);
labels = cellstr(num2str(b(:)))';
explode = [0 0 0 0 0 0 0 0 0 0 1];
pie(a,explode,labels');
h = title('Business Flight Fatal Injuries Rate');
 set(h,'color','red')
 set(h,'FontSize',20)
 set(h,'FontWeight','bold');
saveas(figure1,'Fatelrate_business.jpg');

figure2 = figure('units','normalized','position',[.1 .1 .6 .6]);
xvalues = [0,0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1];
hist(Data_Business.InjurRate,xvalues);
h = title('Business flight Casualty Rate');
 set(h,'color','red')
 set(h,'FontSize',20)
 set(h,'FontWeight','bold');
saveas(figure2,'Injurrate_business.jpg');

figure4 = figure('units','normalized','position',[.1 .1 .4 .6]);
[a,b]=hist(Data_Business.TotalFatalInjuries,unique(Data_Business.TotalFatalInjuries));
labels = cellstr(num2str(b(:)))';
explode = [1 1 0 0 0 0 0 0 ];
p=pie(a,explode,labels');
hText = findobj(p,'Type','text'); % text handles
set(hText,'Visible','off');
set(hText(1),'Visible','on');
set(hText(2),'Visible','on');
set(hText(3),'Visible','on');
set(hText(4),'Visible','on');
set(hText(5),'Visible','on');
set(hText(6),'Visible','on');
set(hText(7),'Visible','on');
set(hText(8),'Visible','on');
h = title('Business Flight Fatal Injuries Count');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
saveas(figure4,'Fatel_business.jpg');

figure5 = figure('units','normalized','position',[.1 .1 .5 .7]);
tb3 = tabulate(Data_Business.BroadPhaseofFlight);
labels = {'Stading','Take off','Climb','Cruise','Descent','Maneuver','Approach','Landing','Go around','Other','Taxi','Unknown'};
explode = [0 1 0 1 0 1 1 0 0 0 0 0];
pie(tb3(:,2),explode,labels')
h = title('Business Flight Accident Phase');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
saveas(figure5,'Accident_phase_business.jpg');

figure6 = figure('units','normalized','position',[.1 .1 .6 .8]);
tb4 = tabulate(Data_Business.Make);
[trash, idx] = sort([tb4{:,3}],'descend');
label = tb4(idx);
p = pie(trash);
hText = findobj(p,'Type','text'); % text handles
set(hText,'Visible','off');
set(hText(1),'Visible','on');
set(hText(2),'Visible','on');
set(hText(3),'Visible','on');
set(hText(4),'Visible','on');
set(hText(5),'Visible','on');
set(hText(6),'Visible','on');
h = title('Maker for business flight');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
rgbmatrix = [rand(38,1), rand(38,1), rand(38,1)];
for k = 1 : 38
  pieColorMap = rgbmatrix(k,:);
  set(p(k*2-1), 'FaceColor', pieColorMap);
end
legend(label(1:6),'Location','southoutside','Orientation','horizontal');
saveas(figure6,'Maker_business.jpg');

Cor = [Data_Business.AircraftDamage'./max(Data_Complex.AircraftDamage);
       Data_Business.TotalFatalInjuries'./max(Data_Complex.TotalFatalInjuries);
       Data_Business.NumberofEngines'./max(Data_Complex.NumberofEngines);
       Data_Business.BroadPhaseofFlight'./max(Data_Complex.BroadPhaseofFlight)]';
[R,Pvalue]=corrplot(Cor,'type','Kendall','testR','on','varNames',{'Dmg','Injry','Engs','Phase'});
fig = gcf;
fig.PaperUnits = 'inches';
fig.PaperPosition = [0 0 8 6];
saveas(gcf,'Correlation_business.jpg');