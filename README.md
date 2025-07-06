# Lab Question 1
import random
import time
import matplotlib.pyplot as plt

# Linear search using `in` operator
def search_in_sequence(sequence, value):
    return value in sequence

# Generate a unique list of numbers
def generate_random_sequence(length):
    return list(range(1, length + 1))

# Plotting function
def plot_time_complexity(x, y_start, y_middle, y_end):
    plt.plot(x, y_start, marker='o', label='Start')
    plt.plot(x, y_middle, marker='o', label='Middle')
    plt.plot(x, y_end, marker='o', label='Back')
    plt.xlabel('Sequence Length')
    plt.ylabel('Average Time (seconds)')
    plt.title('Time Complexity of Search Positions')
    plt.legend()
    plt.grid(True)
    plt.show()

# Setup
sequence_lengths = [10345,59038, 15345, 20123]
num_trials = 1000

# Store results
average_times = {
    'Start': [],
    'Middle': [],
    'Back': []
}

# Main Experiment
for length in sequence_lengths:
    total_time = {'Start': 0, 'Middle': 0, 'Back': 0}
    
    for _ in range(num_trials):
        sequence = generate_random_sequence(length)
        random.shuffle(sequence)  # Make it unordered
        
        # Positions to test
        values = {
            'Start': sequence[0],
            'Middle': sequence[length // 2],
            'Back': sequence[-1]
        }
        
        for pos in ['Start', 'Middle', 'Back']:
            start_time = time.time()
            search_in_sequence(sequence, values[pos])
            end_time = time.time()
            total_time[pos] += (end_time - start_time)
    
    # Compute average
    for pos in ['Start', 'Middle', 'Back']:
        avg = total_time[pos] / num_trials
        average_times[pos].append(avg)

# Plot results
plot_time_complexity(
    sequence_lengths,
    average_times['Start'],
    average_times['Middle'],
    average_times['Back']
)

# Lab Question-2 

# DAA_LinearSearch
import random
import time
import matplotlib.pyplot as plt

def search_in_sequence(sequence, value):
    return value in sequence

def generate_random_unique_sequence(length):
    return random.sample(range(1, length+1), length)

def plot_time_complexity(x, y, title):
    plt.plot(x, y, marker='o')
    plt.xlabel('Sequence Length')
    plt.ylabel('Average Time (seconds)')
    plt.title(title)
    #plt.grid(True)
    plt.show()

sequence_lengths = [5000,10000,15000,20000]  # Vary the sequence lengths as desired
num_trials = 1000

search_positions = ['Start', 'Middle', 'End']
search_values = []
for length in sequence_lengths:
    sequence = generate_random_unique_sequence(length)
    search_values.append([random.choice(sequence) for _ in range(num_trials)])
    #print(search_values)

average_times = {position: [] for position in search_positions}

for position in search_positions:
    for length, values in zip(sequence_lengths, search_values):
        total_time = 0
        for value in values:
            sequence = generate_random_unique_sequence(length)
           # sequence.sort()  # Simulating unordered sequence

            start_time = time.time()
            search_in_sequence(sequence, value)
            end_time = time.time()

            total_time += (end_time - start_time)
        average_time = total_time / num_trials
        average_times[position].append(average_time)

for position in search_positions:
    plot_time_complexity(sequence_lengths, average_times[position], f'Time Complexity - Search at {position}')
 

# Practice Question 1
import random
import matplotlib.pyplot as plt
import time as time

def generateList(size):
  return random.sample(range(1,size*10),size)

def linerSearch(arr,target):
  for num in arr:
    if(num == target):
      return num
  return -1

def measureTime(arr,target):
  startTime=time.time()
  linerSearch(arr,target)
  endTime=time.time()
  return endTime - startTime

timeStart=[]
timeMid=[]
timeEnd=[]

sizes = [100,23430,4500,7000,6770,5666]
for size in sizes:
  arr=generateList(size)

  arr[0]=-1
  startTime=measureTime(arr,-1)

  arr[size//2]=-2
  midTime=measureTime(arr,-2)

  arr[-1]=-3
  endTime=measureTime(arr,-3)

  timeStart.append(startTime)
  timeMid.append(midTime)
  timeEnd.append(endTime)

plt.plot(sizes,timeStart,marker='o',label='start')
plt.plot(sizes,timeMid,marker='o',label='mid')
plt.plot(sizes,timeEnd,marker='o',label='End')

plt.xlabel('Size of array')
plt.ylabel('Time in Seconds')
plt.legend()
plt.grid(True)
plt.show()

# Practice Question 2

# Analyzing the number of comparisons made in each search 

import random
import matplotlib.pyplot as plt
import time as time

def generateList(size):
  return random.sample(range(1,size*10),size)

def linearSearch(arr,target):
  comparisons=0
  for num in arr:
    comparisons+=1
    if(num == target):
      break
  return comparisons


timeStart=[]
timeMid=[]
timeEnd=[]

sizes = [100,23430,4500,7000,6770,5666]
for size in sizes:
  arr=generateList(size)

  startTime=linearSearch(arr,arr[0])
  midTime=linearSearch(arr,arr[size//2])
  endTime=linearSearch(arr,arr[-1])

  timeStart.append(startTime)
  timeMid.append(midTime)
  timeEnd.append(endTime)

plt.plot(sizes,timeStart,marker='o',label='start')
plt.plot(sizes,timeMid,marker='o',label='mid')
plt.plot(sizes,timeEnd,marker='o',label='End')

plt.xlabel('Size of array')
plt.ylabel('Number of comparisons')
plt.title("Analyzing number of comparisons in each search")
plt.legend()
plt.grid(True)
plt.show()
