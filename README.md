# Time-Series-Analysis
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df_power = pd.read_csv("https://raw.githubusercontent.com/jenfly/opsd/refs/heads/master/opsd_germany_daily.csv")
df_power['Date'] = pd.to_datetime(df_power['Date'])
df_power = df_power.set_index('Date')
df_power['Year']=df_power.index.year
df_power['Month']=df_power.index.month
df_power['Weekday Name']=df_power.index.weekday_name
df_power.sample(5, random_state=0)
df_power.loc['2015-10-02']
sns.set(rc={'figure.figsize': (11, 4)})
plt.rcParams['figure.figsize'] = (8, 5)
plt.rcParams['figure.dpi'] = 100
df_power['Consumption'].plot(linewidth=0.5)
cols_to_plot = ['Consumption', 'Solar', 'Wind']
axes = df_power[cols_to_plot].plot( marker='.',alpha=0.5,linestyle='None', figsize=(14, 6),subplots=True)
for ax in axes:ax.set_ylabel('Daily Totals (GWh)')
ax = df_power.loc['2016', 'Consumption'].plot()
ax.set_ylabel('Daily Consumption (GWh)')
ax = df_power.loc['2016-12', 'Consumption'].plot(marker='o', linestyle='-')
ax.set_ylabel('Daily Consumption (GWh)')
ax = df_power.loc['2016-12-23':'2016-12-30', 'Consumption'].plot(marker='o', linestyle='-')
ax.set_ylabel('Daily Consumption (GWh)')

plt.show()
