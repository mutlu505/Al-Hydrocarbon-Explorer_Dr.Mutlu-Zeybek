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
        f'{scale_length} units', ha='center', fontsize=11, fontweight='bold')

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

# Major Hydrocarbon Basins of the World Referenced in ZEYBEK-1 Model Framework
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
import cartopy.feature as cfeature
from matplotlib.patches import Rectangle, FancyBboxPatch
import numpy as np

# Create figure with higher resolution and set projection
fig = plt.figure(figsize=(20, 12))
ax = fig.add_subplot(1, 1, 1, projection=ccrs.Robinson(central_longitude=0))

# Set global extent
ax.set_global()

# Add map features with better styling
ax.add_feature(cfeature.LAND, facecolor='lightgray', edgecolor='darkgray', alpha=0.7)
ax.add_feature(cfeature.OCEAN, facecolor='lightblue', alpha=0.3)
ax.add_feature(cfeature.COASTLINE, linewidth=0.5, edgecolor='darkgray')
ax.add_feature(cfeature.BORDERS, linewidth=0.3, edgecolor='gray', alpha=0.5)
ax.add_feature(cfeature.LAKES, facecolor='lightblue', alpha=0.5)
ax.add_feature(cfeature.RIVERS, linewidth=0.3, edgecolor='lightblue', alpha=0.5)

# Add gridlines
gl = ax.gridlines(draw_labels=True, linestyle='--', linewidth=0.3, color='gray', alpha=0.5)
gl.top_labels = False
gl.right_labels = False
gl.xlabel_style = {'size': 8}
gl.ylabel_style = {'size': 8}

# Define major hydrocarbon basins with enhanced properties
# Format: [name, longitude, latitude, basin_type, size, marker, color, examples]
basins = [
    # North America
    ("Permian Basin", -102.5, 32.0, "Cratonic", 150, "s", "#1f77b4", "Permian Basin, Williston Basin"),
    ("Williston Basin", -103.0, 48.0, "Cratonic", 120, "s", "#1f77b4", "Bakken Formation"),
    ("Gulf of Mexico", -90.0, 28.0, "Passive Margin", 200, "o", "#ff7f0e", "Deep-water Gulf"),
    ("San Joaquin Basin", -120.0, 35.5, "Strike-slip", 100, "D", "#9467bd", "California"),
    
    # South America
    ("Brazil Margin", -40.0, -25.0, "Passive Margin", 180, "o", "#ff7f0e", "Santos Basin, Campos Basin"),
    ("Andes Foreland", -65.0, -30.0, "Foreland", 150, "^", "#2ca02c", "Zagros类比"),
    
    # Europe
    ("North Sea", 2.0, 58.0, "Extensional Rift", 160, "v", "#d62728", "Viking Graben"),
    ("Carpathians", 22.0, 47.0, "Foreland", 120, "^", "#2ca02c", "Polish Carpathians"),
    ("Pannonian Basin", 19.0, 46.5, "Extensional", 130, "v", "#d62728", "Hungary"),
    ("Barents Sea", 30.0, 73.0, "Passive Margin", 140, "o", "#ff7f0e", "Nordkapp Basin"),
    ("North Iberian Margin", -5.0, 43.5, "Passive Margin", 100, "o", "#ff7f0e", "Asturian Basin"),
    
    # Africa
    ("Gulf of Suez", 33.5, 28.0, "Extensional Rift", 150, "v", "#d62728", "Ashrafi Field"),
    ("East Africa Rift", 35.0, -5.0, "Extensional Rift", 170, "v", "#d62728", "Turkana, Albertine"),
    ("West Africa Margin", 5.0, -5.0, "Passive Margin", 190, "o", "#ff7f0e", "Niger Delta, Dahomey"),
    ("North Western Desert", 27.0, 29.5, "Extensional", 130, "v", "#d62728", "Abu Sennan Field"),
    ("Egyptian Red Sea", 34.5, 24.0, "Extensional Rift", 120, "v", "#d62728", "Northern Red Sea"),
    
    # Middle East
    ("Zagros Fold Belt", 52.0, 30.0, "Foreland", 180, "^", "#2ca02c", "Iran, Iraq"),
    ("Arabian Platform", 48.0, 26.0, "Cratonic", 200, "s", "#1f77b4", "Saudi Arabia"),
    ("Dead Sea Transform", 35.5, 31.5, "Strike-slip", 110, "D", "#9467bd", "Levant"),
    
    # Asia
    ("Tarim Basin", 82.0, 39.0, "Cratonic/Strike-slip", 170, "s", "#1f77b4", "Shunbei Field"),
    ("Sichuan Basin", 105.0, 30.0, "Foreland", 160, "^", "#2ca02c", "Ultra-deep gas"),
    ("Junggar Basin", 86.0, 45.0, "Foreland", 150, "^", "#2ca02c", "Southern margin"),
    ("Songliao Basin", 125.0, 46.0, "Extensional", 140, "v", "#d62728", "Gulong Shale"),
    ("Qaidam Basin", 92.0, 37.5, "Extensional", 130, "v", "#d62728", "Western Qaidam"),
    ("Erlian Basin", 114.0, 43.0, "Extensional", 120, "v", "#d62728", "Late Cretaceous"),
    ("East China Sea", 125.0, 28.0, "Passive Margin", 140, "o", "#ff7f0e", "Shelf basins"),
    
    # Australia
    ("Vulcan Sub-basin", 124.0, -12.0, "Passive Margin", 130, "o", "#ff7f0e", "NW Australia"),
    
    # Other regions
    ("Pakistan Shale", 68.0, 27.0, "Cratonic", 110, "s", "#1f77b4", "Potential shales"),
]

