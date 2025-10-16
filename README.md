Some parts of the work were discussed with **Michele Carena s349483**, **Alessandro Benvenuti s343784** and **Federico Carollo s339645** to exchange ideas and approaches.
## Solution Strategy

The implemented solution uses a **Hill Climbing** approach with the following steps:

## Initialization
- **Random generation:** Each knapsack-item pair is randomly assigned with 50% probability

## Tweak Function
The `tweak` function implements an adaptive perturbation strategy:

- **Adaptive iterations:** The number of modifications depends on the current assignment ratio:
  - Low assignment ratio (<10%): 3-8 modifications (aggressive exploration)
  - Medium assignment ratio (10-30%): 2-5 modifications (moderate exploration)  
  - High assignment ratio (>30%): 1-3 modifications 

- **Operations performed:**
  - **Remove item:** If item is in the selected knapsack, remove it
  - **Add item:** If item is unassigned, add it to the selected knapsack
  - **Move item:** If item is in another knapsack, move it to the new knapsack

### Constraint validation
The `make_valid` method ensures solution feasibility through:

1. **Duplicate resolution:** Removes items from multiple knapsacks (keeping only the first occurrence) -> this step is useful in the initial part, where a random solution is picked and duplicates can happen.
2. **Capacity violation repair:** For each violating knapsack:
   - Identifies items causing constraint violations
   - Randomly removes a subset of items until constraints are satisfied

### Fitness Evaluation
- **Simple objective:** Sum of values of all assigned items across all knapsacks
- **Assumption:** Only valid solutions are evaluated (validation is performed before fitness calculation)