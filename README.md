# Al-Hydrocarbon-Explorer_Dr.Mutlu-Zeybek
# ZEYBEK-1 MODEL: Structural Trap Identification Map
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.patches import Rectangle, FancyArrowPatch
from matplotlib.lines import Line2D

# Create figure
fig, ax = plt.subplots(figsize=(16, 10), dpi=600)

# Define coordinates
x0, x1, x2, x3, x4, x5, x6 = 0, 2, 4, 6, 8, 10, 18
y0, y1, y2, y3 = -2, 1, 5, 7

# Plot lithology units
# L1 (Source Rock - Brown)
ax.add_patch(Rectangle((x0, y0), x6-x0, y1-y0, facecolor='brown', alpha=0.6, label='L1 Source Rock'))
# L2 (Reservoir Rock - Yellow)
ax.add_patch(Rectangle((x0, y1), x6-x0, y2-y1, facecolor='yellow', alpha=0.6, label='L2 Reservoir Rock'))
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

# ============================================
# ADD NORTH ARROW
# ============================================
# Arrow start point (top left corner)
arrow_start = (x0 + 0.5, y3 - 1.5)
arrow_end = (x0 + 0.5, y3 - 0.5)

# Draw north arrow
arrow = FancyArrowPatch(arrow_start, arrow_end, 
                        arrowstyle='->', 
                        mutation_scale=30, 
                        color='black', 
                        linewidth=2)
ax.add_patch(arrow)

# Add 'N' letter (North)
ax.text(arrow_start[0], arrow_start[1] + 0.2, 'N', 
        fontsize=16, fontweight='bold', ha='center', va='bottom')

# Add 'NORTH' text
ax.text(arrow_start[0] + 0.3, (arrow_start[1] + arrow_end[1])/2, 'NORTH', 
        fontsize=12, fontweight='bold', ha='left', va='center', rotation=90)

# ============================================
# ADD SCALE BAR
# ============================================
# Scale bar coordinates (bottom left)
scale_x_start = x0 + 15
scale_x_end = x0 + 17  # 2 unit length scale
scale_y = y0 + 0.5

# Draw scale bar (thick black line)
ax.plot([scale_x_start, scale_x_end], [scale_y, scale_y], 
        'k-', linewidth=4)

# Add vertical lines at scale bar ends
ax.plot([scale_x_start, scale_x_start], [scale_y-0.2, scale_y+0.2], 
        'k-', linewidth=2)
ax.plot([scale_x_end, scale_x_end], [scale_y-0.2, scale_y+0.2], 
        'k-', linewidth=2)

# Write scale value
scale_length = scale_x_end - scale_x_start
ax.text((scale_x_start + scale_x_end)/2, scale_y - 0.4, 
        f'{scale_length} kilometers', ha='center', fontsize=11, fontweight='bold')

# Add 'SCALE' label
ax.text(scale_x_start - 0.5, scale_y, 'SCALE', 
        fontsize=11, fontweight='bold', ha='right', va='center')

# ============================================
# ALTERNATIVE: Simple Scale Bar
# ============================================
# For a simpler scale bar, you can use the code below:
# from matplotlib.patches import FancyBboxPatch
# scale_bar = FancyBboxPatch((x0+1, y0+0.3), 2, 0.2, boxstyle="round,pad=0.1",
#                            facecolor='black', alpha=0.8)
# ax.add_patch(scale_bar)
# ax.text(x0+2, y0+0.1, '2 units', ha='center', fontsize=10)

# Add legend
ax.legend(loc='upper right', fontsize=10)

# Save as high-resolution JPG
plt.savefig('zeybek1_geological_map_with_scale_and_north.jpg', dpi=600, bbox_inches='tight', quality=95)
plt.show()

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
