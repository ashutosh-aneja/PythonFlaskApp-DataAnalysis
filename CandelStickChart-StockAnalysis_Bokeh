
import pandas as pd
from bokeh.plotting import figure, show, output_file
pd.core.common.is_list_like=pd.api.types.is_list_like
import pandas_datareader.data as web
import datetime


start=datetime.datetime(2018,3,1)
end=datetime.datetime(2018,5,20)
df=web.DataReader('AMZN','iex',start,end)
df["Date"] = pd.to_datetime(df.index)

def inc_dec(c, o):
        if c > o:
            value="Increase"
        elif c < o:
            value="Decrease"
        else:
            value="Equal"
        return value

df["Status"]=[inc_dec(c,o) for c, o in zip(df.close,df.open)]
df["Middle"]=(df.open+df.close)/2
df["Height"]=abs(df.close-df.open)

p=figure(x_axis_type='datetime', width=1000, height=300)
p.title.text="Candlestick Chart"
p.grid.grid_line_alpha=0.3

hours_12=12*60*60*1000

p.segment(df.Date, df.high, df.Date, df.low, color="Black")

p.rect(df.Date[df.Status=="Increase"],df.Middle[df.Status=="Increase"],
           hours_12, df.Height[df.Status=="Increase"],fill_color="#CCFFFF",line_color="black")

p.rect(df.Date[df.Status=="Decrease"],df.Middle[df.Status=="Decrease"],
           hours_12, df.Height[df.Status=="Decrease"],fill_color="#FF3333",line_color="black")

output_file("stock.html", title="candlestick.py example")

show(p)

df
