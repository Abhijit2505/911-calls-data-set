# importing the required libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style("whitegrid")

# splitting and preparing the data to analyse and visualise
df = pd.read_csv('911.csv')
df['reason'] = df['title'].apply(lambda title:title.split(':')[0])
df['timeStamp'] = pd.to_datetime(df['timeStamp'])
df['Hour'] = df['timeStamp'].apply(lambda time: time.hour)
df['Month'] = df['timeStamp'].apply(lambda time: time.month)
df['Day of Week'] = df['timeStamp'].apply(lambda time: time.dayofweek)
df['Date']=df['timeStamp'].apply(lambda t: t.date())

# analysing categories of the reason with the 'hour' of call with violin plot
sns.violinplot(x = 'reason',y='Hour',data = df,palette = 'rainbow')

# analysing categories of the reason with the 'Day of week' of call
sns.countplot(x = 'Day of Week',data = df,hue = 'reason',palette = 'Set1')
plt.legend(bbox_to_anchor=(1., 1), loc=2, borderaxespad=0.)

# analysing categories of the reason with the 'month' of call
sns.countplot(x ='Month',data = df,hue = 'reason',palette = 'rainbow')
plt.legend(bbox_to_anchor=(1.,1),loc=2,borderaxespad=0)
# analysing with violin plot
sns.violinplot(x = 'reason',y='Month',data = df,palette = 'Set2')

# analysing the reason to call on a some day at a particular 'hour'
dayHour = df.groupby(by=['Day of Week','Hour']).count()['reason'].unstack()
plt.figure(figsize=(12,6))
# analysing using heatmap
sns.heatmap(dayHour,cmap='coolwarm')
# analysing using clustermap
sns.clustermap(dayHour,cmap='viridis')

# analysing the relationship of  
# total number of calls received on a particular month 
byMonth = df.groupby('Month').count()
byMonth['twp'].plot()
# plotting a regression line between 'Month' and total number of calls received in that month
sns.lmplot(x='Month',y='twp',data=byMonth.reset_index())

# analysing the total calls received from the 'twp' on a particular 'Date'
byDate = df.groupby('Date').count()['twp']
byDate.plot()

# analysing the data having reason 'Traffic' with respect to the 'Date' of emergency call
Traffic_data = df[df['reason']=='Traffic'].groupby('Date').count()['twp']
Traffic_data.plot()
plt.title('Traffic')

# analysing the data having reason 'Fire' with respect to the 'Date' of emergency call
Fire_data = df[df['reason']=='Fire'].groupby('Date').count()['twp']
Fire_data.plot()
plt.title('Fire')

#analysing the data having reason 'EMS' with respect to the 'Date' of emergency call
EMS_data = df[df['reason']=='EMS'].groupby('Date').count()['twp']
EMS_data.plot()
plt.title('EMS')
plt.tight_layout()