# Plot basins with different markers for each type
type_markers = {
    "Extensional Rift": {"marker": "v", "color": "#d62728", "label": "Extensional Rift"},
    "Extensional": {"marker": "v", "color": "#d62728", "label": "Extensional"}, 
    "Passive Margin": {"marker": "o", "color": "#ff7f0e", "label": "Passive Margin"},
    "Foreland": {"marker": "^", "color": "#2ca02c", "label": "Foreland Thrust Belt"},
    "Cratonic": {"marker": "s", "color": "#1f77b4", "label": "Cratonic Basin"},
    "Strike-slip": {"marker": "D", "color": "#9467bd", "label": "Strike-slip System"},
    "Cratonic/Strike-slip": {"marker": "s", "color": "#9467bd", "label": "Cratonic/Strike-slip"},
}

# Plot each basin
for basin in basins:
    name, lon, lat, btype, size, _, _, examples = basin
    
    # Get marker properties
    if btype in type_markers:
        marker = type_markers[btype]["marker"]
        color = type_markers[btype]["color"]
    else:
        marker = "o"
        color = "gray"
    
    # Scale size based on basin importance
    scale = size / 30
    
    # Plot the basin
    ax.plot(lon, lat, marker=marker, color=color, markersize=scale, 
            markeredgecolor='black', markeredgewidth=0.5, transform=ccrs.PlateCarree(),
            alpha=0.9, zorder=5)
    
    # Add label for major basins (offset to avoid overlap)
    if size >= 150:  # Only label major basins to avoid clutter
        offset_lon = lon + 2
        offset_lat = lat + 1
        ax.text(offset_lon, offset_lat, name, fontsize=8, fontweight='bold',
                transform=ccrs.PlateCarree(), ha='left', va='bottom',
                bbox=dict(boxstyle="round,pad=0.3", facecolor='white', alpha=0.7, edgecolor='gray'))

# Create custom legend
legend_elements = []
for btype, props in type_markers.items():
    if btype != "Cratonic/Strike-slip":  # Skip duplicate
        legend_elements.append(plt.Line2D([0], [0], marker=props["marker"], color='w',
                                          markerfacecolor=props["color"], markersize=10,
                                          label=props["label"], markeredgecolor='black'))

# Add legend
ax.legend(handles=legend_elements, loc='lower left', fontsize=10, 
          title="Basin Types", title_fontsize=11, framealpha=0.9)

# Add title with styling
plt.title("Major Hydrocarbon Basins of the World\nReferenced in ZEYBEK-1 Model Framework", 
          fontsize=16, fontweight='bold', pad=20)

# Add text box with basin statistics
stats_text = "Key Basins Referenced in Paper:\n" + \
             "• Gulf of Suez (Ashrafi Field) - Primary validation\n" + \
             "• North Sea - Extensional rift\n" + \
             "• Tarim Basin - Ultra-deep/Strike-slip\n" + \
             "• Zagros - Foreland thrust belt\n" + \
             "• Permian Basin - Cratonic\n" + \
             "• Sichuan Basin - Ultra-deep gas\n" + \
             "• West Africa Margin - Passive margin\n" + \
             "• San Joaquin - Strike-slip"

# Add text box
plt.text(0.02, 0.98, stats_text, transform=plt.gca().transAxes, fontsize=9,
         verticalalignment='top', bbox=dict(boxstyle="round,pad=0.5", 
                                          facecolor='lightyellow', alpha=0.9, edgecolor='black'))

# Add scale bar (approximate)
ax.plot([-150, -130], [-55, -55], color='black', linewidth=2, transform=ccrs.PlateCarree())
ax.text(-140, -58, "~2000 km", ha='center', fontsize=8, transform=ccrs.PlateCarree(),
        bbox=dict(facecolor='white', alpha=0.7, edgecolor='none'))

plt.tight_layout()
plt.savefig('major_hydrocarbon_basins_world_map.png', dpi=600, bbox_inches='tight')
plt.show()
