Developing an open-source software for load flow analysis of a distribution network with loops in Python requires a good understanding of power systems, numerical methods, and programming practices. Here's a basic outline and a simplified example to get you started:

1. **Setup**:
   Begin by importing necessary libraries and defining the data structures.

```python
import numpy as np

# Define data structures for buses, lines, and loads.
buses = []
lines = []
loads = []
```

2. **Data Input**:
   For simplicity, let's consider a system with three buses connected in a loop, and one of them has a load connected.

```python
# Example data: [bus_number, voltage_magnitude, voltage_angle]
buses = [[1, 1.0, 0.0],
         [2, 1.0, 0.0],
         [3, 1.0, 0.0]]

# [from_bus, to_bus, resistance, reactance]
lines = [[1, 2, 0.01, 0.03],
         [2, 3, 0.01, 0.03],
         [3, 1, 0.01, 0.03]]

# [bus_number, active_power, reactive_power]
loads = [[3, 0.5, 0.3]]
```

3. **Load Flow Analysis Using Newton-Raphson Method**:

```python
def jacobian(buses, lines):
    # Calculate the Jacobian matrix
    # ... [Implementation]
    return J

def mismatches(buses, lines, loads):
    # Calculate power mismatches
    # ... [Implementation]
    return deltaP, deltaQ

def newton_raphson(buses, lines, loads, max_iter=100, tol=1e-6):
    for i in range(max_iter):
        J = jacobian(buses, lines)
        deltaP, deltaQ = mismatches(buses, lines, loads)
        
        # If mismatches are below tolerance, break
        if max(abs(deltaP)) < tol and max(abs(deltaQ)) < tol:
            break
        
        # Solve for voltage corrections
        corrections = np.linalg.solve(J, np.concatenate((deltaP, deltaQ)))
        
        # Update bus voltages and angles
        # ... [Implementation]

    return buses
```

4. **Execution**:
   Use the developed function to solve the system.

```python
results = newton_raphson(buses, lines, loads)
print(results)
```

This is a very basic and abstract example. A fully functioning load flow software would need to account for various edge cases, have methods to handle non-convergences, implement a robust data input and output system, and possibly a graphical user interface for ease of use.

For larger networks, using a library like `pandapower` or `PYPOWER` would be more efficient. They have built-in functions for power system simulations, and you can customize or extend them for specific needs.
