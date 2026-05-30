# Philosophers Project (Dining Philosophers Problem)

A multithreaded simulation of the classic **Dining Philosophers Problem**, implemented in C using POSIX threads (pthreads) and mutex synchronization.

This project explores concurrent programming, race condition prevention, deadlock handling, and precise thread synchronization in a shared-resource environment.

---

## Overview

The goal of this project is to simulate a group of philosophers sitting at a table who alternate between thinking, eating, and sleeping.

Each philosopher requires two forks (shared resources) to eat, which introduces classical concurrency problems such as:

* Deadlocks
* Race conditions
* Resource starvation
* Thread synchronization issues

The challenge is to design a system where all philosophers can operate safely without conflicts or crashes.

---

## Key Features

### Threading System

* One thread per philosopher
* Independent lifecycle execution
* Concurrent simulation of actions

### Synchronization

* Mutex-based fork protection
* Safe access to shared resources
* Prevention of race conditions
* Controlled locking/unlocking strategy

### Monitoring System

* Global simulation monitor thread
* Death detection system
* Time-based state tracking
* Early termination handling

### Simulation Rules

* Philosophers alternate between:

  * Eating
  * Thinking
  * Sleeping
* A philosopher dies if they do not eat within a defined time limit
* Simulation stops when a death is detected or conditions are met

---

## Project Structure

```bash id="philo1"
.
├── philo.c
├── philo.h
├── init.c
├── actions.c
├── monitor.c
├── philo_routine.c
├── lock_forks.c
├── parse.c
├── philo_utils.c
├── philo_utils2.c
└── Makefile
```

### Module Breakdown

| File              | Responsibility                               |
| ----------------- | -------------------------------------------- |
| `philo.c`         | Program entry point                          |
| `init.c`          | Initialization of philosophers and resources |
| `actions.c`       | Core actions (eat, sleep, think)             |
| `philo_routine.c` | Philosopher thread lifecycle                 |
| `lock_forks.c`    | Fork locking strategy                        |
| `monitor.c`       | Death monitoring system                      |
| `parse.c`         | Argument parsing and validation              |
| `philo_utils.c`   | Utility functions                            |
| `philo_utils2.c`  | Additional helpers                           |

---

## How It Works

Each philosopher runs in a separate thread executing the following cycle:

1. Think
2. Pick up forks (mutex lock)
3. Eat
4. Release forks (mutex unlock)
5. Sleep
6. Repeat

A monitoring thread continuously checks:

* If any philosopher has exceeded the time-to-die threshold
* If the simulation should terminate

This ensures safe termination and prevents undefined behavior.

---

## Synchronization Strategy

To avoid classic concurrency problems:

* Mutexes protect fork access
* Lock ordering prevents deadlocks
* Shared state is carefully synchronized
* Atomic-like checks are used for simulation state

The design ensures:

* No two philosophers use the same fork simultaneously
* No circular waiting condition occurs
* Proper termination under all conditions

---

## Compilation

```bash id="p8qk2l"
make
```

Run the program:

```bash id="l1v9xw"
./philo number_of_philosophers time_to_die time_to_eat time_to_sleep [number_of_meals]
```

Example:

```bash id="c9ph3o"
./philo 5 800 200 200
```

---

## Technical Concepts Demonstrated

* Multithreading with pthreads
* Mutex synchronization
* Race condition prevention
* Deadlock avoidance strategies
* Critical section management
* Time-sensitive programming
* System-level C development
* Resource sharing algorithms

---

## Challenges Solved

### Deadlock Prevention

Careful fork acquisition strategy ensures no circular wait occurs.

### Race Conditions

All shared state is protected using mutex locks.

### Precise Timing

Accurate time tracking ensures correct simulation behavior.

### Thread Safety

All philosopher actions are executed in a thread-safe manner.

---

## Learning Outcomes

This project builds strong foundations in:

* Concurrency theory and practice
* Operating system concepts
* Thread lifecycle management
* Synchronization primitives
* Low-level debugging techniques
* System reliability under race conditions

---

## Future Improvements

* Reduce mutex contention for better performance
* Improve scheduling fairness
* Implement lock-free optimizations
* Add visualization of philosopher states
* Explore advanced concurrency models (semaphores, atomics)
