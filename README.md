# BurstCube-SiPM-Testing
Summer 2016-Created a code used to modify data collected from the oscilloscope using height, max, and moving average
%matplotlib 
import matplotlib.pyplot as plt 
import numpy as np
Using matplotlib backend: MacOSX
In [2]:

from astropy.io import ascii
from glob import glob
In [26]:

files = glob("Desktop/Data Acquisition_07.28.2016/*.CSV")
In [27]:

my_data = [ascii.read(f) for f in files]
In [28]:

def pha(data, window):
    moving_sum = np.convolve(data[1300:1500], np.ones(int(window)), 'same')
    return np.max(moving_sum)
In [22]:

for i,data in enumerate(my_data):
    if len(data) < 10:
        print i
1153
In [29]:

heights = np.array([])
for data in my_data:
    heights = np.append(heights, pha(data['col5'],3))
    
In [9]:

cd Data\ Acquisition_07.28.2016
/Users/Mac/Desktop/Data Acquisition_07.28.2016
In [41]:

a = plt.hist(heights,bins=30.)
plt.title('Signal Data Analysis')
plt.xlabel('Voltage(V)')
plt.ylabel('Counts')
plt.grid(True)
In [26]:

a[0].sum()
Out[26]:
1153.0
