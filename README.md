
# Traffic Circle Simulation

This project is a multithreaded simulation of a traffic circle designed for the Ministry of Transportation to analyze congestion patterns. 
The simulation leverages threads, mutual exclusion mechanisms, and randomized timing to model traffic flow.

## Features

### Simulation Details

- **Traffic Circle**:
  - Represented as a square grid with a side length of `N`.
  - Contains `4` car generators and `4` sinks located at the corners of the grid.

- **Car Behavior**:
  - Cars are generated at randomized intervals and enter the circle if adjacent slots are free.
  - Cars move to the next slot every `INTER_MOVES_IN_NS` nanoseconds.
  - Cars disappear with probability `FIN_PROB` at sinks after completing at least one side.

- **Snapshots**:
  - The simulation takes `10` snapshots during execution.
  - Each snapshot prints the grid, showing car positions (`*`), empty slots (` `), and middle squares (`@`).

### Example Output (N=5)

```
* *   
  @@@* 
*@@@* 
  @@@ 
* *        * 
```

### Requirements

- **Thread Management**:
  - One thread per car and one for each generator.
  - Threads are created and managed using `pthread_create()` and `pthread_join()`.

- **Mutexes**:
  - Each square in the grid has its own mutex for thread-safe operations.
  - Mutex initialization and destruction are handled appropriately.

- **Error Handling**:
  - Checks for errors in thread creation and mutex locking.
  - Prints an error message and exits on failures.

- **Performance**:
  - Cars progress simultaneously in different parts of the grid, avoiding deadlocks and minimizing mutex-locked sections.

### Parameters

Recommended default values:
```c
#define N 5
#define FIN_PROB 0.1
#define MIN_INTER_ARRIVAL_IN_NS 8000000
#define MAX_INTER_ARRIVAL_IN_NS 9000000
#define INTER_MOVES_IN_NS 100000
#define SIM_TIME 2
```

## How to Build and Run

1. Build the project:
   ```bash
   make
   ```

2. Run the simulation:
   ```bash
   ./traffic_circle
   ```

## Dependencies

- POSIX Threads (pthreads)
- Standard C library

## File Structure

- `main.c`: Implementation of the traffic circle simulation.
- `Makefile`: Automates the build process.

