## Network Description:

### Buses:
- **Bus 1**: Slack Bus (Voltage magnitude = 1.0 pu, Voltage angle = 0°)
- **Bus 2**: PQ Bus (Load: 1.5 MW and 0.5 MVar)
- **Bus 3**: PQ Bus (Load: 2.0 MW and 1.0 MVar)

### Lines (All with an impedance of 0.1 + j0.2 pu):
- Line 1-2
- Line 2-3
- Line 3-1 (forming the loop)

## Objective:

Determine the voltage magnitude and angle at Buses 2 and 3 and the power flowing in each line.

## Method:

We will use the Newton-Raphson method for this example due to its robustness in handling complex networks.

## Steps:

1. **Initialization**:
   - Guess the voltage at Bus 2 and Bus 3. Let's assume V2 = V3 = 1.0 pu and angle = 0°.

2. **Calculate Power Mismatch**:
   - Calculate the power mismatch at Buses 2 and 3. Power mismatch ΔP and ΔQ are the differences between specified and calculated power.

3. **Jacobian Matrix**:
   - Construct and update the Jacobian matrix, which contains partial derivatives of power mismatches with respect to voltage magnitude and angles.

4. **Solve Linear Equations**:
   - Solve the linear equation system: `J * [ΔV] = [ΔP, ΔQ]` to find the changes in voltage magnitude and angle (ΔV).

5. **Update Voltages**:
   - Update the voltage at Buses 2 and 3 using the results from step 4.

6. **Check for Convergence**:
   - Check if the changes in voltage magnitude and angle are below a certain threshold. If not, go back to step 2.

7. **Results**:
   - Once converged, we have the voltage magnitude and angle at Buses 2 and 3.
   - Calculate the power flow in each line using the obtained voltages.

## Example Calculation:

Let's assume after one iteration, we get:

- V2 = 0.98 ∠-2°
- V3 = 0.97 ∠-3°

Using these voltages, we can calculate the power flow in each line:

- **Line 1-2**: `P_{1-2} = \frac{|V_1 - V_2|^2}{Impedance}`
- **Line 2-3**: `P_{2-3} = \frac{|V_2 - V_3|^2}{Impedance}`
- **Line 3-1**: `P_{3-1} = \frac{|V_3 - V_1|^2}{Impedance}`

## Conclusion:

In this simplified example, we saw how to perform load flow analysis in a network with loops. In a real-world scenario, the network would be much larger and more complex, but the principles remain the same. Software tools are often used for such analyses to handle the complexity and iterations efficiently.
