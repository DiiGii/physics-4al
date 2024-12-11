# physics-4al
Github for physics 4al notebook code

```python
# Import statements
import numpy as np
import matplotlib.pyplot as plt

# Load in data
control1 = np.loadtxt('baby_oil4.txt', delimiter=';')
time = control1[:,0]
elapsed_time = (time-time[0]) / 1000.
ultrasound_unrefined = control1[:,1]
ultrasound = ultrasound_unrefined / 100

# Plot data
# Create a scatter plot
plt.scatter(elapsed_time,ultrasound,color="blue")
# Provide a title to the plot
plt.title('Ultrasound data for control1')
# Label the y-axis
plt.ylabel('Displacement (m)')
# Label the x-axis
plt.xlabel('Time (s)')
plt.show()

# Create a variable that starts from 0 and ends at the size of the array
array_index=np.arange(0,len(ultrasound))
# Plot the distance vs array index
plt.scatter(array_index, ultrasound)
# Add axes labels
plt.xlabel('Array index')
plt.ylabel('Distance (m)')

--- 

# Get lower and upper index

lower_index = 0
upper_index = 56

lower_time_limit = elapsed_time[lower_index]
print('The lower time cutoff is ' + str(lower_time_limit))

upper_time_limit = elapsed_time[upper_index]
print('The upper time cutoff is ' + str(upper_time_limit))

# Create new arrays for the time window and distance window that we care about
time_window = elapsed_time[lower_index:upper_index]
dist_window = ultrasound[lower_index:upper_index]

plt.plot(time_window, dist_window)

# Add axes labels
plt.xlabel('Time (s)')
plt.ylabel('Distance (m)')

---
coeff_quad = np.polyfit(time_window, dist_window, 2)
y_fit=coeff_quad[0]*time_window**2+coeff_quad[1]*time_window+coeff_quad[2]

plt.plot(time_window,y_fit, label = 'Model', color='red')
plt.scatter(time_window, dist_window, label = 'Data')
plt.legend()

# Your x and y axes labels here
plt.xlabel('Time (s)')
plt.ylabel('Distance (m)')


#Title 
plt.title('Fitted Distance (m) vs Time (s)')
print('Acceleration is ' + str(coeff_quad[0] * 2) + ' meters per second squared')

---
coeff_quad, cov_quad = np.polyfit(time_window, dist_window, 2, cov=True)

# Error in quadratic coefficient
quad_err = np.sqrt(cov_quad[0,0])

# Error in accel
accel_err = 2 * quad_err
print("error:")
print(accel_err)
```
