# Al-Hydrocarbon-Explorer_Dr.Mutlu-Zeybek
# ZEYBEK-1 MODEL: Structural Trap Identification Map
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.patches import Rectangle
from matplotlib.lines import Line2D

# Create figure
fig, ax = plt.subplots(figsize=(16, 10), dpi=300)

# Define coordinates
x0, x1, x2, x3, x4, x5, x6 = 0, 2, 4, 6, 8, 10, 18
y0, y1, y2, y3 = -2, 1, 5, 7

# Plot lithology units
# L1 (Source Rock - Brown)
ax.add_patch(Rectangle((x0, y0), x6-x0, y1-y0, facecolor='brown', alpha=0.6, label='L1 Source Rock'))
# L2 (Reservoir - Yellow)
ax.add_patch(Rectangle((x0, y1), x6-x0, y2-y1, facecolor='yellow', alpha=0.6, label='L2 Reservoir'))
# L3 (Cap Rock - Green)
ax.add_patch(Rectangle((x0, y2), x6-x0, y3-y2, facecolor='green', alpha=0.6, label='L3 Cap Rock'))

# Plot faults
# F1 (Conductive - Red)
ax.axvline(x=x1, color='red', linewidth=3, linestyle='--', label='F1 Conductive Fault')
# F2 (Sealing - Blue)
ax.axvline(x=x2, color='blue', linewidth=3, linestyle='-', label='F2 Sealing Fault')
# F3 (Sealing - Blue)
ax.axvline(x=x4, color='blue', linewidth=3, linestyle='-', label='F3 Sealing Fault')
# F4 (Conductive - Red)
ax.axvline(x=x5, color='red', linewidth=3, linestyle='--', label='F4 Conductive Fault')

# Plot target
ax.plot(x3, (y1+y2)/2, 'r*', markersize=20, label='Drill Target')

# Set labels and title
ax.set_xlabel('X Coordinate (East)', fontsize=14)
ax.set_ylabel('Y Coordinate (Depth/North)', fontsize=14)
ax.set_title('ZEYBEK-1 Model: Structural Trap Identification Map', fontsize=16)

# Set grid and limits
ax.grid(True, alpha=0.3)
ax.set_xlim(x0-1, x6+1)
ax.set_ylim(y0-1, y3+1)

# Add coordinate labels
for i, x in enumerate([x0, x1, x2, x3, x4, x5, x6]):
    ax.text(x, y0-0.5, f'x{i}', ha='center', fontsize=10, fontweight='bold')

for i, y in enumerate([y0, y1, y2, y3]):
    ax.text(x0-0.5, y, f'y{i}', va='center', fontsize=10, fontweight='bold')

# Add legend
ax.legend(loc='upper right', fontsize=10)

# Save as high-resolution JPG
plt.savefig('zeybek1_geological_map.jpg', dpi=300, bbox_inches='tight', quality=95)
plt.show()

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
