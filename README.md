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

 
