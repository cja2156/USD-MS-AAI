import numpy as np
import matplotlib.pyplot as plt

# Function to simulate variability based on sample size
def simulate_variability(true_mean, true_std, sample_sizes, num_simulations=10000):
    results = {}
    for n in sample_sizes:
        sample_means = [np.mean(np.random.normal(true_mean, true_std, n)) for _ in range(num_simulations)]
        results[n] = sample_means
    return results

# Parameters
true_mean = 5.0  # Assume a true mean (e.g., average brain cancer rate or test score improvement)
true_std = 2.0  # Assume a true standard deviation
sample_sizes = [10, 30, 100, 300]  # Different sample sizes to simulate

# Simulate the variability
np.random.seed(57)
variability_results = simulate_variability(true_mean, true_std, sample_sizes)

# Plotting the results
fig, axs = plt.subplots(len(sample_sizes), 1, figsize=(12, 18))

for i, n in enumerate(sample_sizes):
    axs[i].hist(variability_results[n], bins=30, edgecolor='black', density=True)
    axs[i].set_title(f'Sampling Distribution of the Sample Mean (n = {n})')
    axs[i].set_xlabel('Sample Mean')
    axs[i].set_ylabel('Density')
    axs[i].axvline(true_mean, color='blue', linestyle='dashed', linewidth=1)
    axs[i].text(true_mean + 0.1, 0.05, f'Mean = {true_mean:.2f}', color='blue')

plt.tight_layout()
plt.show()
