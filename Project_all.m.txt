clear;
clc;
load('data.mat');

figure1 = figure('units','normalized','position',[.1 .1 .4 .6]);
xvalues = [0,0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1];
[a,b]=hist(Data_Complex.DeathRate,xvalues);
labels = cellstr(num2str(b(:)))';
explode = [0 0 0 0 0 0 0 0 0 0 1];
pie(a,explode,labels');
h = title('Fatal Injuries Rate Chart');
 set(h,'color','red')
 set(h,'FontSize',20)
 set(h,'FontWeight','bold');
saveas(figure1,'Fatelrate_all.jpg');

figure2 = figure('units','normalized','position',[.1 .1 .6 .6]);
xvalues = [0,0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1];
hist(Data_Complex.InjurRate,xvalues);
h = title('Casualty Rate Chart');
 set(h,'color','red')
 set(h,'FontSize',20)
 set(h,'FontWeight','bold');
saveas(figure2,'Injurrate_all.jpg');

figure3 = figure('units','normalized','position',[.05 .05 1.0 .6]);
tb1 = tabulate(Data_Complex.PurposeofFlight);
labels = {'Unknown','Personal','Business','Instructional','Ferry','Aerial Application','Aerial Observation','Other Work Use','Public Use','Executive/Corporate','Positioning'};
bar(tb1(:,2))
 set(gca,'XTickLabel',labels);
h = title('Purpose of Flight Chart');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
saveas(figure3,'Purpose_all.jpg');

figure4 = figure('units','normalized','position',[.1 .1 .4 .6]);
[a,b]=hist(Data_Complex.TotalFatalInjuries,unique(Data_Complex.TotalFatalInjuries));
labels = cellstr(num2str(b(:)))';
explode = [1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0];
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
set(hText(30),'Visible','on');
h = title('Fatal Injuries Count Chart');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
rgbmatrix = [rand(477,1), rand(477,1), rand(477,1)];
for k = 1 : 30
  pieColorMap = rgbmatrix(k,:);
  set(p(k*2-1), 'FaceColor', pieColorMap);
end
saveas(figure4,'Fatel_all.jpg');

figure5 = figure('units','normalized','position',[.1 .1 .5 .7]);
tb3 = tabulate(Data_Complex.BroadPhaseofFlight);
labels = {'Stading','Take off','Climb','Cruise','Descent','Maneuver','Approach','Landing','Go around','Other','Taxi','Unknown'};
explode = [0 1 0 1 0 1 1 0 0 0 0 0];
pie(tb3(:,2),explode,labels')
h = title('Accident Phase Chart');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
saveas(figure5,'Accident_phase.jpg');

figure6 = figure('units','normalized','position',[.1 .1 .7 .8]);
tb4 = tabulate(Data_Complex.Make);
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
h = title('Maker Chart');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
rgbmatrix = [rand(477,1), rand(477,1), rand(477,1)];
for k = 1 : 477
  pieColorMap = rgbmatrix(k,:);
  set(p(k*2-1), 'FaceColor', pieColorMap);
end
legend(label(1:6),'Location','southoutside','Orientation','horizontal');
saveas(figure6,'Maker.jpg');

Cor = [Data_Complex.AircraftDamage'./max(Data_Complex.AircraftDamage);
       Data_Complex.TotalFatalInjuries'./max(Data_Complex.TotalFatalInjuries);
       Data_Complex.NumberofEngines'./max(Data_Complex.NumberofEngines);
       Data_Complex.BroadPhaseofFlight'./max(Data_Complex.BroadPhaseofFlight);
       Data_Complex.PurposeofFlight'./max(Data_Complex.PurposeofFlight)]';
[R,Pvalue]=corrplot(Cor,'type','Kendall','testR','on','varNames',{'Dmg','Injry','Engs','Phase','FType'});
fig = gcf;
fig.PaperUnits = 'inches';
fig.PaperPosition = [0 0 8 6];
saveas(gcf,'Correlation_all.jpg');

figure8 = figure('units','normalized','position',[.1 .1 .7 .7]);
label=['1982','1983','1984','1985','1986','1987','1988','1989','1990'];
x=1:1:9;
subplot(2,1,1);
q=plot(All_Count.VarName2,All_Count.VarName1,Business_Count.VarName2,Business_Count.VarName1);
set(q(1),'Marker','*');
set(q(1),'LineWidth',2);
set(q(2),'Marker','o');
set(q(2),'LineWidth',2);
h = title('Total Accident Count');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
legend('All Accident Count','Business Accident Count');
subplot(2,1,2);
p=plot(All_Count.VarName2,All_Count.VarName1./max(All_Count.VarName1),Business_Count.VarName2,Business_Count.VarName1./max(Business_Count.VarName1));
set(p(1),'Marker','*');
set(p(1),'LineWidth',2);
set(p(2),'Marker','o');
set(p(2),'LineWidth',2);
h = title('Normalized Accident Count');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
legend('All Accident','Business Accident');
saveas(figure8,'Count.jpg');

figure9 = figure('units','normalized','position',[.1 .1 .8 .6]);
tb9a = tabulate(Data_Complex.WeatherCondition);
X = tb9a(:,2);
label = {'IMC','VMC','UNK'};
cta = {num2str(tb9a(1,2)),num2str(tb9a(2,2)),num2str(tb9a(3,2))};
pta = {num2str(tb9a(1,3)),num2str(tb9a(2,3)),num2str(tb9a(3,3))};
labela = strcat(strcat(strcat(cta,{' : ',' : ',' : '}),pta),{'%','%','%'});
ax1 = subplot(1,2,1);
pie(ax1,X,labela)
h = title('All Weather Conditions');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
legend('IMC','VMC','UNK');
tb9b = tabulate(Data_Business.WeatherCondition);
Y = tb9a(:,2);
ctb = {num2str(tb9b(1,2)),num2str(tb9b(2,2)),num2str(tb9b(3,2))};
ptb = {num2str(tb9b(1,3)),num2str(tb9b(2,3)),num2str(tb9b(3,3))};
labelb = strcat(strcat(strcat(ctb,{' : ',' : ',' : '}),ptb),{'%','%','%'});
ax2 = subplot(1,2,2);
pie(ax2,Y,labelb)
h = title('Business Weather Conditions');
set(h,'color','red')
set(h,'FontSize',20)
set(h,'FontWeight','bold');
legend('IMC','VMC','UNK');
saveas(figure9,'Weather.jpg');