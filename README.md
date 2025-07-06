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
